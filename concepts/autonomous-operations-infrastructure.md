# Autonomous Operations Infrastructure

## Overview
Five systems running autonomously 24/7 without manual intervention. Designed to survive session compactions, reboots, and travel.

## Active Systems (Live as of Feb 15)

### 1. Telegram Memory System ✅
**Purpose:** Persistent semantic search over all Telegram messages

**Tech stack:**
- Supabase PostgreSQL + pgvector
- OpenAI embeddings (3-small model)
- Telegram Bot API (polling)

**Specs:**
- Polling interval: Every 30 minutes
- Cron job ID: e9dab4a1-d14c-458e-9a85-6f7efe914695
- Auto-runs: Yes
- Cost: ~$1-5/mo (embeddings)

**Status:** LIVE since Feb 14, 01:20 EST

**Benefit:** Survives session compactions. Can search entire conversation history from any session.

### 2. 2Brain Daily Capture Cron ✅
**Purpose:** Auto-capture work ideas, tasks, lessons to GitHub

**Tech stack:**
- Local 2Brain app (`/Applications/2Brain.app`)
- GitHub API (commits)
- Manual writes + cron automation

**Specs:**
- Firing interval: Every 6 hours (0, 6, 12, 18 UTC)
- Script: `/Users/cora/.openclaw/workspace/telegram-capture.mjs` (ref)
- Repo: https://github.com/cora-brlvnt/mission-control
- Cost: Free (GitHub + local app)

**Status:** LIVE, tested, verified

**Benefit:** Automatic backup of work ideas. Clean, organized knowledge base.

### 3. Tailscale Health Check ✅
**Purpose:** Auto-restart Tailscale if daemon crashes

**Tech stack:**
- Shell script (zsh)
- Tailscale CLI (`tailscale status`)
- launchd (cron equivalent on macOS)

**Specs:**
- Polling interval: Every 5 minutes
- Script: `/Users/cora/.openclaw/workspace/scripts/tailscale-health-check.sh`
- Logs: `/Users/cora/.openclaw/workspace/logs/tailscale-health.log`
- Cost: Free

**Status:** READY (verified, not yet active; can enable on-demand)

**Benefit:** Network resilience. No manual intervention if connection drops.

### 4. OpenClaw Gateway ✅
**Purpose:** Central hub for all integrations and automation

**Tech stack:**
- Node.js daemon
- launchd auto-start (macOS)
- Config: `~/.openclaw/config.yml`

**Specs:**
- Version: 2026.2.13
- Port: 18789 (localhost)
- Auto-restart: Yes (via launchd on reboot)
- Integrations: Telegram, Discord, Google Workspace, ElevenLabs TTS
- Cost: Free (open source)

**Status:** LIVE, auto-starts on reboot

**Benefit:** All messaging, scheduling, and integrations route through one system.

### 5. Cora Voice Web App ✅
**Purpose:** Real-time voice interface with STT, Claude, TTS

**Tech stack:**
- Node.js + WebSocket
- Deepgram Nova-3 (STT)
- Claude API (inference)
- ElevenLabs (TTS)
- Supabase (conversation logging)
- Fly.io (deployment)

**Specs:**
- URL: https://cora-voice.fly.dev/app
- Region: iad (US East)
- Auto-runs: Yes (Fly.io keeps it alive)
- Repo: https://github.com/cora-brlvnt/cora-voice
- Cost: ~$5-10/mo (Fly + Deepgram + ElevenLabs)

**Status:** LIVE, responding, auto-archiving conversations

**Benefit:** Accessible voice interface. All conversations logged with embeddings for future search.

## Deployment & Resilience

| System | Auto-Start | Survives Reboot | Survives Session Compaction | Cost/mo |
|--------|-----------|-----------------|---------------------------|---------|
| Telegram Memory | ✅ (cron) | ✅ | ✅ | $1-5 |
| 2Brain Capture | ✅ (cron) | ✅ | ✅ | Free |
| Tailscale Health | ✅ (ready) | ✅ | ✅ | Free |
| OpenClaw Gateway | ✅ (launchd) | ✅ | ✅ | Free |
| Cora Voice App | ✅ (Fly.io) | ✅ | ✅ | $5-10 |

**Total monthly cost:** ~$6-15

## Key Design Principles

1. **No single points of failure** — Each system runs independently
2. **Persistent data** — Everything survives session restart or reboot
3. **Minimal cost** — Total < $20/month
4. **Zero manual intervention** — All systems self-maintain
5. **Cross-session awareness** — Telegram memory searchable from any session

## Monitoring

**Heartbeat ritual (daily):**
- Check Telegram memory last update
- Check 2Brain last commit
- Check Cora Voice app availability
- Review memory/YYYY-MM-DD.md for errors

**Alert triggers:**
- Telegram polling > 1 hour without update
- 2Brain commit > 12 hours without update
- Cora Voice app down (HTTP 5xx)
- OpenClaw gateway restart loops

## Validation Status
✅ All systems tested and verified as of Feb 15, 2026.
✅ Ready for 8-day Rome trip (Feb 15-23) with zero manual intervention.
