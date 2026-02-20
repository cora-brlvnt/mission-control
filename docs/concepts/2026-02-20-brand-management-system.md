# Brand Management System — Centralized Library

**Date:** February 20, 2026  
**Status:** ✅ Live  
**Location:** `/Users/cora/.openclaw/workspace/brands/`  
**Tech:** JSON manifests + file-based asset storage  
**Cost:** Free (local storage)

---

## Overview

Centralized multi-brand asset library supporting Berelvant, client brands, and internal projects. Powers the Marketing Asset Generator skill and enables rapid, consistent asset creation across brands and platforms.

---

## Architecture

### Directory Structure

```
brands/
├── berelvant/
│   ├── manifest.json         # Brand identity + guidelines
│   ├── logos/
│   │   ├── logo.svg          # Full logo
│   │   ├── logo-dark.svg     # Dark mode variant
│   │   ├── logomark.svg      # Icon only
│   │   └── favicon.ico       # Web favicon
│   ├── images/
│   │   ├── hero-light.jpg    # Homepage hero
│   │   ├── hero-dark.jpg     # Dark mode hero
│   │   ├── team.jpg          # Team photo
│   │   ├── office.jpg        # Office/workspace
│   │   └── product.jpg       # Product screenshot
│   ├── fonts/
│   │   ├── Satoshi-Bold.ttf
│   │   ├── Satoshi-Regular.ttf
│   │   ├── Satoshi-Medium.ttf
│   │   └── SatoshiMono-Regular.ttf
│   ├── guidelines.md         # Brand voice, tone, usage rules
│   └── palette.json          # Color definitions + accessibility
├── [client-brand-1]/
│   └── [same structure]
├── [client-brand-2]/
│   └── [same structure]
└── README.md                 # System overview & setup
```

---

## Brand Manifest (manifest.json)

### Example: Berelvant

```json
{
  "name": "Berelvant",
  "slug": "berelvant",
  "description": "AI growth infrastructure for enterprises",
  
  "identity": {
    "positioning": "AI Growth Architect + Automation Systems Builder",
    "mission": "Help growth teams escape AI hype and build real infrastructure",
    "tone": "Direct, credible, systems-minded, practical"
  },
  
  "colors": {
    "primary": {
      "name": "Blue",
      "hex": "#3b82f6",
      "rgb": "rgb(59, 130, 246)",
      "usage": "Primary CTA, headings, highlights"
    },
    "secondary": {
      "name": "Dark Gray",
      "hex": "#1f2937",
      "rgb": "rgb(31, 41, 55)",
      "usage": "Text, backgrounds, structure"
    },
    "accent": {
      "name": "Amber",
      "hex": "#fbbf24",
      "rgb": "rgb(251, 191, 36)",
      "usage": "Warnings, highlights, data viz"
    },
    "neutrals": {
      "light": "#f3f4f6",
      "medium": "#d1d5db",
      "dark": "#4b5563"
    }
  },
  
  "typography": {
    "headings": {
      "font": "Satoshi Bold",
      "size": "32px-48px",
      "line_height": "1.2",
      "weight": "700",
      "letter_spacing": "-0.02em"
    },
    "body": {
      "font": "Satoshi Regular",
      "size": "14px-16px",
      "line_height": "1.6",
      "weight": "400"
    },
    "cta": {
      "font": "Satoshi Bold",
      "size": "14px",
      "weight": "700",
      "text_transform": "none"
    }
  },
  
  "assets": {
    "logo": "logos/logo.svg",
    "logomark": "logos/logomark.svg",
    "hero_light": "images/hero-light.jpg",
    "hero_dark": "images/hero-dark.jpg",
    "favicon": "logos/favicon.ico"
  },
  
  "guidelines": {
    "logo_clearspace": "20px minimum",
    "logo_min_width": "120px",
    "color_contrast_ratio": "WCAG AA minimum",
    "brand_voice_keywords": ["direct", "practical", "credible", "systems-minded"],
    "avoid": ["hype", "generic AI buzzwords", "empty claims", "vague positioning"]
  },
  
  "metadata": {
    "created": "2026-02-20",
    "updated": "2026-02-20",
    "owner": "Renzo Proano",
    "domains": ["berelvant.com", "renzoproano.com"]
  }
}
```

---

## Brand Guidelines (guidelines.md)

