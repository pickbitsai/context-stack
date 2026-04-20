---
name: context-stack-builder
description: Bootstrap a PickBits Context Stack (identity + project + state) for the current project by inventorying the folder, reading attached artifacts (tickets, PR descriptions, meeting notes), asking a short set of targeted questions, and writing a starter stack into ./context-stack/. Use when the user says "build my context stack", "start the context stack", "init context stack", "set up Claude's memory for this project", "bootstrap a context stack", "/context-stack-builder", or any request to create AI working-memory files from scratch for a project folder.
---

# Context Stack Builder — Level 1

Bootstraps three of the five Context Stack layers (Identity, Projects, State) from whatever the user already has in the current folder. The full practice is documented in [GUIDE.md](../../../GUIDE.md) in this repo.

## 0. Safety Contract (non-negotiable)

This skill reads files and writes files. Before doing anything, state the following to the user in one line and abide by it:

- **Reads only from** the current working directory (CWD) and user-provided attachments. No parent-directory traversal.
- **Writes only to** `./context-stack/`. Creates the directory if missing. Never modifies or deletes files outside it.
- **Never reads** `.env`, `*.key`, `*.pem`, `credentials.*`, `*.secret`, anything matching common secret patterns, or anything in `.gitignore`. If a file appears to contain secrets, skip it and note the skip in the debrief.
- **Logs every file read or written** in the Step 5 debrief.

If the user's request would violate any of these rules, explain the conflict and stop.

## 1. What gets built

Three files, written into `./context-stack/`:

1. **`identity.md`** — who the user is, how they want to be answered, their working stack. Populated from: the user's answers to Step 2, `git config user.name` / `user.email`, any `about.md` or bio-style files found.
2. **`project-<slug>.md`** — one project brief. Populated from: `README.md`, `CLAUDE.md`, `package.json` (or equivalent), recent `git log`, attachments that describe the project.
3. **`state.md`** — this week's working memory. Populated from: `git log --since="7 days ago"`, the 3–5 most recently modified tracked files, pasted meeting notes / ticket dumps, user answers.

**Do not generate Layer 4 (Artifacts) or Layer 5 (Patterns).** Those are hand-authored over time. The skill's job is scaffolding, not the full stack.

## 2. The workflow

### Step 1 — Inventory (silent; no user output yet)

Scan the CWD in priority order. Store what you find; do not describe it to the user yet.

| Priority | Source | What it tells you |
|---|---|---|
| High | `README.md`, `CLAUDE.md`, `AGENTS.md` | Project name, purpose, stack, conventions |
| High | `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod` | Language, stack, scripts |
| High | `git config user.name` / `user.email`, `git log --since="7 days ago"` | User identity, recent activity |
| Medium | `CONTRIBUTING.md`, `docs/*.md`, `ARCHITECTURE.md` | Team conventions, architecture |
| Medium | User attachments (pasted text, screenshots, PDFs, .eml exports, Jira/Linear exports) | Tickets, meeting notes, PR descriptions — rich project/state signal |
| Low | Top-level file tree (file names only) | Stack hint when no manifest exists |

**Skip** anything matching secret patterns or `.gitignore` entries. Record each skip with a one-line reason.

### Step 2 — Ask clarifying questions

Ask **3–5** short questions. Never more than 5. Skip any question the inventory already answered.

Typical questions, in priority order:

1. **Role.** "What's your role on this project?" — `identity.md`.
2. **Tone preferences.** "How do you want me to answer you? (direct / detailed / short paragraphs / push back / etc.)" — `identity.md`.
3. **This week's priority.** "What's the one thing blocking or driving you this week?" — `state.md`. **Skip if the user attached meeting notes, a ticket export, or a sprint doc.**
4. **Last decision.** "What was the last significant decision you made on this project?" — `project.md` + `state.md`.
5. **Who else is involved.** "Are you solo on this, or who else is on the team?" — `project.md`.

Batch the questions in one message. Don't interrogate one-at-a-time.

### Step 3 — Draft the three files

