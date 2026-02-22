# Concept: Client Integration System for Mission Control

**Finalized:** February 22, 2026 (Evening)  
**Status:** Built, ready for deployment  
**Impact:** Centralized client data + on-brand agent outputs

---

## Overview

Client Integration connects the Onboarding Platform (where client details are stored) with Mission Control (where agents create deliverables). Agents pull client tone of voice and brand guidelines, ensuring all outputs match the client's brand.

---

## Architecture

### Data Model

**Clients Table:**
```json
{
  "id": "uuid",
  "name": "GCG Forex",
  "company": "Global Copy Group",
  "industry": "fintech/trading",
  "email": "gcg@forex.com",
  "website": "https://gcg.forex.com",
  "tone_of_voice": "Professional, energetic, accessible to traders",
  "google_drive_folder": "https://drive.google.com/drive/folders/xyz",
  "created_at": "2026-02-22T18:00:00Z"
}
```

**Tasks Table (Updated):**
```json
{
  "id": "uuid",
  "title": "Q2 GCG Campaign",
  "description": "...",
  "client_id": "uuid", // Links to clients table
  "approval_status": "pending", // pending → complete → in_review → approved
  "created_at": "2026-02-22T18:15:00Z"
}
```

### Data Flow

```
1. ONBOARDING PLATFORM
   - Add client (name, company, tone, Drive folder)
   - Store in Supabase clients table
   
2. MISSION CONTROL
   - Create task
   - Select client from dropdown
   - Task linked to client via client_id
   
3. AGENT RUNNER (every 15 min)
   - Read task from Supabase
   - Fetch client data (tone, Drive folder link)
   - All agents receive client context
   
4. AGENTS
   - Each agent uses client tone in their outputs
   - Vision: Include industry keywords from client
   - Echo: Write copy in client's tone
   - Pixel: Follow brand colors + fonts from Drive
   - Social: Use client voice per platform
   
5. DELIVERABLES
   - All outputs tagged with client_id
   - Dashboard shows "Deliverables for GCG Forex"
   - Client data baked into all recommendations
```

---

## User Interface

### Onboarding Platform - Client Management

**Page:** `/clients`

**UI Elements:**
- Text input: Client name
- Text input: Company name
- Select dropdown: Industry
- Text input: Email
- Text input: Website
- Text area: Tone of voice
- Text input: Google Drive folder link
- Buttons: Create, Edit, Delete
- Table: List of all clients

**Auth:** @berelvant.com domain only

---

### Mission Control - Client Selection

**Page:** Task creation form

**Change:** New dropdown field
- Label: "Select Client"
- Options: List of all clients from clients table
- Default: "—"
- Required: No (tasks can exist without client for generic work)

**Impact:** When agent runner executes, it knows which client → fetches tone + Drive link

---

## Agent Behavior Changes

### Vision (SEO Agent)
**Before:** Generic keyword research  
**After:** Client-focused keywords
- Search for client industry keywords (e.g., "forex broker" for Forex.com)
- Include competitor analysis for client niche
- Suggest content aligned with client ICP (industry, company size)

### Echo (Copywriter)
**Before:** Generic tone  
**After:** Client tone-aware
- Read client tone_of_voice field
- Generate 5 headlines matching that tone
- A/B test variations (energetic vs. professional)
- Ensure CTA matches client brand voice

### Pixel (Designer)
**Before:** Generic color palette  
**After:** Brand-guided design
- Check client Drive folder for brand guidelines
- Extract colors + fonts (or fallback to default)
- Create layouts using client brand palette
- Image prompts mention client industry context

### Social (Organic Social)
**Before:** Generic tone per platform  
**After:** Client tone × platform tone
- Use client voice (e.g., "professional but energetic")
- Adapt to platform norms (Instagram casual, LinkedIn formal)
- Hashtags specific to client industry

---

## Approval Workflow

### Status Progression

```
PENDING (default)
  ↓ (agents finish)
COMPLETE (deliverables ready)
  ↓ (Renzo reviews)
IN_REVIEW (being evaluated)
  ↓ (decision made)
APPROVED (ready to implement)
  ↓ (export + use)
IMPLEMENTED (task complete)
```

