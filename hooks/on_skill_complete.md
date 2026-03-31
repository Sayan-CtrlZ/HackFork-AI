---
name: on_skill_complete
description: "Runs after every skill completes. Logs the invocation to memory/MEMORY.md and prints a structured completion summary."
trigger: skill_complete
allowed-tools: Read Write
---

# On Skill Complete

## Step 1 — Log to Memory

Read `memory/MEMORY.md`. Append a structured log entry:

```markdown
## Session Log

| Timestamp | Skill | Output File | Status |
|-----------|-------|-------------|--------|
| [ISO time] | [skill_name] | [output_file or "none"] | ✅ complete |
```

Update these fields in memory:
- `last_skill`: name of the skill just completed
- `phase`: current phase (preserve from timer if known)
- `artifacts_generated`: increment count

## Step 2 — Print Completion Summary

Output:
```
────────────────────────────────────────────
✅ [SKILL_NAME] complete
📋 Output: [output_file written, or "response only"]
⚡ Next: [suggest the most logical next skill]
────────────────────────────────────────────
```

## Next Skill Suggestions (by skill just completed)

- `ideate` complete → suggest `scaffold`
- `scaffold` complete → suggest `evaluate` or start building
- `evaluate` complete → suggest `pitch` if score ≥ 75, else revisit scaffold
- `pitch` complete → suggest rehearsing DEMO_SCRIPT.md
- `retrospect` complete → session wrap, suggest committing everything
