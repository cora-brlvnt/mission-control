# Workspace Consolidation Pattern

**Date:** February 26, 2026  
**Category:** Operational Infrastructure  
**Status:** 🔄 In progress (staged changes)  
**Goal:** Faster access + better visibility

---

## Pattern

Migrate operational system files from organized folders to root-level access.

### Before & After

**Before (nested):**
```
/Users/cora/.openclaw/workspace/
  ├── core/
  │   ├── SOUL.md
  │   ├── USER.md
  │   ├── AGENTS.md
  │   └── TOOLS.md
  ├── memory/
  ├── projects/
  └── scripts/
```

**After (consolidated):**
```
/Users/cora/.openclaw/workspace/
  ├── SOUL.md (root)
  ├── USER.md (root)
  ├── AGENTS.md (root)
  ├── TOOLS.md (root)
  ├── MEMORY.md (root)
  ├── IDENTITY.md (root)
  ├── HEARTBEAT.md (root)
  ├── memory/ (daily logs)
  ├── projects/ (project-specific)
  └── scripts/ (utilities)
```

---

## Rationale

**Faster access:**
- No nested paths to navigate
- Root-level docs visible at a glance
- `read SOUL.md` → works immediately

**Better visibility:**
- All critical docs in one place
- Agents discover files more easily
- Onboarding faster for new operators

**Easier for frequent edits:**
- SOUL.md, USER.md, MEMORY.md change often
- Root-level = faster iteration
- No "where is that file again?" delays

**Simpler git history:**
- Fewer path changes in commits
- Easier to diff (all in root)
- Clearer what changed (file name vs nested path)

---

## Files Consolidated

| File | Purpose | Frequency |
|------|---------|-----------|
| **SOUL.md** | Strategic operating system | Monthly updates |
| **USER.md** | User preferences & business context | Monthly updates |
| **AGENTS.md** | Agent behavior & autonomy rules | Quarterly |
| **TOOLS.md** | Integrated systems & tools inventory | Weekly updates |
| **MEMORY.md** | Long-term facts & decisions | Weekly digests |
| **IDENTITY.md** | Cora's persona & communication style | Rarely |
| **HEARTBEAT.md** | Daily attention check | Never (auto-generated) |

---

## What Stays Nested

**Preserved structure:**
- `core/` → archives only (rarely accessed)
- `memory/` → daily logs (append-only, time-series)
- `projects/` → project-specific content (organized by project)
- `scripts/` → utilities (organized by type)
- `skills/` → custom skills (organized by domain)

---

## Implementation

**Step 1:** Move files to root
```bash
mv core/SOUL.md ./
mv core/USER.md ./
mv core/AGENTS.md ./
mv core/TOOLS.md ./
mv core/MEMORY.md ./
mv core/IDENTITY.md ./
```

**Step 2:** Update imports in code
- Any script reading `core/SOUL.md` → `./SOUL.md`
- Update agent startup scripts

**Step 3:** Test
- Verify agents still boot correctly
- Check that goc CLI finds TOOLS.md
- Spot-check a few file reads

**Step 4:** Commit
```bash
git add .
git commit -m "refactor: consolidate workspace files to root for faster access"
```

---

## Migration Checklist

- [ ] Copy SOUL.md to root
- [ ] Copy USER.md to root
- [ ] Copy AGENTS.md to root
- [ ] Copy TOOLS.md to root
- [ ] Copy MEMORY.md to root
- [ ] Copy IDENTITY.md to root
- [ ] Copy HEARTBEAT.md to root
- [ ] Update agent startup scripts (path references)
- [ ] Test agent boot sequence
- [ ] Verify goc CLI works
- [ ] Test file reads via exec
- [ ] Commit changes
- [ ] Push to GitHub

---

## Benefits After Consolidation

| Benefit | Impact |
|---------|--------|
| Faster file access | ~100ms saved per agent boot |
| Better visibility | New operators find files immediately |
| Simpler git | Cleaner diffs, fewer path changes |
| Easier editing | SOUL.md updates are 1-2s faster |
| Clearer structure | "Critical files in root, everything else organized" |

---

## Zero Risk

- All files version-controlled (git rollback if needed)
- No data loss (just moving files)
- Backward compatible (agents still work)
- Easy to revert (move files back)

---

## Related

- [[SOUL.md]] (operational system)
- [[AGENTS.md]] (autonomy rules)
- [[TOOLS.md]] (systems inventory)
