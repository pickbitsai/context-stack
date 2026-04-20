# Context Stack — Field Guide

Level 1 of 7. How I organize AI context across a dozen projects so it wakes up already knowing what I'm working on.

---

Most people use AI like a better Google — fire a question, get an answer, walk away. Useful, but flat.

A small number use it differently. Their AI wakes up already knowing what they're working on, what was decided last week, what's blocked. It drafts with their context. It catches things they forgot. They stop asking questions and start shipping with it.

This guide is the shortest path I've found — three files, a 60-second load, a 10-minute weekly reset. Not a methodology. Just what I do every Monday so AI feels like a co-builder instead of a chatbot.

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

## Get started — pick your surface

Same three-file pattern. Pick the path that matches how you already work.

### Claude Desktop + Cowork *(non-dev · canonical path)*
You don't need this repo for this path. You need **Claude Desktop** (paid plan) and a local folder for your project.

1. Open Claude Desktop → **Cowork** tab
2. New **Project** → **connect your local folder** (e.g. `~/Desktop/my-project/`)
3. Ask: *"Read this folder. Draft my identity, project, and state files into it."*
4. Cowork writes the three `.md` files directly into your folder — no uploads, no downloads.

Cowork Projects persist context across sessions. Update `state.md` weekly; the next session picks up automatically.

### Claude Code *(CLI · for developers)*
```bash
cd context-stack
# Open in Claude Code. Then in your session:
build my context stack
```

The `context-stack-builder` skill scans your folder, asks a few questions, and writes a starter stack into `./context-stack/`. Read the debrief — it tells you what got populated, what it guessed, and what to add next.

### VS Code with the Claude Code extension
Same skill, same prompt, inside your editor. Install the Claude Code extension, open the repo, say *"build my context stack."*

### No paid Claude plan?
Copy the [templates](./templates/) by hand — first pass is ~15 minutes. Load them into any Claude session at session start. Same pattern, slightly more manual.

### Safety (for the skill paths)
Reads only from CWD, writes only to `./context-stack/`, never touches secrets. [Full contract.](./.claude/skills/context-stack-builder/SKILL.md#0-safety-contract-non-negotiable)

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