**Tracking:** Dashboard shows status for each task
**Admin controls:** Renzo can manually update status via task detail page

---

## Setup Steps

### 1. Create Clients Table

```sql
CREATE TABLE IF NOT EXISTS public.clients (
  id uuid DEFAULT gen_random_uuid() PRIMARY KEY,
  name TEXT NOT NULL,
  company TEXT,
  industry TEXT,
  email TEXT,
  website TEXT,
  tone_of_voice TEXT,
  google_drive_folder TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT timezone('utc'::text, now()),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT timezone('utc'::text, now())
);
```

### 2. Update Tasks Table

```sql
ALTER TABLE public.tasks ADD COLUMN IF NOT EXISTS client_id uuid REFERENCES public.clients(id);
ALTER TABLE public.tasks ADD COLUMN IF NOT EXISTS approval_status TEXT DEFAULT 'pending';
```

### 3. Add Row-Level Security (RLS)

```sql
ALTER TABLE public.clients ENABLE ROW LEVEL SECURITY;

CREATE POLICY IF NOT EXISTS "clients_read" ON public.clients
  FOR SELECT
  USING (auth.jwt() ->> 'email' LIKE '%@berelvant.com%');

CREATE POLICY IF NOT EXISTS "clients_admin" ON public.clients
  FOR ALL
  USING (auth.jwt() ->> 'email' = 'principal@berelvant.com');
```

### 4. Create Indexes

```sql
CREATE INDEX IF NOT EXISTS tasks_client_id_idx ON public.tasks(client_id);
CREATE INDEX IF NOT EXISTS clients_created_at_idx ON public.clients(created_at);
```

---

## Example Workflow

**Scenario:** Add GCG Forex as client, create task

### Step 1: Add Client (Onboarding Platform)
```
Name: GCG Forex
Company: Global Copy Group
Industry: fintech
Email: gcg@forex.com
Website: https://gcg.forex.com
Tone: "Professional, energetic, accessible to traders"
Drive: https://drive.google.com/drive/folders/xyz
```
→ Saved to Supabase clients table

### Step 2: Create Task (Mission Control)
```
Title: Q2 GCG Forex Campaign
Details: 500 leads in 2 weeks, $10K budget
Client: GCG Forex (dropdown select)
```
→ Task linked to client_id

### Step 3: Agents Run (Auto)
```
Vision: Reads client industry = "fintech" → searches "best forex broker", "forex trading app"
Echo: Reads tone = "professional, energetic" → writes copy matching that tone
Pixel: Reads Drive folder → extracts brand colors → designs using client palette
Social: Reads tone + industry → writes social posts with client voice + fintech hashtags
```

### Step 4: Deliverables Reference Client
```
All outputs tagged: "For: GCG Forex"
Copy matches their tone ✓
Design uses their colors ✓
Social posts use their voice ✓
```

---

## Benefits

| Benefit | Impact |
|---------|--------|
| **Centralized client data** | Single source of truth (Onboarding Platform) |
| **On-brand outputs** | Agents use actual client tone + brand guidelines |
| **Faster onboarding** | New clients fill form once, agents use forever |
| **Scalability** | Same system handles 1 client or 100 clients |
| **Approval workflow** | Track status, manage handoff between teams |
| **Audit trail** | Every task linked to client, clear history |

---

## Future Enhancements

1. **Client-visible dashboard** — Clients log in, see their projects
2. **File uploads** — Upload logos directly instead of Drive links
3. **Template library** — Save reusable client settings
4. **Reporting** — What was delivered to each client, ROI metrics
5. **Invoicing** — Tie tasks to billable hours or project budgets
6. **White-label** — Agencies can use Mission Control for their own clients

---

## Status

✅ **Code:** Complete and deployed  
✅ **UI:** Client form + dropdown + approval status  
✅ **Agents:** All 7 updated to use client data  
⏳ **Database:** SQL ready, awaiting manual migration  
⏳ **Testing:** Pending client data flow verification

**Deployment:** Merge to main + deploy to Railway + run SQL migration
