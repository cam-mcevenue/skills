# Skills

Cameron McEvenue's agent skills, grouped by category, for installing into any project with a skill-aware coding agent. They're built around one workflow: GitHub Issues as the tracker, and agent docs in an `ai-docs/` folder in each monorepo.

## Installation

```sh
npx skills@latest add cam-mcevenue/skills
```

The picker groups skills by category: select a whole category or individual skills. To install specific skills non-interactively:

```sh
npx skills@latest add cam-mcevenue/skills --skill <name> [<name>...]
```

Install `core` in every repo; add the other categories per repo.

Commit the installed skills and `skills-lock.json` in each project. To pull updates:

```sh
npx skills@latest update
```

`update` refreshes installed skills only; re-run `add` to pick up skills added here later.

Then, in each repo, run `/ai-docs-setup` once to scaffold `ai-docs/` and the GitHub labels, and add domains with `/domain-create`.

## Included Skills

Skills marked _(user)_ run only when you type their name; the rest an agent can also reach on its own.

### Core

For any repo, code or not.

- **ai-docs-setup** _(user)_: scaffold `ai-docs/` (router, glossary, ADR folder, issue tracker context) and the repo's GitHub labels.
- **claude-handoff** _(user)_: hand the conversation off to a fresh background agent that picks up the work immediately.
- **domain-create** _(user)_: add a domain to `ai-docs/`: its router, glossary, and optionally its issue tracker label.
- **domain-modeling**: build and sharpen the domain model in `ai-docs/`: glossaries, ADRs, routers.
- **grill-me** _(user)_: a relentless interview to sharpen a plan or design.
- **grilling**: the interview loop `grill-me` and other skills run on.
- **handoff** _(user)_: compact the conversation into a handoff document for another agent.
- **research**: investigate a question against primary sources and write up the findings.
- **teach** _(user)_: teach a new skill or concept within this workspace.
- **to-questionnaire** _(user)_: turn a decision you can't fully answer into a questionnaire for someone else.
- **wait-what** _(user)_: re-pitch a message that didn't land.
- **writing-for-agents**: how to write skills, `AGENTS.md` and other docs agents read.

### Engineering

For working on code.

- **code-review**: two-axis review of changes since a fixed point: coding standards and the originating spec.
- **codebase-design**: shared vocabulary for designing deep modules.
- **diagnosing-bugs**: diagnosis loop for hard bugs and performance regressions.
- **grill-with-docs** _(user)_: a grilling session that writes glossary terms and ADRs as it goes.
- **implement** _(user)_: implement a piece of work from a spec or tickets.
- **implement-spec** _(user)_: implement a whole spec and its tickets on one integration branch.
- **improve-codebase-architecture** _(user)_: find deepening opportunities and grill through the one you pick.
- **pr**: write a PR body.
- **prototype**: build a throwaway prototype to answer a design question.
- **retro** _(user)_: run a retrospective on a coding session.
- **tdd**: test-driven development, red-green-refactor.
- **to-spec** _(user)_: turn the conversation into a spec issue.
- **to-tickets** _(user)_: break a spec or plan into tracer-bullet ticket issues with blocking links.
- **triage** _(user)_: move issues through triage, write agent briefs, or close them with an outcome.
- **use-issue-tracker**: the GitHub Issues workflow: labels, commands, specs and tickets, closing.
- **wayfinder** _(user)_: plan a huge, foggy piece of work as a map of decision tickets.
- **which-skill** _(user)_: ask which skill or flow fits your situation.

### Stack: TypeScript

- **ts-conventions**: how TypeScript is written across my projects.
- **ts-effect**: building production TypeScript applications with Effect v4.

## Credits

Most skills here are adapted from other authors' skills and then changed to fit this workflow. Each adapted skill keeps its upstream name and ships the author's license in its folder, which credits the source.

- [mattpocock/skills](https://github.com/mattpocock/skills) by Matt Pocock (MIT)
- [kitlangton/skills](https://github.com/kitlangton/skills) by Kit Langton (MIT)
- [humanlayer/skills](https://github.com/humanlayer/skills) by HumanLayer (MIT)

Install skills from this repo only: the adapted ones share their upstream names, so installing the originals alongside would collide.

## Developing Skills

See [AGENTS.md](AGENTS.md) for the layout, frontmatter and licensing conventions, and the steps for adding a skill.

## License

[MIT](LICENSE)
