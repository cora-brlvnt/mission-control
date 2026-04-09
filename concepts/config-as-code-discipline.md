# Config-as-Code Discipline

**Date:** April 9, 2026  
**Source:** ClawX config wipe incident (April 8)

---

## Principle

Configuration files for critical infrastructure must be treated as code: version-controlled, never edited through UI tools that perform full-file overwrites, and backed up before any modification.

## The Problem

GUI-based config editors (like ClawX settings UI) often save only the fields they manage, silently overwriting the entire file. This destroys hand-crafted sections the UI doesn't know about — channels, env vars, hooks, plugins, auth profiles.

## Rules

1. **Never edit config through UI** — Use file write, API patch, or CLI tools that perform safe merges
2. **Backup before every change** — Automatic `.bak` files + manual desktop backups
3. **Config changes are code changes** — Review what changed, verify after applying
4. **Single source of truth** — The config file on disk is authoritative; UI state is a read-only view
5. **Recovery plan required** — Know where backups live before you need them

## Application

- OpenClaw: `config.patch` API or `write` tool for safe merges
- Any system with JSON/YAML config: `git diff` before commit, never blind overwrite
- Backup locations documented in operational runbook

## Related Concepts

- Infrastructure reliability
- Local-first AI infrastructure
- Autonomous systems design
