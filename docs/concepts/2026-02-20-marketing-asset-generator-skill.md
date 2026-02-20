# Marketing Asset Generator Skill — Production Ready

**Date:** February 20, 2026  
**Status:** ✅ Production-ready  
**Location:** `/Users/cora/.openclaw/workspace/skills/marketing-asset-generator/`  
**Tech:** Gemini 3 Pro Image (nano-banana-pro skill)  
**Cost:** Free (uses existing API credits)

---

## Overview

Production-grade OpenClaw skill for batch-generating marketing assets across 10+ platforms. Supports tone variations, A/B testing, brand compliance, and platform-specific optimization. Fully integrated with brand management system.

---

## Capabilities

### Supported Platforms (10+)

1. **Social Media**
   - Instagram (feed, stories, reels)
   - Facebook (feed, ads, carousel)
   - LinkedIn (post images, articles, company page)
   - TikTok (landscape, vertical, square)
   - X/Twitter (thread headers, quotes, links)

2. **Email & Web**
   - Email headers (hero images)
   - Landing page headers
   - Blog post thumbnails
   - Website banners

3. **Video**
   - YouTube thumbnails (optimized CTR)
   - Video intro/outro cards
   - Teaser cards for reels

### Features

- **Tone variations:** Professional, playful, data-driven, storytelling
- **A/B testing:** Generate 2-3 variations per asset (test winning combinations)
- **Brand compliance:** Uses centralized brand library (logos, fonts, colors, guidelines)
- **Batch generation:** Create 5-10 assets in single request
- **Platform optimization:** Correct aspect ratios, safe zones, text sizing per platform
- **Multi-brand support:** Switch between client brands seamlessly

---

## Workflow Integration

### Input
```
task: "Generate Instagram feed posts for Q1 campaign"
brand: "berelvant"  // Uses /Users/cora/.openclaw/workspace/brands/berelvant/ assets
variations: 3
platforms: ["instagram_feed"]
tone: ["professional", "playful"]
```

### Output
```
assets/
├── berelvant_instagram_feed_variation1.png
├── berelvant_instagram_feed_variation2.png
├── berelvant_instagram_feed_variation3.png
└── metadata.json  // Descriptions, copy suggestions, alt text
```

### Copy Generation
- Headlines (strong, benefit-driven)
- Body copy (2-3 sentences)
- CTA buttons (Download, Learn More, Join)
- Alt text (accessible, SEO)

---

## Brand Management System (Coupled)

**Location:** `/Users/cora/.openclaw/workspace/brands/`

**Structure per brand:**
```
brands/
├── berelvant/
│   ├── manifest.json  (guidelines, colors, fonts)
│   ├── logos/
│   │   ├── logo.svg
│   │   ├── logo-dark.svg
│   │   └── logomark.svg
│   ├── images/
│   │   ├── hero.jpg
│   │   ├── team.jpg
│   │   └── product.jpg
│   ├── fonts/
│   │   ├── SatoshiBold.ttf
│   │   └── SatoshiRegular.ttf
│   └── guidelines.md
└── [other-brand]/
```

**manifest.json example:**
```json
{
  "brand": "berelvant",
  "primary_color": "#3b82f6",
  "secondary_color": "#1f2937",
  "accent_color": "#fbbf24",
  "typography": {
    "heading_font": "Satoshi Bold",
    "body_font": "Satoshi Regular",
    "cta_font": "Satoshi Bold"
  },
  "tone": "Direct, credible, systems-minded, practical",
  "positioning": "AI Growth Architect, not 'marketer who runs ads'"
}
```

---

## Use Cases

### 1. Campaign Launch
- Generate hero images for email + landing page
- Create social variations (Instagram, LinkedIn, Twitter)
- A/B test 2 headlines + 2 imagery styles

### 2. Content Marketing
- Batch-generate blog thumbnails for Q1 posts (10 articles)
- YouTube thumbnail variations (test thumbnail elements)
- Social quotes + callout graphics

### 3. Ads & Promotion
- Facebook/Instagram ad creatives (image + carousel variations)
- Display ads (GDN-sized banners)
- Retargeting creative variants

### 4. Multi-Brand Agency Work
- Switch brands in single script (avoid manual rebranding)
- Maintain consistency across client assets
- Batch export for client delivery

---

## Skill Commands

```
// Generate Instagram posts
openclaw skill run marketing-asset-generator --task="Instagram feed posts" --brand="berelvant" --platform="instagram_feed" --count=5

// A/B test variations
openclaw skill run marketing-asset-generator --task="Email hero" --variations=3 --tone="professional,playful"

// Multi-brand batch
openclaw skill run marketing-asset-generator --task="Q1 thumbnails" --brands="berelvant,forex-proxy" --platform="youtube"

// List available brands
openclaw skill run marketing-asset-generator --list-brands
```

---

## Integration Points

**Connected systems:**
- **Gemini 3 Pro Image:** Rendering engine (nano-banana-pro skill)
- **Brand management:** `/Users/cora/.openclaw/workspace/brands/`
- **Content calendar:** ClickUp (link to generated assets)
- **Asset storage:** Google Drive `/Berelvant/Marketing Assets/` (auto-upload)
- **Measurement:** Asset engagement tracking (Instagram insights, YouTube CTR)

---

## Measurement (Success Metrics)

- **Time saved:** Measure hours spent on asset creation (before/after)
- **Consistency:** Brand compliance score (100% on guidelines match)
- **Efficiency:** Assets per hour (target: 5-10 per session)
- **Quality:** Engagement rates (Instagram posts, email CTR, landing page conversion)
- **Adoption:** Usage frequency (weekly, campaigns/month)

---

## Roadmap (Future)

1. **Video generation:** Reel templates with auto-captions
2. **Copy A/B testing:** Run landing page variations, measure conversion
3. **Asset analytics:** Auto-pull engagement metrics from Instagram/YouTube
4. **Template library:** Save and reuse winning asset templates
5. **Client delivery:** Auto-zip + email assets with brand guidelines

---

## Status & Next Actions

**Current:** ✅ Production-ready, tested, integrated with brand system

**Next:**
1. Document usage templates (Q1 campaign example)
2. Create asset delivery workflow (Drive + email)
3. Measure engagement on generated assets (post-campaign)
4. Plan video generation feature (Phase 2)