Use the templates at `templates/{identity,project,state}.md.template` (relative to the repo root) as structural scaffolds. Fill placeholders from inventory + answers. Rules:

- **Specificity over completeness.** 4 specific lines in `state.md` beats 20 generic ones.
- **When signal is weak, mark it `[TBD: short reason]`** rather than inventing. Every `[TBD]` surfaces in the debrief.
- **Recent-first in `state.md`.** Today at the top, then yesterday, then the week.
- **Honest scope in `project-*.md`.** Status should describe what actually works, not the roadmap.
- **Project slug:** lowercase, hyphenated, derived from repo name or the user's stated project name. `project-feedrunner.md`, not `project-FeedRunner.md` or `project-my-app-v2-rewrite.md`.

### Step 4 — Write the files

Create `./context-stack/` if missing. Write all three files. 

**If any of the three files already exist in `./context-stack/`:**
- Do not overwrite silently.
- Show the user a diff (what you'd change).
- Ask before replacing. Default answer on ambiguity: keep the existing file and write your draft to `<name>.new.md` for the user to merge.

### Step 5 — Debrief

Return this exact shape:

```
## Context Stack built

**Created:**
- context-stack/identity.md          (N lines, from: [sources])
- context-stack/project-<slug>.md    (N lines, from: [sources])
- context-stack/state.md             (N lines, from: [sources])

**Files read:**
- [path 1]
- [path 2]
- ...

**Files skipped:** (secrets, .gitignored, irrelevant — one-line reason each)
- [path] — [reason]

**[TBD] markers left:** (what input would resolve each)
- identity.md:L7 — [TBD: your primary non-negotiable]
- project-<slug>.md:L12 — [TBD: confirm active branch]

**Next steps for you (Levels 4 + 5):**
- **Layer 4 (Artifacts):** link your repos, don't copy them. This folder is your first artifact.
- **Layer 5 (Patterns):** create `./context-stack/patterns/` and drop in prompt templates you re-use (code review rubric, PR description format). One file per pattern.
- **Daily load:** at session start, reference identity.md + the relevant project-*.md + state.md. Ask: "Load these. Tell me where I left off."
- **Monday reset:** ~10 minutes updating each project file + archiving last week's state.md.

**Field Guide:** GUIDE.md (in this repo)
**Repo + future episodes:** github.com/pickbitsai/context-stack
**Series updates:** @pickbitsai on Instagram · TikTok · YouTube · X
```

## 3. Principles

- **Safety first.** Every read, every write, logged. Nothing outside CWD. Nothing that looks like a secret.
- **Scaffold, don't solve.** Build a starting point. The user refines.
- **Specific beats complete.** A short state.md that says what's real beats a long one full of filler.
- **The debrief is the product.** What the skill tells the user about what it couldn't do is what makes this feel honest rather than magic.
- **Weekly reset is the user's job.** The skill initializes. Keeping `state.md` fresh is Layer 1 of the user's practice.

## 4. What this skill is NOT

- Not a replacement for the full Context Stack practice. It builds Layers 1–3 of a 5-layer system.
- Not a Jira/GitHub/Confluence integrator. Those are separate skills shipped in later episodes of the series.
- Not a generator that invents content when signal is missing. If the signal isn't there, it marks `[TBD]` and moves on.

## 5. Common misfires

- **"state.md filled with the roadmap, not this week's work."** → Thin inventory. Re-run with a pasted `git log --since="7 days ago"` output or a meeting-notes paste to ground the output.
- **"identity.md has my name wrong."** → Override in the questions, or fix `git config user.name` before running.
- **"I have 3 projects in this folder."** → Current version produces one `project-*.md`. Run per-project-folder, or ask for a multi-project variant.
- **"The skill wrote to my existing file without asking."** → Bug. Filing an issue at github.com/pickbitsai/context-stack is the right move.

---

Skill source and related episodes: **github.com/pickbitsai/context-stack**
Full Field Guide: **[GUIDE.md](../../../GUIDE.md)** (in this repo)
Series updates: **@pickbitsai** across Instagram · TikTok · YouTube · X
