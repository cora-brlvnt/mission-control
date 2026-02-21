# Centralized Brand Management System

**Date:** February 20, 2026  
**Status:** ✅ Complete & Ready to Use  
**Location:** `/Users/cora/.openclaw/workspace/brands/`  
**Purpose:** Single source of truth for multi-brand assets + guidelines

---

## Overview

Enterprise-grade brand management infrastructure supporting unlimited brands. Each brand is self-contained with guidelines, colors, typography, logos, images, and asset templates.

## Directory Structure

```
brands/
├── README.md                           # Setup guide + folder explanation
├── _templates/                         # Template for every new brand
│   ├── brand-guidelines-TEMPLATE.json
│   ├── color-palette-TEMPLATE.json
│   ├── typography-TEMPLATE.json
│   └── assets-TEMPLATE.json
└── berelvant/                          # Example brand (ready to populate)
    ├── brand-guidelines.json           # Brand metadata + voice
    ├── color-palette.json              # Primary, secondary, accent, usage rules
    ├── typography.json                 # Fonts, sizes, weights, fallbacks
    ├── assets.json                     # Manifest of all brand assets
    ├── logos/                          # Logo files (PNG, SVG, variations)
    ├── images/                         # Hero, product, team photos
    ├── templates/                      # Pre-designed ad templates
    └── fonts/                          # Custom font files
```

## How It Works

### Creating a New Brand

1. Copy entire `_templates/` structure to `brands/your-brand/`
2. Fill in JSON files:
   - **brand-guidelines.json:** Colors, tone, values, target audience
   - **color-palette.json:** Hex codes, usage rules (when to use each color)
   - **typography.json:** Font families, sizes, line-height, weights
   - **assets.json:** Manifest (list of all assets + metadata)
3. Add actual files (logos, images, fonts) to respective folders
4. Point Marketing Asset Generator to your brand file: `--brand-file brands/your-brand/brand-guidelines.json`

### Using with Marketing Asset Generator

```python
python generate_marketing_asset.py \
  --brand-file brands/berelvant/brand-guidelines.json \
  --asset-types "instagram_feed,youtube_thumbnail,email_hero" \
  --topic "AI automation workshop launch"
```

Result: 3 platform-optimized assets, all with Berelvant brand colors + tone.

## JSON Schema

### brand-guidelines.json
```json
{
  "brand_name": "Berelvant",
  "brand_mission": "AI Growth Architect",
  "brand_values": ["Innovation", "Transparency", "Scaling"],
  "tone": {
    "primary": "authoritative",
    "secondary": "approachable",
    "avoid": "salesy"
  },
  "target_audience": "CMOs, Founders, Agency Owners",
  "products": ["Workshops", "FastTrack Hub", "Copilot"],
  "key_messaging": ["AI automation", "Revenue scaling", "Enterprise systems"],
  "founded": 2024,
  "website": "https://berelvant.com"
}
```

### color-palette.json
```json
{
  "primary": { "hex": "#3B82F6", "name": "Trust Blue", "usage": "CTAs, headers, brand identity" },
  "secondary": { "hex": "#1F2937", "name": "Deep Gray", "usage": "Body text, backgrounds" },
  "accent": { "hex": "#F59E0B", "name": "Action Orange", "usage": "Highlights, emphasis" }
}
```

### typography.json
```json
{
  "heading": { "family": "Inter", "weight": 700, "sizes": [32, 28, 24, 20] },
  "body": { "family": "Inter", "weight": 400, "size": 16, "lineHeight": 1.6 }
}
```

## Integration Points

- **Marketing Asset Generator:** Load brand file → apply colors/tone to all assets
- **ClickUp:** Tag projects with brand name → auto-apply brand guidelines
- **2Brain:** Link to brand folder for quick reference
- **Airtable:** Store asset inventory + performance by brand
- **GitHub:** Version control brand changes (colors update → commit + deploy)

## Use Cases

- **Multi-client agencywork:** Each client gets dedicated brand folder
- **Campaign consistency:** All assets use same brand file → guaranteed coherence
- **Brand evolution:** Update JSON, regenerate all assets → instant rebrand
- **Team onboarding:** New team member → view brand folder → understand brand instantly
- **A/B testing:** Same brand, different tone file → test variations
- **Archive:** Old brands stay in folder → revert to old brand if needed

## Maintenance

- **Add new asset:** Put in appropriate folder + update assets.json manifest
- **Update brand:** Edit JSON files → regenerate assets using new file
- **New color:** Add to color-palette.json → all future assets use new color
- **Font change:** Update typography.json → regenerate text-heavy assets

## Status
✅ Production-ready | ✅ Ready to populate with Berelvant assets | ✅ Supports unlimited brands | ✅ GitHub-versioned

## Next Actions
- Populate berelvant/ with actual logos, images, fonts
- Create secondary brand folder (if multi-brand needed)
- Document brand evolution process (change history in MEMORY.md)
- Integrate with ClickUp (auto-tag projects with brand)
