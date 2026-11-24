# Skills repo

Cameron McEvenue's skills, installed into other projects with `npx skills add cam-mcevenue/skills`. They serve one workflow, kept consistent across Cameron's projects: GitHub Issues as the tracker, agent docs in `ai-docs/`. Two kinds live here: **own** skills, written here, and **adapted** skills, copied from another author and then changed to fit that workflow. Adapted skills have diverged on purpose: upstream changes are not synced, only the credit is kept. Projects install everything from this repo alone: adapted skills keep their upstream names, so installing the upstream repo alongside would collide.

## Layout

- `skills/<category>/<skill>/SKILL.md`. The categories:
  - `core`: any repo, code or not.
  - `engineering`: working on code.
  - `stack-<name>`: one language or framework, such as `stack-typescript`.
- `.agents/skills/` is the **upstream mirror**: original skills installed with `npx skills add <owner>/<repo>` and tracked in `skills-lock.json`. It records what each adapted skill started from and is never published.

## Install picker

The CLI finds skills only through `.claude-plugin/marketplace.json`; each group there is a heading in the install picker. Edit it by hand:

- One group per category folder, with the same name.
- Every skill appears in exactly one group, as `./skills/<category>/<skill>`, sorted by name.

## Adapted skills

An adapted skill carries its attribution in its `LICENSE`, and only there: the `SKILL.md` frontmatter and body stay free of it, since everything in `SKILL.md` lands in the agent's context. An install copies only the skill folder, so each adapted skill folder carries its own `LICENSE`, copied verbatim from the upstream repo with only its copyright lines changed. Anything outside the folder, symlinks pointing out of it included, never reaches an install.

Unmodified, the upstream copyright line stays and the source follows it:

```text
Copyright (c) 2026 Matt Pocock

https://github.com/<owner>/<repo>/blob/HEAD/<path-to-skill>/SKILL.md
```

Modified, from one work:

```text
Original work Copyright (c) 2026 Matt Pocock
Modified work Copyright (c) 2026 Cameron McEvenue

Adapted from: https://github.com/<owner>/<repo>/blob/HEAD/<path-to-skill>/SKILL.md
```

Modified, from several works (see `skills/engineering/pr/`):

```text
Copyright (c) 2026 Cameron McEvenue

Adapted from the following MIT-licensed works:
- Copyright (c) 2026 Matt Pocock - pr (<url>)
- Copyright (c) 2026 HumanLayer - show-me (<url>)
```

The first edit to an unmodified skill's content switches its `LICENSE` to the modified format, in the same change.

Own skills carry no `LICENSE`.

Read the upstream license before adapting: MIT asks only for the notice, but others add duties (Apache-2.0 requires marking changed files).

## Adding a skill

Keep skills operational and concise; add supporting files only when the skill needs them. Skill names are unique across this repo.

An own skill:

1. Create `skills/<category>/<skill>/SKILL.md`.
2. Add it to its group in `marketplace.json`.
3. Add it to its category's list in `README.md`.

An adapted skill:

1. Install the original into the upstream mirror: `npx skills add <owner>/<repo> --skill <skill>`.
2. Copy `.agents/skills/<skill>/` to `skills/<category>/<skill>/` under its upstream name: skills call each other by name (`grill-me` calls `grilling`), so a rename breaks the callers. Rename only a skill nothing calls, as `ask-matt` became `which-skill`. Bring along every skill it calls.
3. Add the `LICENSE` copy with the copyright lines above.
4. Add it to its group in `marketplace.json` and to `README.md`.

CLI side effects in this repo:

- It links installs into `.claude/skills/`, Claude Code's folder, creating it if missing. Those links point into the mirror and are safe to delete.
- Its "Updating for: … OpenClaw" line appears because OpenClaw's project skill folder is `skills/`. It writes there only if OpenClaw is installed on the machine (`~/.openclaw`); if `skills/<skill>` links ever appear beside the category folders, that is the cause.
