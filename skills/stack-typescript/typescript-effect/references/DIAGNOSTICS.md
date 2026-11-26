# Effect diagnostics

For a repo that runs the Effect language service through `@effect/tsgo` and reports its rules through Oxlint.

## The wrapper

The Effect rules need the Effect-patched Oxlint binding, which `effect-tsgo` preloads. Every lint or check entry point runs through it: the scripts (`effect-tsgo vp check`) and the editor's language servers (`effect-tsgo oxlint --lsp`, `effect-tsgo tsc --lsp --stdio`). Started without it, Oxlint fails to load the config with `Unknown plugin: 'effecttsgo'`. Nothing in `node_modules` is patched. A repo on tsrs instead of tsgo adds `--tsrs-lint` before every Oxlint call (`effect-tsgo --tsrs-lint vp check`) and starts the type server as `effect-tsgo tsrs --lsp --stdio`.

## Two files, two jobs

- **The tsconfig plugin block describes the code.** `effectFn`, `allowedUnstableApis`, `allowedExperimentalApis` and `allowedDuplicatedPackages` are facts the rules need, not policy. A fact the whole repo shares goes in the shared base (often `tsconfig.effect.json`); a fact one package needs goes in that package's `tsconfig.json`.
- **`oxlint.config.ts` decides which rules run and how loudly**: severities, the preset, and per-path `overrides`.

Put a severity in `oxlint.config.ts`. Put a project fact in the plugin block.

## Diagnostics off in the plugin

`diagnostics: false` stops the language service reporting through the TypeScript server, so a finding appears once, from Oxlint, instead of twice (once as `typescript(TS…) effect(…)`, once as `effecttsgo(…)`). This follows upstream's guidance in `Effect-TS/tsgo/docs/README.md`. It silences only the second reporter: the Oxlint rules still run, and hovers, completions, refactors and renames each keep their own flag.

## Facts are load-bearing

An Oxlint rule can be set to `"error"` and still never fire, because the analyzer lacks a project fact. `effect-fn-opportunity` stays silent without `effectFn` in the plugin block. If a rule looks dead, check the plugin options before the severity.

## Prefer an allowlist over a path exception

When a rule fires on sanctioned usage, the narrower fix is usually a fact. List the API in `allowedUnstableApis` (a subtree like `effect/cli`, or one export as `package/module#export`) and the rule stays on everywhere: anything unstable not on the list still warns, even in the package that needed the exception. Switching the rule off for a path hides everything else in that path too. The same pattern covers `allowedExperimentalApis` for `experimental-api-usage` and `allowedDuplicatedPackages` for `duplicate-package`.

## Scoping

Facts scope per package, in that package's `tsconfig.json`. Severities scope by path, through `overrides` with a `files` glob in the root `oxlint.config.ts`.

A package's `plugins` entry **merges** with the base's key by key, so it declares only what it adds. Arrays inside the entry **replace**: a package listing its own `allowedUnstableApis` drops the base's list, so it repeats the base's items.

Avoid the plugin's own `overrides` array (`include`/`exclude`): its patterns resolve relative to the config file that declares them, and a pattern that matches nothing fails silently.
