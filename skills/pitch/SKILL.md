---
name: pitch
description: "Generates PITCH.md and DEMO_SCRIPT.md. Reads JUDGE_REPORT.md to pre-empt identified weaknesses in coached Q&A. Requires JUDGE_REPORT.md — run evaluate first."
allowed-tools: Read Write Bash
---

# Pitch Skill

```
╔══════════════════════════════════════╗
║  🤝  HackFork  —  [MODE: BUILDER]    ║
║  Running: pitch skill                ║
╚══════════════════════════════════════╝
```

## Protocol

### Phase 0 — Gate Check

Read `JUDGE_REPORT.md`. If it does not exist:
```
🔴 BLOCKED: JUDGE_REPORT.md not found.
   Run the evaluate skill first.
   A pitch without an evaluation is a pitch that fails.
```
Stop and do not proceed.

### Phase 1 — Extract Weaknesses from JUDGE_REPORT.md

Read the Top 3 Failure Modes. Every coached answer in PITCH.md must directly pre-empt at least one of these weaknesses.

Map failure modes to expected judge questions:
- Demo friction → "Can you show me a live demo?"
- Thin skill design → "What makes this an agent vs a chatbot?"  
- Low creativity → "This has been built before, what's different?"

### Phase 2 — Check Timer

Invoke `timer` tool. If < 2h remaining, add:
```
⏱️  WARNING: Less than 2h remaining.
   Write the DEMO_SCRIPT first — it's more important than PITCH.md.
```

### Phase 3 — Write PITCH.md

The hook must be specific to this project. Generic hooks like "Have you ever struggled with X?" are banned.

The coached Q&A answers must:
- Reference specific features/files in the repo
- Not say "we plan to" — only "we built" or "it does"
- Be ≤ 3 sentences each

### Phase 4 — Write DEMO_SCRIPT.md

Include word-for-word stage directions in *italics*. Timestamps are mandatory.

The Fallback Protocol section must list 3 pre-generated files to show if the live demo fails.

### Phase 5 — Completion

```
────────────────────────────────────────────
✅ pitch complete
📋 PITCH.md written
📋 DEMO_SCRIPT.md written
────────────────────────────────────────────
⚡ Next: Rehearse DEMO_SCRIPT.md 3 times before presenting.
```

────────────────────────────────────────
⚡ Next skill: retrospect (post-hackathon)
