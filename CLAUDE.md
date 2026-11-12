# Skills repo

Public skills installed into other projects with `npx skills add cam-mcevenue/skills`. The `skills` CLI builds its install picker from `.claude-plugin/marketplace.json`: each group there becomes a heading.

## Layout

- Every skill lives at `skills/<domain>/<skill-name>/SKILL.md`.
- Every domain folder has exactly one group in `.claude-plugin/marketplace.json`, named after the folder.
- Every skill path (`./skills/<domain>/<skill-name>`) is listed in its domain's group, and only there.
- A new domain is a new folder plus a new group.

## Adding or changing a skill

- Keep skills operational and concise; add supporting files only when the skill needs them.
- Choose a name unique across this repo and mattpocock/skills: projects install both, and every skill lands in the same flat folder.
- A skill adapted from another author's opens its body with a credit line: `Based on <skill> from <repo-url> (<license>).`
- Update the domain's list in `README.md` whenever a skill is added, renamed, or removed.
