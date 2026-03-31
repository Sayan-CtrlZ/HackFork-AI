---
name: retrospect
description: "Post-hackathon learning extraction. Reads git history and JUDGE_REPORT.md to produce RETROSPECTIVE.md with crystallized rules for future hackathons."
allowed-tools: Read Write Bash
---

# Retrospect Skill

```
╔══════════════════════════════════════╗
║  🤝  HackFork  —  [MODE: BUILDER]    ║
║  Running: retrospect skill           ║
╚══════════════════════════════════════╝
```

> This skill runs after the hackathon ends.
> Its output is stored for the next run — making HackFork smarter over time.

## Protocol

### Phase 1 — Git Timeline Analysis

Invoke `git-analyzer` with `format: "timeline"`, `since: "first-commit"`.

Categorize commits into phases:
- Ideation commits (config, setup, planning files)
- Build commits (actual code)
- Polish commits (README, styling, cleanup)
- Pitch commits (PITCH.md, DEMO_SCRIPT.md)

Identify:
- Where did time actually go?
- Was the build/pitch ratio healthy? (target: 70% build, 30% pitch)
- Any 4h+ gaps? (team ran out of steam — note this)

### Phase 2 — Scope Delta

Compare PROJECT_BRIEF.md (if exists) "IN scope" list against what git history shows was actually built.

Calculate scope delta:
```
Planned features:  [n]
Shipped features:  [n]
Scope completion:  [%]
```

### Phase 3 — Weakness Prediction Accuracy (if JUDGE_REPORT.md exists)

If actual judge feedback is available (user pastes it), compare:
- JUDGE_REPORT.md predicted weaknesses
- Actual judge feedback

Accuracy score: did HackFork's adversarial evaluation find the real issues?

### Phase 4 — Crystallized Rules

Extract 3-5 rules in this format:
```
RULE #1: [short imperative statement]
Evidence: [what happened that proves this rule]
Apply when: [specific trigger condition]
```

These rules are written to `memory/MEMORY.md` under `crystallized_rules` for future sessions.

### Phase 5 — Write RETROSPECTIVE.md

Follow the output schema. End with the crystallized rules.

### Phase 6 — Update Memory

Append to memory/MEMORY.md:
```yaml
last_retrospect: [ISO timestamp]
hackathons_completed: [increment]
crystallized_rules: [array of rules]
```

────────────────────────────────────────
⚡ HackFork session complete. Memory updated. See you at the next hackathon.
