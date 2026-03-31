# HackFork Knowledge Base

Structured knowledge that HackFork uses across all skills. Read this file to ground responses in real hackathon strategy.

---

## Judging Rubric (Source of Truth)

| Criterion | Weight | What judges actually look at |
|---|---|---|
| Agent Quality | 30% | Is the identity distinct? Are rules enforced? Does it do something a plain prompt can't? |
| Skill Design | 25% | Are skills focused? Do they compose into a pipeline? Are there input/output contracts? |
| Working Demo | 25% | Does it run in < 60s from cold? Is there a clear wow moment? What's the fallback? |
| Creativity | 20% | Is this genuinely new? Would you remember it in a week? Is there a memorable angle? |

---

## Phase Timing Strategy (24h Hackathon)

| Phase | Time Window | % Elapsed | Key Output |
|---|---|---|---|
| Ideate | 0h – 3h | 0–12% | PROJECT_BRIEF.md locked |
| Build | 3h – 15h | 12–62% | Core demo path working |
| Polish | 15h – 19h | 62–79% | Demo friction eliminated |
| Pitch | 19h – 23h | 79–96% | PITCH.md + DEMO_SCRIPT.md |
| Lock | 23h – 24h | 96–100% | No new code — rehearse only |

**Golden ratio:** 60% build / 40% pitch prep. Most teams fail because they build until 23h.

---

## The 5 Hackathon Failure Modes

1. **Demo friction > 30s** — Judge loses interest before the wow moment. Fix: zero-dependency demo path.
2. **Feature-first storytelling** — "It can do X and Y and Z" — no narrative. Fix: one sentence, one problem, one demo moment.
3. **Generic identity** — "An AI assistant for [domain]." Fix: named persona, specific constraint, unique behavioral rule.
4. **Scope creep** — Built 8 features instead of 1 great one. Fix: ruthless cut with every evaluate run.
5. **Unprepared Q&A** — Fumbles the "why not ChatGPT?" question. Fix: coached answers in PITCH.md pre-empting JUDGE_REPORT weaknesses.

---

## What Judges Remember (30s After Your Demo)

Judges evaluate 20-40 projects in a day. They remember:
- The **one sentence** that explained what you built
- The **one moment** where it worked unexpectedly well
- Whether you **answered confidently** when challenged

They forget:
- Your tech stack
- How many features you have
- Your slide design

---

## Model Selection Guide

| Provider | Best For | Key Env Var |
|---|---|---|
| `google:gemini-2.0-flash` | Fast demos, free tier, low latency | `GOOGLE_API_KEY` |
| `google:gemini-2.5-pro` | Complex reasoning, best quality | `GOOGLE_API_KEY` |
| `anthropic:claude-sonnet-4-5` | Nuanced writing, pitch copy | `ANTHROPIC_API_KEY` |
| `openai:gpt-4o` | Tool use, structured output | `OPENAI_API_KEY` |

---

## Skill Invocation Reference

| User says... | HackFork invokes... | Output file |
|---|---|---|
| "I have an idea" / "Ideate" | `ideate` | `PROJECT_BRIEF.md` |
| "Build plan" / "Scaffold" | `scaffold` | `TODO.md` |
| "Evaluate" / "Judge Mode" | `evaluate` | `JUDGE_REPORT.md` |
| "Pitch" / "Demo script" | `pitch` (requires JUDGE_REPORT.md) | `PITCH.md` + `DEMO_SCRIPT.md` |
| "Retrospect" / "Post-mortem" | `retrospect` | `RETROSPECTIVE.md` |