### Example Content

**Voice & Tone**
- Direct: No filler, get to the point
- Credible: Back claims with data, not hype
- Practical: Focus on implementation, not theory
- Systems-minded: Show how pieces fit together

**Words to Use**
- Framework, infrastructure, measurable, leverage, compounding, system, integration

**Words to Avoid**
- AI will change everything, revolutionary, disruption, hype, cutting-edge, buzzwords

**Visual Identity**
- Clean, minimal aesthetic (not "AI slop")
- Blue + dark gray primary palette
- Satoshi font (modern, readable, distinctive)
- Real imagery (teams, workflows, offices—not stock photos)

**Copy Standards**
- Headlines: Active voice, benefit-driven
- Body: 1-2 sentences max per paragraph
- CTAs: Specific action (not "Learn More")
- Case studies: Numbers first, story second

---

## Integration with Marketing Asset Generator

### Skill Usage

```javascript
// Generator reads brand manifest
const brandConfig = require('brands/berelvant/manifest.json');

// Applies guidelines to generated assets
assets.apply_brand_colors(brandConfig.colors);
assets.apply_typography(brandConfig.typography);
assets.validate_contrast(brandConfig.guidelines.color_contrast_ratio);
assets.validate_voice(brandConfig.identity.tone);
```

### Asset Generation Flow

1. **Fetch brand config** → manifest.json
2. **Load assets** → logos, images, fonts
3. **Apply styling** → colors, typography
4. **Render** → Gemini 3 Pro Image (nano-banana-pro)
5. **Validate** → Brand compliance check
6. **Output** → PNG + metadata.json

---

## Multi-Brand Workflow

### Adding a New Client Brand

```bash
# 1. Create folder
mkdir -p brands/new-client/{logos,images,fonts}

# 2. Create manifest.json (copy from template)
cp brands/manifest-template.json brands/new-client/manifest.json

# 3. Add assets
cp -r /path/to/client/logos/* brands/new-client/logos/
cp -r /path/to/client/images/* brands/new-client/images/

# 4. Update manifest with client specifics
vim brands/new-client/manifest.json

# 5. Test generation
openclaw skill run marketing-asset-generator --brand="new-client" --test
```

### Generating Assets for Multiple Brands

```bash
openclaw skill run marketing-asset-generator \
  --task="Q1 Social Media Pack" \
  --brands="berelvant,client-a,client-b" \
  --platform="instagram_feed,linkedin" \
  --batch
```

Output: 
```
assets/berelvant_instagram_feed_*.png
assets/berelvant_linkedin_*.png
assets/client-a_instagram_feed_*.png
assets/client-a_linkedin_*.png
... (etc for client-b)
```

---

## Governance & Updates

### Brand Changes
- Update `manifest.json` when identity changes
- Version control all changes (git commit with reason)
- Notify team of new guidelines

### Asset Maintenance
- Review brand images annually (keep current)
- Update fonts if licensing/quality improves
- Archive obsolete logos (don't delete, keep in git history)

### Quality Standards
- Logo usage: Always maintain clearspace + minimum width
- Color contrast: WCAG AA minimum (7:1 for body text)
- Typography: Consistent sizing and weight across platform
- Voice: Every asset reflects brand tone

---

## Measurement

- **Consistency score:** % of assets compliant with guidelines (target: 100%)
- **Brand recognition:** How often brand elements trigger immediate recognition (qualitative + surveys)
- **Asset reuse:** How many campaign materials use library (track via ClickUp)
- **Time to market:** Average time from request to final asset (target: <2 hours for batch)

---

## Status & Next Actions

**Current:** ✅ Live, integrated with Marketing Asset Generator, ready for multi-brand production

**Next:**
1. Onboard first client brand (copy template, customize)
2. Create asset templates for each platform (reusable starting points)
3. Document brand voice with examples (do's/don'ts)
4. Measure consistency score on first batch of generated assets
5. Plan quarterly brand review process

---

## Files & Locations

- **System root:** `/Users/cora/.openclaw/workspace/brands/`
- **Manifest template:** `brands/manifest-template.json`
- **Guidelines template:** `brands/guidelines-template.md`
- **Asset generator:** `/skills/marketing-asset-generator/`
- **Storage:** Google Drive `/Berelvant/Marketing Assets/` (auto-synced)
