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

Install `core` in every repo; add the other categories per repo. A `stack-*` category pairs with `engineering`: leave out the stacks a repo doesn't use.

Commit the installed skills and `skills-lock.json` in each project. To pull updates:

```sh
npx skills@latest update
```

`update` refreshes installed skills only; re-run `add` to pick up skills added here later.

Then, in each repo, run `/ai-docs-setup` once to scaffold `ai-docs/` and the GitHub labels, and add domains with `/domain-create`.

## Modes

A **mode** is a way of working, started with a command at the top of a session: `/mode-engineering` for work on code, `/mode-finance` for a business's finance docs. Work runs through its **playbooks**: you describe the task, and the mode matches it to a list of steps it works through on its own, reading each skill as it needs it. In engineering they are **Spec a feature**, **Build a feature** and **Fix a bug**. To take full control of a session instead, type a skill's command yourself.

- **Start a mode first**, unless the work is general and uses only core skills: those also run on their own, by typing their command.
- **Engineering and stack skills run only under `/mode-engineering`.** Stacks have no mode of their own. When the agent wants a stack skill that isn't installed, it says so once and asks whether to install it or carry on.
- **One mode per session.** To switch, or when a session fills up, `/handoff` to a fresh one. Handing off replaces compaction.
- **Not sure what comes next?** `/mode-engineering-help` maps the flows and skills.

Agents never load skills on their own: skills, modes and the agents they start read skills as files. No project's `AGENTS.md` or `CLAUDE.md` needs a line about skills.

## Included Skills

Skills marked _(reference)_ have no command: modes and other skills read them.

### Core

For any repo, code or not.

- **ai-docs-setup**: scaffold `ai-docs/` (router, glossary, ADR folder, issue tracker context) and the repo's GitHub labels.
- **core-skills** _(reference)_: where skills live and when to read the core ones.
- **domain-create**: add a domain to `ai-docs/`: its router, glossary, and optionally its issue tracker label.
- **domain-modeling**: build and sharpen the domain model in `ai-docs/`: glossaries, ADRs, routers.
- **grill-me**: a relentless interview to sharpen a plan or design.
- **handoff**: write the conversation into a handoff document for a fresh session, and optionally start it in the background.
- **principle-attack-the-premise** _(reference)_: after two failed fixes that share one premise, test the premise.
- **principle-build-the-lever** _(reference)_: build the script or check that does the work or proves it.
- **principle-encode-lessons-in-structure** _(reference)_: turn a repeated instruction into a lint, check or script.
- **principle-explain-the-number** _(reference)_: explain what limits a measured number before trusting it.
- **principle-guard-the-context-window** _(reference)_: route bulk to subagents and keep summaries in the main thread.
- **principle-prove-it-works** _(reference)_: verify against the real artifact before declaring done.
- **principle-sequence-verifiable-units** _(reference)_: break multi-step work into units that each end in a check.
- **research**: investigate a question against primary sources and write up the findings.
- **learn**: learn a new skill or concept over several sessions, in a workspace of lessons.
- **to-questionnaire**: turn a decision you can't fully answer into a questionnaire for someone else.
- **unslop**: cut AI tells from any writing.
- **wait-what**: re-pitch a message that didn't land.
- **writing-for-agents**: how to write skills, `AGENTS.md` and other docs agents read.

### Engineering

For working on code.

