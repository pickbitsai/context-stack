# The Context Stack — Field Guide

**Level 1 of 7. Turn your project knowledge into AI working memory — so you stop re-explaining yourself every Monday.**

---

**Who this is for:** Knowledge workers, founders, engineers, and ops people who use AI (Claude, ChatGPT, Gemini, Cursor) and keep hitting the same wall — you spend ten minutes loading context before every session, forget what you decided last week, and lose threads across tools.

**What it is:** A five-layer system for structuring project knowledge so AI can load it in under 60 seconds — without you copy-pasting anything.

---

## The problem

You open Claude. You paste the project brief again. You explain where you left off again. You describe the stakeholders again. Fifteen minutes in, you're finally ready to work. By next Monday, the context is gone. You start over.

Your AI has no memory of you. It's been reset since yesterday. And the way most people deal with this — longer prompts, bigger system messages, more tabs — is a treadmill.

**The Context Stack fixes it with structure.**

---

## The 5 Layers

### Layer 1 — Identity *(static)*
Who you are, your role, your non-negotiables, your preferences. Things that don't change week to week.

> *"I'm a product lead at a 20-person SaaS. I prefer direct answers. I use React and Postgres. I don't write bullet lists. I care about shipped work, not demos."*

**Where it lives:** A single markdown file (`identity.md`) or your AI's persistent memory.

---

### Layer 2 — Projects *(semi-static)*
One brief per active project. Goals, stakeholders, tech stack, deadlines, decisions made.

**Where it lives:** One folder. One file per project (`project-feedrunner.md`, `project-pantryplan.md`). Updated weekly, not daily.

---

### Layer 3 — State *(dynamic — updated daily)*
What you touched today. What's blocked. What's next. One file, refreshed each morning.

> *"Today: shipped pipeline v3 migration. Blocked on a Supabase RLS bug. Tomorrow: retry logic for publish."*

**Where it lives:** `state.md` — your working memory.

---

### Layer 4 — Artifacts *(referenced, not copied)*
Code, docs, past decisions. You don't paste them — you **link** or let the AI read them. That's what Claude file access, Cursor, and MCP servers are for.

**Rule:** Reference, don't replicate. The moment you copy-paste, the artifact is stale.

---

### Layer 5 — Patterns *(reusable)*
Prompt templates, rules, and instructions that worked. Saved, not re-invented.

> *Code review rubric. Weekly status update format. Client email draft style.*

**Where it lives:** A `patterns/` folder with named files.

---

## The daily load — under 60 seconds

1. Open your AI tool.
2. Reference `identity.md` + the relevant `project-*.md` + `state.md`.
3. Ask: *"Load these, then tell me where I left off."*

That's it. No re-explaining.

## The Monday reset — 10 minutes, once a week

1. Update each project file with last week's decisions.
2. Archive last week's `state.md`. Start a fresh one.
3. Prune `patterns/` — delete what you haven't used in 30 days.

Ten minutes of hygiene replaces the 15 minutes/day you were losing to re-context.

## The math

| | Before | After |
|---|---|---|
| Time per session loading context | 15 min | 60 sec |
| Sessions per week | 5 | 5 |
| Weekly hygiene | 0 | 10 min |
| **Weekly context cost** | **75 min** | **15 min** |
| **Recovered** | — | **~1 hour/week** |

Across a team of 10, that's **10 hours of focused work recovered every week.**

---

## Level 1 of 7

This is the manual version — the starting point. The series builds out from here, one layer of automation at a time:

| | |
|---|---|
| **Level 1 — Manual** | Hand-authored markdown. You own every word. *(You are here.)* |
| **Level 2 — Autopilot** | Claude Code Routines refresh the state file while you sleep. |
| **Level 3 — Atlassian** | Jira + Confluence replace `project-*.md` and `state.md`. |
| **Level 4 — GitHub** | Repos, PRs, and commits become the Artifacts layer. |
| **Level 5 — Docs** | Drive / SharePoint / Lucid as team memory. |
| **Level 6 — Slack / Teams** | Decisions-made-in-chat surface automatically. |
| **Level 7 — Full Stack** | All of the above, composed, governed. |

---

## Get started in 60 seconds

You already have the repo. The fastest path to your first Context Stack:

```bash
cd context-stack
# Open in Claude Code. Then in your session:
build my context stack
```

The `context-stack-builder` skill scans your folder, asks a few questions, and writes a starter stack into `./context-stack/`. Read the debrief — it tells you what got populated, what it guessed, and what to add next.

Don't have a project folder to try it on yet? Point it at an existing repo you're working in. It's designed to be safe: reads only from CWD, writes only to `./context-stack/`, never touches secrets. [Full safety contract here.](./.claude/skills/context-stack-builder/SKILL.md#0-safety-contract-non-negotiable)

---

## Printable versions

- **Dark theme (screen / digital):** [`docs/field-guide-dark.html`](./docs/field-guide-dark.html)
- **Light theme (paper / office print):** [`docs/field-guide-print.html`](./docs/field-guide-print.html)

Open in any browser, `Ctrl+P` → **Save as PDF**. Turn on "Background graphics" if you want the styling on the dark variant.

---

## Go deeper

- **1:1 AI Coaching** — [pickbits.ai/coaching](https://pickbits.ai/coaching) — I build your stack live against your actual projects.
- **Enterprise Team Training** — [pickbits.ai/consulting](https://pickbits.ai/consulting) — your team's Jira + GitHub + docs, wired in two weeks.
- **Follow the series** — [@pickbitsai](https://x.com/pickbitsai) across Instagram · TikTok · YouTube · X. New level each week.

— Mark Pickering, Founder, PickBits.AI
