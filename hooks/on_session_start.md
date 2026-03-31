---
name: on_session_start
description: "Runs automatically when gitclaw starts. Loads memory, detects hackathon phase, and prints the HackFork welcome banner."
trigger: session_start
allowed-tools: Read Bash timer
---

# On Session Start

## Step 1 — Print the HackFork Banner

Output this exactly:

```
╔══════════════════════════════════════════╗
║   🍴  HackFork  v1.0.0                   ║
║   Adversarial Hackathon Co-Pilot         ║
║   git-native · dual-persona · rubric-AI  ║
╚══════════════════════════════════════════╝
```

## Step 2 — Load Memory

Read `memory/MEMORY.md`. If it exists, extract:
- `current_project` — name of the active hackathon project
- `hackathon_deadline` — stored deadline for the timer tool
- `last_skill` — last skill that was invoked
- `phase` — current hackathon phase

If memory is empty or missing, print:
```
💡 No active session found. Starting fresh.
   Tip: Tell me your hackathon idea to begin.
```

## Step 3 — Phase Detection

If `hackathon_deadline` exists in memory, invoke the `timer` tool with `action: status`.

Print the result:
```
────────────────────────────────────────────
⏱️  Time remaining: [X]h [Y]m
📍 Current phase: [PHASE]
[warning if applicable]
────────────────────────────────────────────
```

If no deadline is set, print:
```
⚠️  No deadline set. Type "set deadline to [time]" to enable phase tracking.
```

## Step 4 — Ready Prompt

Print:
```
Type your idea, a skill name, or /skills to see capabilities.
[MODE: BUILDER] ready.
```
