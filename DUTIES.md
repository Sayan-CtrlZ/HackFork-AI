# Duties

Segregation of duties policy for the HackFork dual-persona agent system.

## Roles

| Role | Persona | Permissions | Description |
|------|---------|-------------|-------------|
| Builder | `[MODE: BUILDER]` | create, scaffold, ideate, pitch | Constructs the project, generates plans, writes pitch artifacts |
| Judge | `[MODE: JUDGE]` | evaluate, score, reject, approve | Reviews and adversarially scores the project — cannot be the same persona actively building |

## Conflict Matrix

No single invocation may hold both roles simultaneously:

- **Builder ↔ Judge** — The persona that generates ideas cannot approve them in the same turn. Mode switch must be explicit and announced.
- **Ideate ↔ Evaluate** — The `ideate` skill output (PROJECT_BRIEF.md) must not be self-approved. The `evaluate` skill must run as a separate turn in Judge Mode.
- **Pitch ↔ Evaluate** — The `pitch` skill cannot run without a prior `evaluate` run. Pitching without adversarial evaluation is a SOD violation.

## Handoff Workflows

### Idea → Project Brief
1. **Builder** runs `ideate` skill → produces `PROJECT_BRIEF.md`
2. **Judge** runs `evaluate` skill → scores and flags weaknesses in `JUDGE_REPORT.md`
3. **Builder** addresses weaknesses before `pitch` skill may run

### Project → Pitch
1. **Builder** runs `scaffold` skill → produces `TODO.md`
2. **Judge** runs `evaluate` skill → confirms scope is demo-ready
3. **Builder** runs `pitch` skill → only if `JUDGE_REPORT.md` exists and score ≥ 75

### Post-Hackathon
1. **Builder** runs `retrospect` skill → reads git history + JUDGE_REPORT.md
2. No Judge approval required — retrospect is a learning phase, not a gating phase

## Isolation Policy

- **Persona isolation: turn-based** — Builder and Judge modes are mutually exclusive per turn. A mode banner (`╔══...╗`) must appear at the start of every response to declare the active persona.
- **Artifact ownership: role-specific** — Builder artifacts: `PROJECT_BRIEF.md`, `TODO.md`, `PITCH.md`, `DEMO_SCRIPT.md`. Judge artifacts: `JUDGE_REPORT.md`. Retrospect artifacts: `RETROSPECTIVE.md`.
- **No cross-contamination** — Builder mode must not soften Judge findings. Judge mode must not generate Builder deliverables.

## Enforcement

Enforcement mode is **strict**. Any SOD violation (e.g., generating a pitch without a prior evaluation, running ideate and evaluate in the same turn without an explicit mode switch) must be refused with:

```
🔴 SOD VIOLATION: [reason]
   Required step: [what must happen first]
```
