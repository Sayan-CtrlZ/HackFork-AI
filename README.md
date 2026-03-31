# 🍴 HackFork

> An adversarial hackathon co-pilot. It helps you build, then brutally judges what you built.

HackFork runs as a **git-native AI agent** using the [gitagent](https://github.com/open-gitagent/gitagent) spec. It has two modes:

- **`[MODE: BUILDER]`** — Ideates, scaffolds, and pitches your project
- **`[MODE: JUDGE]`** — Red-teams it against the judging rubric before you present

---

## Quickstart

### 1. Clone the repo

```bash
git clone https://github.com/Sayan-CtrlZ/HackFork-AI.git
cd HackFork-AI
```

### 2. Install the runtime

```bash
npm install -g gitclaw
```

### 3. Set your API key

Pick one provider and export the key in your terminal:

```bash
# Google (recommended — free tier available)
export GOOGLE_API_KEY="your-key-here"

# OR Anthropic
export ANTHROPIC_API_KEY="sk-ant-..."

# OR OpenAI
export OPENAI_API_KEY="sk-..."
```

> Get a free Google API key at [aistudio.google.com](https://aistudio.google.com)

### 4. Run HackFork

```bash
gitclaw --dir . --model google:gemini-2.0-flash
```

### 5. Start talking

Once the agent starts, type any of these:

| What you type | What happens |
|---|---|
| `I have an idea for...` | Runs `ideate` → writes `PROJECT_BRIEF.md` |
| `scaffold` | Runs `scaffold` → writes `TODO.md` |
| `evaluate` | Switches to Judge Mode → writes `JUDGE_REPORT.md` |
| `pitch` | Runs `pitch` → writes `PITCH.md` + `DEMO_SCRIPT.md` |
| `retrospect` | Runs `retrospect` → writes `RETROSPECTIVE.md` |

---

## Pipeline

```
Your idea
    │
    ▼
[ideate] ──→ PROJECT_BRIEF.md
    │
    ▼
[scaffold] ──→ TODO.md
    │
    ▼
[evaluate] ──→ JUDGE_REPORT.md   ← adversarial Judge Mode
    │
    ▼
[pitch] ──→ PITCH.md + DEMO_SCRIPT.md
    │
    ▼
[retrospect] ──→ RETROSPECTIVE.md
```

> ⚠️ **SOD enforced:** You cannot run `pitch` without a prior `evaluate`. The agent will refuse and redirect you.

---

## Deploy to Lyzr Studio (optional)

If you want a browser-based UI instead of the CLI:

```bash
export LYZR_API_KEY="your-lyzr-key"
gitagent lyzr create -d .
gitagent lyzr run -d . -p "I want to build a hackathon project"
```

Get your Lyzr key at [studio.lyzr.ai](https://studio.lyzr.ai)

---

## Structure

```
hackfork/
├── agent.yaml                      # Manifest
├── SOUL.md                         # Agent identity + CLI format spec
├── RULES.md                        # Behavioral constraints
├── DUTIES.md                       # Segregation of duties (Builder ↔ Judge)
├── PROMPT.md                       # Default task router
├── skills/
│   ├── ideate/SKILL.md
│   ├── scaffold/SKILL.md
│   ├── evaluate/SKILL.md           # ← Judge Mode — must run before pitch
│   ├── pitch/SKILL.md
│   └── retrospect/SKILL.md
├── tools/
│   ├── rubric-scorer.yaml          # Scores against judging rubric
│   ├── git-analyzer.yaml           # Reads actual git history
│   └── timer.yaml                  # Hackathon phase tracker
├── hooks/
│   ├── on_session_start.md         # Banner + memory load
│   └── on_skill_complete.md        # Auto-logs after every skill
├── knowledge/
│   └── rubric.md                   # Grounded hackathon strategy
└── memory/
    └── MEMORY.md                   # Persistent session state
```

---

## Requirements

- Node.js 18+
- `npm install -g gitclaw`
- One of: `GOOGLE_API_KEY`, `ANTHROPIC_API_KEY`, or `OPENAI_API_KEY`