- **architect**: design deep modules: sketch types, signatures and module structure before code, with the shared vocabulary for a module's shape.
- **code-review**: two-axis review of changes since a fixed point: coding standards and the originating spec.
- **correct**: change the repo so agents can't repeat a mistake you keep correcting.
- **diagnosing-bugs**: diagnosis loop for hard bugs and performance regressions.
- **grill-with-docs**: a grilling session that writes glossary terms and ADRs as it goes.
- **how**: explain how a part of the codebase works.
- **implement**: implement a piece of work from a spec or tickets.
- **implement-spec**: implement a whole spec and its tickets on one integration branch.
- **improve-codebase-architecture**: find deepening opportunities and grill through the one you pick.
- **mode-engineering**: work on code for the session, with the engineering and stack skills in reach.
- **mode-engineering-help**: ask which skill or flow fits your situation in engineering mode.
- **pr**: write a PR body.
- **principle-boundary-discipline** _(reference)_: validate at system boundaries, trust types inside.
- **principle-exhaust-the-design-space** _(reference)_: prototype competing designs for a decision with no precedent.
- **principle-experience-first** _(reference)_: choose user delight over implementation convenience.
- **principle-fix-root-causes** _(reference)_: fix a bug where the system first went wrong.
- **principle-foundational-thinking** _(reference)_: get the data structures right before writing logic.
- **principle-laziness-protocol** _(reference)_: bias toward deletion and the smallest change.
- **principle-make-operations-idempotent** _(reference)_: converge to the same end state across retries.
- **principle-migrate-callers-then-delete-legacy-apis** _(reference)_: migrate callers and delete the old API in one wave.
- **principle-minimize-reader-load** _(reference)_: collapse layers and hidden state a reader must hold.
- **principle-model-the-domain** _(reference)_: encode the domain in a code structure, not scattered conditionals.
- **principle-outcome-oriented-execution** _(reference)_: converge on the target architecture without throwaway compatibility code.
- **principle-redesign-from-first-principles** _(reference)_: redesign as if a new requirement was there from day one.
- **principle-separate-before-serializing-shared-state** _(reference)_: remove shared writes before serializing them.
- **principle-subtract-before-you-add** _(reference)_: remove dead weight before building.
- **principle-test-behavior-not-implementation** _(reference)_: assert what users can observe.
- **principle-type-system-discipline** _(reference)_: make illegal states unrepresentable.
- **prototype**: build a throwaway prototype to answer a design question.
- **retro**: run a retrospective on a coding session.
- **tdd**: test-driven development, red-green-refactor.
- **teach**: explain a body of work plainly, from how it works and why it's that way.
- **to-spec**: turn the conversation into a spec issue.
- **to-tickets**: break a spec or plan into tracer-bullet ticket issues with blocking links.
- **triage**: move issues through triage, write agent briefs, or close them with an outcome.
- **use-issue-tracker** _(reference)_: the GitHub Issues workflow: labels, commands, specs and tickets, closing.
- **wayfinder**: plan a huge, foggy piece of work as a map of decision tickets.
- **why**: explain why something works the way it does, from the commits and PRs.

### Finance

For a business's finance docs and procedures. Everything about the business lives in the repo's `ai-docs/finance/`; these hold only the ways of working.

- **ledger-entry**: write a check or journal entry to enter manually in QBO.
- **mode-finance**: work on the finance docs for the session, following the business's own procedures.

### Stack: TypeScript

- **typescript** _(reference)_: how TypeScript is written and run across my projects: the rules, modules, Vite+ and the pnpm workspace.
- **typescript-effect** _(reference)_: building production TypeScript applications with Effect v4, including agent-friendly CLIs. Overrides **typescript** in Effect code.

## Credits

Most skills here are adapted from other authors' skills and then changed to fit this workflow. Each adapted skill ships the author's license in its folder, which credits the source, and most keep their upstream name.

- [mattpocock/skills](https://github.com/mattpocock/skills) by Matt Pocock (MIT)
- [kitlangton/skills](https://github.com/kitlangton/skills) by Kit Langton (MIT)
- [humanlayer/skills](https://github.com/humanlayer/skills) by HumanLayer (MIT)
- [pstack](https://github.com/cursor/plugins/tree/main/pstack) by Lauren Tan (MIT): the mode pattern, from `poteto-mode` and `poteto-help`
- [cli-for-agent](https://github.com/cursor/plugins/tree/main/cli-for-agent) by Cursor (MIT): the CLI reference in `typescript-effect`, from `cli-for-agents`

Install skills from this repo only: the adapted ones share their upstream names, so installing the originals alongside would collide.

## Developing Skills

See [AGENTS.md](AGENTS.md) for the layout, frontmatter and licensing conventions, and the steps for adding a skill.

## License

[MIT](LICENSE)
