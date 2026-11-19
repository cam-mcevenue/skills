---
name: sync-skill
description: Copy newly installed third-party skills into skills/<author>/ with attribution, and check existing copies' frontmatter and licenses.
disable-model-invocation: true
---

The user installs skills with `npx skills add`. This skill installs nothing.

An installed skill lives in `.agents/skills/<skill>/` and is recorded in `skills-lock.json`. Its published **copy** lives in `skills/<owner>/<skill>/`, where `<owner>` comes from the lock entry's `source` (`<owner>/<repo>`).

## 1. Sync new skills

A skill is **unsynced** when it's in `skills-lock.json` but has no copy. If no skills are unsynced, tell the user, then go to step 2.

For each unsynced skill:

1. Ask the user for its `category`.
2. Copy `.agents/skills/<skill>/` to `skills/<owner>/<skill>/`, keeping the skill's name.
3. Give the copy the attribution described under [Attribution](#attribution).

## 2. Check existing copies

Check every other copy against [Attribution](#attribution). Report each copy that doesn't match, saying what's wrong. Fix a copy only after the user agrees.

## Attribution

Frontmatter: set these fields, and leave every other field and the body as they are. A `license` field is never added: the `LICENSE` files are the source of truth. If the upstream skill already has a `license` field, the copy keeps it like any other upstream field.

```yaml
metadata:
  author: <author name>
  source: https://github.com/<owner>/<repo>/blob/HEAD/<skillPath>
  adapted-by: <owner.name in .claude-plugin/marketplace.json>
  category: <category>
```

License files:

- `skills/<owner>/LICENSE` holds the upstream repo's license, copied exactly.
- Each copy has its own `LICENSE`, identical to `skills/<owner>/LICENSE`.
- For each work named in `metadata.credits`, the copy also has `LICENSE-<owner of that work>` (for example `LICENSE-humanlayer`). It contains that repo's license, copied exactly. Keep `metadata.credits` and `CREDITS.md` as you found them.

Every license here is expected to be MIT. If any upstream or credited repo's license isn't MIT (its `spdx_id` is anything other than `MIT`, including `NOASSERTION` or no license), stop work on every skill from that repo. Name the repo and its license, and leave the next step to the user.

Look up these facts with `gh`:

- license: `gh api repos/<owner>/<repo>/license`. `.license.spdx_id` names the license, and `.content`, decoded from base64, is its text.
- author name: `gh api users/<owner> --jq .name`. If it's empty, use `<owner>`.
