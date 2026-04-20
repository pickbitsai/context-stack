# The Context Stack

**Stop re-explaining yourself to AI every Monday.**

Turn your project knowledge into AI working memory — in under 60 seconds a day — using the PickBits Context Stack model.

This repo ships the skills, templates, and connector configs that make the practice real. Start manual (Level 1), graduate to autopilot (Level 2), wire your systems of record (Levels 3–6).

---

## Quickstart

```bash
gh repo clone pickbitsai/context-stack
cd context-stack
```

Open the folder in Claude Code (or any editor with the Claude Code extension). In your session, say:

```
build my context stack
```

The `context-stack-builder` skill will scan your current project, ask a handful of questions, and write a starter Context Stack into `./context-stack/`. Read the debrief — it tells you what was populated, what it guessed, and what to add next.

---

## What is the Context Stack?

Five layers of project knowledge that make AI useful on day 1 and every day after:

| Layer | What it is | Mechanism |
|---|---|---|
| **1. Identity** | Who you are, how you work, what you expect | Hand-authored. Static. |
| **2. Projects** | Active project briefs — goals, stack, decisions | Hand or generated. Weekly. |
| **3. State** | This week's working memory — what's open, blocked, next | Daily. Manual or auto-refresh. |
| **4. Artifacts** | Code, docs, specs | Referenced (links), not copied. |
| **5. Patterns** | Your prompt templates, rules, rubrics | Hand-authored. Reusable. |

Full narrative: the PickBits Context Stack Field Guide — available at [pickbits.ai/bio](https://pickbits.ai/bio).

---

## What's in this repo

```
.claude/skills/
  context-stack-builder/      Level 1 — bootstrap your stack from an existing
                              project folder + attachments. (Episode 1.)
templates/                    Annotated templates for the three starter layers.
mcp-configs/                  Example connector configs — Atlassian, GitHub,
                              Docs — shipped with episodes 3–6.
```

---

## The series

New skills and integrations land here every week during the launch series. Each episode adds one layer of automation:

1. **Manual Context Stack** — the five-layer practice, hand-authored. *(This repo — `context-stack-builder`.)*
2. **Claude Code Routines** — put your stack on autopilot.
3. **Wire Atlassian** — Jira + Confluence as your Project + State layers.
4. **Wire GitHub** — repos as the Artifacts layer.
5. **Wire Docs** — Drive / SharePoint / Lucid as team memory.
6. **The Full Stack** — all layers, composed, governed.

Follow [@pickbitsai](https://x.com/pickbitsai) for episode drops across Instagram · TikTok · YouTube · X.

---

## Safety

The `context-stack-builder` skill reads files and writes files. Its [safety contract](./.claude/skills/context-stack-builder/SKILL.md#0-safety-contract-non-negotiable) is explicit:

- Reads only from your current working directory.
- Writes only to `./context-stack/`.
- Never touches `.env`, `*.key`, `*.pem`, or anything matching common secret patterns.
- Logs every file read or written in the debrief.
- Never overwrites existing Context Stack files without asking.

Read the skill source before running it. That's the point of shipping it open.

---

## License

[MIT](./LICENSE). Use, fork, adapt. Attribution to `pickbits.ai` appreciated, not required.

---

## Contributing

Bug reports, template improvements, new MCP configs — open an issue or PR. Keep contributions focused: one skill, template, or config per PR.

---

**Field Guide + the full series:** [pickbits.ai/bio](https://pickbits.ai/bio)
**Coaching (1:1):** [pickbits.ai/coaching](https://pickbits.ai/coaching)
**Enterprise team training:** [pickbits.ai/consulting](https://pickbits.ai/consulting)
