# Finance domain layout

The fixed layout of `ai-docs/finance/`. This file is the map for every folder below, so they carry no `ROUTER.md` of their own; the domain's top `ROUTER.md` links its root files and points here.

```text
ai-docs/finance/
├── ROUTER.md
├── GLOSSARY.md
├── _adrs/
├── governance/
│   ├── resolutions/
│   ├── <ENTITY>_articles.md
│   └── <ENTITY>_bylaws.md
├── ledger/
│   ├── current/
│   ├── snapshots/
│   └── <ENTITY>_COA.md
├── procedures/
├── records/
│   ├── active/
│   └── archive/
├── resources/
└── tasks/
    ├── todo/
    └── done/
```

| Folder | Holds |
|---|---|
| `_adrs/` | decisions and their reasons, in the **domain-modeling** skill's ADR format |
| `governance/resolutions/` | resolutions, one per file: `<ENTITY>_<yyyy-mm-dd>_<slug>.md` |
| `governance/` | each entity's constating documents: `<ENTITY>_articles.md`, `<ENTITY>_bylaws.md` |
| `ledger/current/` | the latest QBO exports per entity, as `.csv` exactly as exported: `<ENTITY>_balance_sheet.csv`, `<ENTITY>_profit_loss.csv`. Gitignored. |
| `ledger/snapshots/` | dated copies of those exports: `<ENTITY>_<report>_<yyyy-mm-dd>.csv` |
| `ledger/` | each entity's chart of accounts, with account numbers: `<ENTITY>_COA.md` |
| `procedures/` | repeatable tasks for this business: `<slug>.md`, or `<ENTITY>_<slug>.md` when one entity's |
| `records/active/` | transactions or events still in play: `<yyyy-mm-dd>_<slug>.md` |
| `records/archive/` | settled records, moved from `active/` |
| `resources/` | outside parties and reference: advisors, the broker and its statement footnotes, one file each |
| `tasks/todo/`, `tasks/done/` | task files, below |

## Naming

- **Entities.** A file that belongs to one entity starts with its prefix: `<ENTITY>_`. A file that covers several entities, or none, has no prefix.
- **Dates** are `yyyy-mm-dd`, and lead the name when a file is dated.

## The glossary

`GLOSSARY.md` holds the business's standing terms, beside its other language:

- **Each entity**, as a term naming its prefix: "**ACME**: the operating company. Files: `ACME_`."
- **The report types**, such as the balance sheet and the profit and loss, with the file each lives in.
- **Rates** the procedures use, such as the sales tax rate.

## The ledger

- **A stale export.** Before relying on a report in `ledger/current/`, check it reaches the date the task needs. Missing or short, ask the user to export it again from QBO.
- **The chart of accounts** marks the entity's general journal clearing account: the account a check is written against.

## Tasks

One file per task in `tasks/todo/`, moved to `tasks/done/` when done:

```md
---
status: open
waiting-on:
---

## Context

<why the task exists, with links to records and docs>

## Done when

<the condition that closes it>
```

- **Name**: `NNNNNN_<slug>.md`, the next six-digit number after the highest in `todo/` and `done/`.
- **Status**: `open`, or `waiting` with `waiting-on:` naming who or what.

## Procedures

A procedure has one shape:

```md
### <Title>

**<What it does and where it ends, in one line.>**

1. <A step. Name each skill it uses in bold, and each file it reads or writes by its path.>
2. ...

**Reply:** <what the final report must contain.>
```

Documents a procedure processes come from `_input/`, and what it produces for the user goes to `_output/`. Business facts stay in the docs a procedure names, not in the procedure itself: account numbers in the chart of accounts, terms in the glossary, outside parties in `resources/`.
