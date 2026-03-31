---
name: scaffold
description: "Generates a demo-impact ordered TODO.md and project directory structure from PROJECT_BRIEF.md. Every task is ordered by what appears in the demo, not by technical priority."
allowed-tools: Read Write Bash
---

# Scaffold Skill

```
╔══════════════════════════════════════╗
║  🤝  HackFork  — [MODE: BUILDER]     ║
║  Running: scaffold skill             ║
╚══════════════════════════════════════╝
```

## Protocol

You are in **Builder Mode**. You read PROJECT_BRIEF.md and produce a BUILD PLAN ordered by demo impact — never by technical architecture.

### Phase 1 — Read & Parse PROJECT_BRIEF.md

Extract:
- Demo Moment (the single most important thing to build first)
- In-scope features
- Out-of-scope items (go directly to "Explicitly Deferred")
- Target stack implied by the idea

### Phase 2 — Invoke Timer

Call `timer` tool with `action: status`. If < 8h remaining, add a warning:
```
⚠️  Less than 8h remaining — Phase 3 tasks are auto-deferred.
```

### Phase 3 — Order by Demo Impact

Apply this filter to every task before placing it:

> "If I remove this task from the demo, does the judge still see something impressive?"
> - YES → Phase 2 or 3
> - NO  → Phase 1 (must have)

### Phase 4 — Write TODO.md

Format each task as:
```markdown
- [ ] [Task description] — Est: [time] [🔴/🟡/🟢]
```

Include a project directory structure suggestion as a code block.

Mark tasks that use the `rubric-scorer` or `git-analyzer` tools — they demonstrate advanced agent usage to judges.

### Phase 5 — Completion

Log to memory/MEMORY.md. Suggest:
```
⚡ Next: Start building Phase 1 tasks. Run evaluate when Phase 1 is complete.
```

────────────────────────────────────────
⚡ Next skill: evaluate (after Phase 1 complete)
