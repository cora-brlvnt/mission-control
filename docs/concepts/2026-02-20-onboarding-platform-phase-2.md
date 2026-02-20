# Phase 2 Onboarding Platform — Complete Production Stack

**Date:** February 20, 2026  
**Status:** ✅ Live  
**Tech:** Next.js 14 + React 18 + Supabase + Railway  
**Cost:** ~$5-10/month (Railway hosting)  
**Repo:** https://github.com/cora-brlvnt/onboarding-platform

---

## Overview

Production-grade onboarding platform for Berelvant client lifecycle management. Phase 2 adds real-time Supabase authentication, full CRUD operations for clients and workflows, and live dashboard data integration.

---

## Architecture

### Frontend
- **Framework:** Next.js 14 (React 18, TypeScript)
- **UI Components:** Shadcn/ui + Tailwind CSS
- **Features:** 
  - Real Supabase auth (email/password)
  - Client management (Create, Read, Update, Delete)
  - Workflow management (templates, automation setup)
  - Live dashboard with KPI cards

### Backend
- **Database:** Supabase PostgreSQL with Row-Level Security (RLS)
- **Auth:** Supabase Auth with session management
- **API:** Next.js API routes + Supabase client-side SDK

### Deployment
- **Hosting:** Railway (production)
- **URL:** https://berelvant-onboarding-platform-production.up.railway.app/
- **Auto-deploy:** GitHub → Railway (continuous)

---

## Capabilities (Phase 2)

### Client Management
- Create new client records (name, email, status, plan tier)
- Read client list with filtering + search
- Update client details (name, status, notes)
- Delete client (with soft-delete safety)
- Client dashboard (active count, revenue, churn)

### Workflow Management
- Pre-built workflow templates (Lead Capture, Email Sequence, Appointment Reminders, Pipeline Router, Two-Way SMS)
- Assign workflows to clients
- Track workflow status (active, paused, completed)
- Configuration UI for workflow parameters

### Dashboard
- Active client count
- Total onboarded clients (all-time)
- Revenue summary (retainer-based)
- Workflow activation rate
- Real-time KPI cards (auto-updated)

### Security
- Session-based auth (Supabase)
- RLS policies (users can only see their own data)
- Protected API routes
- CORS configured for Railway deployment

---

## Integration Points

**Who uses this:**
- Berelvant team (internal: client management)
- Sales (opportunity tracking, conversion metrics)
- Automation (workflow deployment trigger)
- Analytics (onboarding KPI dashboard)

**Incoming data:**
- GHL Workflows (lead capture → auto-client creation)
- Email sequences (triggered post-onboarding)
- Pipeline router (deal stage → workflow assignments)

**Outgoing data:**
- Client list → Telegram notifications (new signups)
- Workflow status → ClickUp task updates
- Revenue dashboard → MEMORY.md KPI tracking

---

## Measurement (KPIs)

- **Active clients:** Target 10-20 by end of March
- **Onboarding completion:** Target 70%+ (Day 1 → Day 7)
- **Workflow adoption:** Target 80%+ of clients activate workflow
- **Churn:** Target <5% monthly
- **NPS:** Target 8+ (post-launch survey)

---

## Roadmap (Phase 3+)

1. **Client success portal** (self-serve workflow configuration, progress tracking)
2. **Workflow analytics** (automation performance, lead conversion metrics)
3. **Email notifications** (client signup alerts, workflow completion reminders)
4. **Two-way sync** (GHL → Platform auto-create clients)
5. **Pricing tiers** (Starter, Pro, Enterprise with feature gates)

---

## Status & Next Actions

**Current:** ✅ Production-ready, live, tested end-to-end

**Next:**
1. Monitor error logs (Railway logs dashboard)
2. Measure first client adoption (post-workshop leads)
3. Plan self-serve portal (Phase 3)
4. Integration with GHL lead capture (auto-create clients)

---

## Documentation

- **Code:** https://github.com/cora-brlvnt/onboarding-platform
- **Supabase setup:** Schema migrations in `/migrations/` folder
- **Deployment:** Railway GitHub integration (auto-deploy on push to main)
- **API reference:** `/pages/api/clients`, `/pages/api/workflows`
