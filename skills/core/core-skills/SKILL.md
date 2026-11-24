---
name: core-skills
description: Where skills live, and when to read the core ones. Read by modes, workers and other skills.
disable-model-invocation: true
user-invocable: false
---

# Core skills

Bundled skills named in bold are files: read `../<name>/SKILL.md` from this file's folder with the file-read tool. A skill of the same name in the skill listing is a different copy. When a trigger matches, here or in another skill, read that skill in full before acting.

A skill missing from disk isn't installed. In the main session, tell the user once and ask: install it and retry, or carry on without it. As a worker, carry on and name the missing skill in your report.

## Triggers

- Domain terms, a glossary, an ADR, or a folder added, renamed or removed under `ai-docs/` → **domain-modeling**
- A question that needs primary sources, or reading to delegate → **research**
- Writing or editing a skill, `AGENTS.md` or `CLAUDE.md` → **writing-for-agents**
