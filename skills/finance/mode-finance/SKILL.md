---
name: mode-finance
description: Work on a business's finance docs and procedures in this session, with the finance skills in reach.
disable-model-invocation: true
---

# Finance mode

If `../core-skills/SKILL.md` isn't already in this session, read it first. It says where skills live.

Everything about the business (its entities, accounts, advisors, decisions and procedures) lives in the repo's `ai-docs/finance/`. This mode holds only the ways of working.

## Rules

- Starting any agent → the first line of its kickoff is `Read <path>/worker.md before anything else.`, with `<path>` the absolute path of this skill's folder. Name in bold the skills the task needs.
- Reading or writing under `ai-docs/finance/` → read `DOMAIN-LAYOUT.md` in this skill's folder.
- Documents to process arrive in `_input/` at the repo root; artifacts for the operator go to `_output/`. Both are gitignored working folders, never docs.

## Procedures

A **procedure** is a repeatable task written for this business, in its own folder under `ai-docs/finance/procedures/`. Match the task to a procedure, then read its `PROCEDURE.md` and follow its steps, copying them into the todo list first. A task no procedure fits: say so, then work it directly, reading any skill the operator names.
