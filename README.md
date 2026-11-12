# Skills

Cameron McEvenue's agent skills, grouped by domain, for installing into any project with a skill-aware coding agent.

## Installation

```sh
npx skills@latest add cam-mcevenue/skills
```

The picker groups skills by domain: select a whole domain or individual skills. To install specific skills non-interactively:

```sh
npx skills@latest add cam-mcevenue/skills --skill <name> [<name>...]
```

Always-include set for new projects: _none yet_.

Commit the installed skills and `skills-lock.json` in each project. To pull updates:

```sh
npx skills@latest update
```

`update` refreshes installed skills only; re-run `add` to pick up skills added here later.

## Included Skills

### Engineering

None yet.

### Writing

None yet.

## Companion Skills

I use these alongside my own skills and recommend them:

- [mattpocock/skills](https://github.com/mattpocock/skills) by Matt Pocock (MIT). Install them from his repo so updates come straight from the source:

  ```sh
  npx skills@latest add mattpocock/skills
  ```

Any skill here adapted from someone else's carries a "Based on" credit line in its `SKILL.md`.

## Repository Layout

```text
.claude-plugin/
  marketplace.json      one group per domain folder
skills/
  engineering/
    <skill-name>/
      SKILL.md
  writing/
    <skill-name>/
      SKILL.md
```

Conventions:

- each skill lives at `skills/<domain>/<skill-name>/SKILL.md`
- each domain folder has a group of the same name in `.claude-plugin/marketplace.json`; that group is what the install picker shows as a heading
- skills can include supporting files when needed

## Developing Skills

When adding a new skill:

1. create `skills/<domain>/<skill-name>/SKILL.md`
2. add `./skills/<domain>/<skill-name>` to that domain's group in `.claude-plugin/marketplace.json`
3. list it under its domain in this README
4. add supporting files only when the skill needs them
5. keep the skill operational and concise

When adding a new domain, create `skills/<domain>/` and add a matching group to `marketplace.json`.

## License

[MIT](LICENSE)
