# Skills repo

Cameron McEvenue's skills, installed into other projects with `npx skills add cam-mcevenue/skills`. Two kinds live here: **own** skills, written here, and **adapted** skills, copied from another author and then changed. Projects install everything from this repo alone: adapted skills keep their upstream names, so installing the upstream repo alongside would collide.

## Layout

- `skills/<author>/<skill>/SKILL.md`, where `<author>` is a GitHub handle. `skills/cam-mcevenue/` holds own skills; every other author folder holds adapted ones.
- `skills/<author>/LICENSE` is that author's license, copied verbatim from their repo: the master each of their skill folders gets a copy of.
- `.agents/skills/` is the **upstream mirror**: original skills installed with `npx skills add <owner>/<repo>` and tracked in `skills-lock.json`. It exists for diffing against upstream and is never published.

## Install picker

The CLI finds skills only through `.claude-plugin/marketplace.json`; each group there is a heading in the install picker. Edit it by hand, keeping it in step with frontmatter:

- Every skill appears in exactly one group, as `./skills/<author>/<skill>`.
- The group name is the skill's `metadata.category`, plus `-<author>` for adapted skills: `engineering`, `engineering-mattpocock`, `engineering-kitlangton`.
- Groups sort by category, the own group first within each.

## Frontmatter

Every skill sets `metadata.category`. An adapted skill also carries its attribution in frontmatter, and only there; the body opens straight into the skill:

```yaml
license: MIT
metadata:
  author: Matt Pocock
  source: https://github.com/<owner>/<repo>/tree/<commit>/<path-to-skill>
  adapted-by: Cameron McEvenue
  category: engineering
```

`source` pins the upstream commit the copy was last synced from (`commit` in `skills-lock.json`).

## Licensing adapted skills

An install copies only the skill folder, so each adapted skill folder carries its own `LICENSE`, a copy of `skills/<author>/LICENSE`. Anything outside the folder, symlinks pointing out of it included, never reaches an install.

- Keep upstream credits as found: `metadata.credits` and `CREDITS.md`. For each work they credit, add that owner's license verbatim as `LICENSE-<owner>` (see `skills/mattpocock/pr/`).
- Copy license text verbatim, copyright lines included.
- Read the upstream license before adapting: MIT asks only for the notice, but others add duties (Apache-2.0 requires marking changed files).

## Adding a skill

Keep skills operational and concise; add supporting files only when the skill needs them. Skill names are unique across this repo.

An own skill:

1. Create `skills/cam-mcevenue/<skill>/SKILL.md` with `metadata.category`.
2. Add it to its group in `marketplace.json`.
3. Add it to the skill list in `README.md`.

An adapted skill:

1. Install the original into the upstream mirror: `npx skills add <owner>/<repo> --skill <skill>`.
2. Copy `.agents/skills/<skill>/` to `skills/<author>/<skill>/` under its upstream name: skills call each other by name (`grill-me` calls `grilling`), so a rename breaks the callers. Bring along every skill it calls.
3. Add the frontmatter above and the `LICENSE` copy. A new author also gets `skills/<author>/LICENSE`.
4. Add it to its group in `marketplace.json` and to `README.md`.

## Syncing upstream changes

1. Run `npx skills update` here. It replaces a mirrored skill's whole folder, and only when upstream has changed.
2. `git diff .agents/skills/<skill>` shows what upstream changed. Port the changes worth keeping into `skills/<author>/<skill>/` and bump the commit in `source`.
3. Commit the mirror, `skills-lock.json` and the ports together.

CLI side effects in this repo:

- It links installs into `.claude/skills/`, Claude Code's folder, creating it if missing. Those links point into the mirror and are safe to delete.
- Its "Updating for: … OpenClaw" line appears because OpenClaw's project skill folder is `skills/`. It writes there only if OpenClaw is installed on the machine (`~/.openclaw`); if `skills/<skill>` links ever appear beside the author folders, that is the cause.
