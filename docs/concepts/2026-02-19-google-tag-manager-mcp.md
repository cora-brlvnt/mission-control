# Google Tag Manager MCP Integration — Stape Provider

## Overview
Programmatic Google Tag Manager automation via Stape MCP server. Enables container management, tag deployment, conversion tracking audits, and version control without manual GTM UI work.

## Technical Specs

### Endpoint
**URL:** https://rpro-gtm-mcp-server.performance-ee6.workers.dev  
**Provider:** Stape (Google Tag Manager API wrapper)  
**Protocol:** MCP (Model Context Protocol) — JSON-RPC 2.0  
**Cost:** $0/month (Cloudflare Workers free tier)

### Authentication
**Method:** Browser OAuth 2.0 (one-time setup)  
**Flow:**
1. First call triggers browser → Google login → approval
2. Token stored locally: `~/.mcp-auth/`
3. Subsequent calls use cached token (no per-request auth)

**First-time setup:** 30 seconds (browser → click → done)

### Expected Tools (17+)

**Container Management:**
- List containers across GTM account
- Get container details (ID, name, version, description)
- Create new container
- Update container settings

**Tag Management:**
- Create tags (GA4, Facebook Pixel, custom)
- Update tag configuration
- Delete tags
- Validate tag syntax
- View tag firing status

**Trigger Management:**
- Create triggers (page view, click, custom)
- Update trigger conditions
- Delete triggers
- Conditional logic chains

**Variable Management:**
- Custom variables (lookups, constants, regex)
- Data layer variables
- URL variables
- Environment variables

**Version Control:**
- Create draft version
- Publish version
- Deploy to production
- Rollback to previous version
- View version history

**Tracking Audits:**
- Verify GA4 firing status
- Check conversion tracking active
- Audit Facebook Pixel presence
- Report missing tracking

---

## Use Cases

### 1. Auto-Deploy GA4 to Client Containers
```
Task: "Deploy GA4 tag to client GTM container B3d2uKVUfJlaSf6crRW5"
→ Create tag (Measurement ID: G-XXXXX)
→ Create trigger (All Pages)
→ Publish version
→ Verify firing
```

### 2. Setup Conversion Tracking Programmatically
```
Task: "Setup purchase conversion tracking for Forex.com"
→ Create event variable (datalayer.purchaseValue)
→ Create trigger (custom event: 'purchase')
→ Create GA4 event tag
→ Publish & test
```

### 3. Audit Tracking Setup (Daily)
```
Task: "Audit conversion tracking across all client containers"
→ List all containers
→ Check GA4 tag firing
→ Verify conversion event triggers
→ Report status (working / broken / misconfigured)
```

### 4. Multi-Container Management
```
Task: "Update GA4 configuration across 5 client containers"
→ Get all containers
→ Update GA4 tags (new Measurement ID)
→ Publish versions
→ Notify clients
```

### 5. Onboarding Platform Integration
```
Task: "Show client their tracking status on dashboard"
→ Check GTM container status
→ Audit GA4 firing
→ Display: ✅ Tracking active / 🚨 Configuration issue
```

---

## Integration with Measurement Stack

**Three-layer reporting:**
1. **GSC** (Google Search Console) — Keywords, impressions, rankings
2. **GA4** (Google Analytics 4) — Traffic, conversions, landing pages
3. **GTM** (Google Tag Manager) — Tags, triggers, conversion audit

**Combined workflow:**
- GTM deploys tags → GA4 fires → Data captured
- Daily audit: "Is GA4 firing? Is conversion tracking working?"
- Optimization: GSC identifies keywords → GA4 shows conversions → GTM ensures tracking

**Cost:** $0 (all Cloudflare Workers)

---

## Status

✅ **Implementation complete** (Feb 19)  
🔐 **OAuth setup pending** (one-time, 30 seconds)  
📅 **Ready for production** (Feb 24+)

---

## Next Steps

### Immediate (Feb 24)
1. Trigger GTM OAuth setup (browser → login → approve)
2. Verify API access (list containers)
3. Test one deployment (GA4 tag to test container)

### Week 2 (Mar 3-9)
1. Schedule daily tracking audits (9 AM EST)
2. Build automation: "Deploy GA4 to new client" workflow
3. Create dashboard: "Tracking Status" (all clients, all containers)

### Production (Mar 10+)
1. Offer as managed service ("We audit your tracking daily")
2. Integrate with Berelvant onboarding (show tracking status)
3. Scale to multi-container management (5+ client containers)

---

## Documentation
Full integration notes: `/Users/cora/.openclaw/workspace/MCP_GTM_INTEGRATION.md`
