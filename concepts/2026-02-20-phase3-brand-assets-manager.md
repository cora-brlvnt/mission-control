# Phase 3: Brand Assets Manager — Live Asset Library UI

**Date:** February 20, 2026  
**Status:** ✅ Deployed to GitHub, waiting for 3-step Supabase activation  
**Tech:** Supabase (PostgreSQL + file storage) + React + Next.js  
**Cost:** Free (uses existing Supabase project)

---

## Overview

Live UI for managing brand assets (logos, images, fonts) per brand. Extends Phase 2 Onboarding Platform with asset management capability. Enables Marketing Asset Generator to pull brand assets dynamically.

---

## What Phase 3 Does

### For Berelvant Team
- **Upload brand assets** (logos, hero images, product shots, fonts)
- **Organize by brand** (Berelvant + multiple client brands)
- **View asset library** (grid of all assets per brand)
- **Get direct URLs** (use in emails, templates, campaigns)

### For Marketing Asset Generator
- **Fetch brand assets** on demand (logos, images, fonts)
- **Generate variations** using uploaded brand imagery
- **Maintain consistency** across all client-facing assets

### For Multi-Brand Scaling
- **New client?** Create new brand folder, upload assets, go live
- **Switch brands?** Choose from dropdown, all assets load immediately
- **Reusable templates** across brands (same platform, different brand)

---

## Database Schema

### brands Table
```sql
id (UUID)
name (TEXT) — "Berelvant", "Client A", etc.
slug (TEXT) — "berelvant", "client-a", etc.
description (TEXT)
created_at, updated_at
```

### assets Table
```sql
id (UUID)
brand_id (UUID) → brands.id
filename (TEXT) — "berelvant-logo.svg"
file_type (TEXT) — "logo", "image", "font"
file_url (TEXT) — Public S3 URL
file_size (INTEGER)
usage (TEXT) — "brand logo", "hero image", etc.
uploaded_at, updated_at
```

### brands_with_assets View
```sql
Aggregates assets per brand as JSON:
{
  "images": [
    { "name": "hero-light.jpg", "file": "s3://...", "usage": "homepage hero" }
  ],
  "logos": [
    { "name": "logo.svg", "file": "s3://...", "usage": "brand logo" }
  ],
  "fonts": [
    { "name": "Satoshi-Bold.ttf", "file": "s3://...", "usage": "headings" }
  ]
}
```

---

## React Components

### BrandList
- Shows all brands in grid/list
- Click to view brand detail
- Add new brand button

### BrandDetail
- Brand name, description, created date
- Asset gallery (organized by type)
- Upload new asset form (drag-drop)
- Delete asset option

### AssetUploadForm
- Drag-drop or click to select file
- File type selector (logo, image, font)
- Usage description field
- Submit → Supabase storage

### AssetGallery
- Grid of assets organized by type
- Hover to see metadata (filename, size, upload date)
- Click to copy direct URL
- Delete button

---

## Deployment Path (3 Steps)

### Step 1: Create Database Schema (90 seconds)
- Go to Supabase SQL editor
- Paste SQL migration file
- Click Run
- Schema created: brands, assets, brands_with_assets view

### Step 2: Create Storage Bucket (90 seconds)
- Go to Supabase Storage
- New bucket: `brand-assets` (set to Public)
- Creates public file storage for all brand assets

### Step 3: Verify on Production (2 minutes)
- Visit: https://berelvant-onboarding-platform-production.up.railway.app/brand-assets
- Should see brand list
- Test upload: Click brand → drag PNG → verify in gallery

**Total time:** ~3 minutes  
**No technical risk:** Supabase auto-handles schema migrations + storage

---

## Integration Points

### Incoming (from Onboarding Platform)
- **Brand context:** Which brand's assets to display
- **Asset filters:** Show only logos, or only images, etc.

### Outgoing (to Marketing Asset Generator)
- **Brand manifest:** Brand name, description, asset URLs
- **Asset URLs:** Direct S3 links for use in prompts
- **Asset metadata:** File type, size, usage description

### Real-time Features
- **File upload:** Asset appears in gallery immediately (Supabase real-time)
- **Asset deletion:** Removes from gallery + S3 immediately
- **Brand switching:** Switch brand → load different asset gallery instantly

---

## Multi-Brand Use Case

### Adding a New Client Brand

**Day 1:** Client signed up via Onboarding Platform
```
Onboarding Platform creates:
- brands row: id=UUID, name="Client A", slug="client-a"
- Dashboard shows "Client A" created
```

**Day 2:** Upload Client A's brand assets
```
Visit: /brand-assets
Select: "Client A"
Upload: logo.svg, hero.jpg, Satoshi-Bold.ttf
Verify: All assets appear in gallery
```

**Day 3:** Use Client A's brand for content generation
```
Marketing Asset Generator:
  Input: --brand="client-a" --platform="instagram"
  Output: Asset generator pulls client-a logos/images
  Result: Instagram posts branded for Client A
```

---

## Security & Access Control

### RLS Policies
- All users can view all brands
- All users can upload assets
- All users can delete assets
- **Future:** Add org/team scoping if multi-tenant needed

### File Security
- Public bucket (no auth required to view)
- Supabase handles CORS + CDN distribution
- Files are versioned in Supabase (history preserved)

### Data Safety
- Soft deletes available (mark asset as deleted, keep S3 copy)
- Backup: All assets stored in Supabase + replicated S3

---

## Measurement & Success Metrics

| Metric | Target | Purpose |
|--------|--------|---------|
| Brands created | 3+ by March 31 | Multi-brand adoption |
| Assets uploaded | 50+ total | Rich asset library |
| Asset reuse rate | 70%+ across campaigns | Leverage on brand investments |
| Marketing assets generated | 100+ by March 31 | Product-market fit |
| Time to new brand | <30 min | Ease of onboarding |

---

## Roadmap (Phase 4+)

### Phase 4: Brand Template Library
- Pre-designed ad templates per brand
- Email templates with brand colors/fonts
- Landing page components

### Phase 5: AI Brand Variations
- Auto-generate dark mode variants from light logos
- Auto-crop images for different platforms
- Auto-resize fonts for optimal readability

### Phase 6: Brand Performance Dashboard
- Track engagement on assets by brand
- Which brand colors perform best?
- Which imagery style gets highest CTR?
- Optimize future assets based on data

---

## Status & Rollout

**Current:** ✅ Code deployed to GitHub, Supabase steps documented

**Activation:** Renzo's 3-step process (takes ~3 minutes)

**Timeline:**
- Feb 20: Code pushed, waiting for activation
- Feb 21-23: Renzo can activate if ready
- Feb 24+: Full integration with Marketing Asset Generator
- March 1+: Scale to 3+ client brands

---

## Files & Locations

**Code:** https://github.com/cora-brlvnt/onboarding-platform (branch: main)

**Setup guides:**
- `PHASE3_QUICK_START.md` — 3-step execution guide
- `PHASE3_AUTOMATED_SETUP.md` — Detailed SQL + setup

**Live URL:**
- https://berelvant-onboarding-platform-production.up.railway.app/brand-assets (after activation)

---

## Key Success Factor

**Simplicity.** Phase 3 is not complex software; it's a simple CRUD interface on Supabase. The value is:
1. Centralizing brand assets in one place
2. Making them accessible to automated systems (Marketing Asset Generator)
3. Enabling multi-brand at scale

Everything else is implementation detail.
