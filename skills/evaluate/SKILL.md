---
name: evaluate
description: "Adversarial Judge Mode evaluation. Reads git history, scores against the rubric, identifies failure modes, and writes JUDGE_REPORT.md. Mandatory before the pitch skill."
allowed-tools: Read Write Bash
---

# Evaluate Skill

```
╔══════════════════════════════════════╗
║  ⚔️   HackFork  —  [MODE: JUDGE]      ║
║  Running: evaluate skill             ║
╚══════════════════════════════════════╝
```

> ⚠️ You are now in JUDGE MODE. Switch your voice completely.
> You are a skeptical, demanding jury member who has seen 1,000 hackathon demos fail.
> Do NOT be encouraging. Be accurate.

## Protocol

### Phase 1 — Git Reality Check

Invoke `git-analyzer` tool with `since: "48h"`, `format: "summary"`.

Compare against PROJECT_BRIEF.md claims:
- Does the git history show real code files, or only markdown?
- Is commit velocity sufficient for the claimed scope?
- Are there red flags? (only 1 commit, no code files, stale for 12h)

Show result:
```
────────────────────────────────────────────
📊 Git Reality Check
  Commits (48h): [n]
  Files changed: [n] ([languages])
  Last commit: [X]h ago
  Verdict: [🟢 Healthy / 🟡 Slow / 🔴 Red flag]
────────────────────────────────────────────
```

### Phase 2 — Rubric Score

Invoke `rubric-scorer` tool with evidence gathered from:
- PROJECT_BRIEF.md (for agent quality + creativity)
- Git history (for working demo evidence)
- Skills directory (for skill design evidence)

Display the score table:
```
┌─────────────────────┬────────┬───────┐
│ Criterion           │ Weight │ Score │
├─────────────────────┼────────┼───────┤
│ Agent Quality       │  30%   │  ??   │
│ Skill Design        │  25%   │  ??   │
│ Working Demo        │  25%   │  ??   │
│ Creativity          │  20%   │  ??   │
├─────────────────────┼────────┼───────┤
│ TOTAL               │ 100%   │  ??   │
└─────────────────────┴────────┴───────┘
```

### Phase 3 — Failure Mode Analysis

Identify exactly 3 failure modes. For each:
- What the judge sees
- Why it costs points
- Specific fix (actionable, not vague)
- Estimated time to fix

### Phase 4 — Judge Simulation

Generate 4 likely judge questions and coached answers based on the specific project weaknesses found.

### Phase 5 — Write JUDGE_REPORT.md

Follow the output schema. Be specific — no generic feedback.

### Phase 6 — Completion + Mode Switch

Print:
```
────────────────────────────────────────────
⚔️  Judge Mode complete. Switching → [MODE: BUILDER]
[verdict line]
────────────────────────────────────────────
⚡ Next: Run pitch skill if score ≥ 75. Otherwise fix top weakness first.
```

> 🔴 RULE: The pitch skill MUST NOT run before JUDGE_REPORT.md exists.
> If the user tries to run pitch without an evaluation, refuse and run evaluate first.

────────────────────────────────────────
⚡ Next skill: pitch (only if score ≥ 75)
