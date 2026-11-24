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

## Naming

`<ENTITY>` is one of the entities the glossary defines. `[ENTITY_]` marks an optional prefix: with it, the file belongs to that entity; without it, the file is shared by every entity, or belongs to none. Dates are `yyyy-mm-dd`, so names sort.

| Folder | Name | Holds |
|---|---|---|
| `_adrs/` | `<yyyy-mm-dd>_[ENTITY_]<slug>.md`, dated when decided | decisions and their reasons ([Decisions](#decisions)) |
| `governance/` | `<ENTITY>_articles.md`, `<ENTITY>_bylaws.md` | summaries of each entity's articles and by-laws ([Governance](#governance)) |
| `governance/resolutions/` | `<ENTITY>_<yyyy-mm-dd>.md` | every resolution one entity passed that day, in one file ([Resolutions](#resolutions)) |
| `ledger/` | `<ENTITY>_COA.md` | each entity's chart of accounts ([The ledger](#the-ledger)) |
| `ledger/current/` | `<ENTITY>_balance_sheet.csv`, `<ENTITY>_profit_loss.csv` | the latest QBO exports, as exported. Gitignored. |
| `ledger/snapshots/` | `<ENTITY>_<report>_<yyyy-mm-dd>.csv` | temporary dated copies of those exports. Gitignored. |
| `procedures/` | `[ENTITY_]<slug>.md` | repeatable tasks for this business ([Procedures](#procedures)) |
| `records/active/` | `<yyyy-mm-dd>_[ENTITY_]<slug>.md`, dated when it happened | transactions and events that bear on current work ([Records](#records)) |
| `records/archive/` | as `active/` | records no longer relevant |
| `resources/` | `[ENTITY_]<slug>.md`, led by `<yyyy-mm-dd>_` when dated, such as an advisor memo | reference reading: tax rules, advisor details, broker quirks ([Resources](#resources)) |
| `tasks/todo/`, `tasks/done/` | `<nnnnnn>_<slug>.md` | open and finished work items ([Tasks](#tasks)) |

## The glossary

`GLOSSARY.md` defines the names every other file uses:

- **Each entity**, by the prefix files carry. Always refer to an entity by that name.
- **The people**: owners, shareholders, employees.
- **Each advisor**, by the short role name frontmatter uses (`CPA`, `Lawyer` and the like); what each does lives in `resources/`.
- **Report and finance terms** the docs abbreviate, such as COA or FYE.
- **The currency** amounts are in unless stated.

## Frontmatter values

`related-entities` and `entity` take entity names, plus a person's name where one is a party. `advisors`, `owner` and `waiting-on` take advisor role names, or the user's name.

## Governance

A summary of one entity's articles or by-laws, never the document itself:

```md
---
entity: <ENTITY>
description: <one sentence>
---

## Facts
## Amounts
## Implications
```

`## Amounts` is dropped when there are none.

## Resolutions

One file per entity per date, covering every director and shareholder resolution passed that day:

```md
---
entity: <ENTITY>
date: <yyyy-mm-dd>
resolutions:
  - director: <title>
  - shareholder: <title>
  - special: <title>
description: <one sentence>
---

## Facts
## Amounts
## Implications
```

Routine annual resolutions (approving the statements, electing the director, the audit exemption) need no file of their own; note in the entity's latest resolution or a task when a year's are outstanding.

## Records

Records hold facts: the history of a significant transaction or event, its amounts and what follows from it. Open work goes in `tasks/`.

```md
---
date: <yyyy-mm-dd>
related-entities: [<ENTITY>, <person>]
advisors: [<role>]
source: <optional: the documents the record was built from>
description: <one sentence>
---

## Related record
## Facts
## Amounts
## Implications
```

- **One record per transaction or event.** When it involves several entities, keep one shared file, with a `### <ENTITY> side` subsection for each under `## Facts`.
- **`## Related record`** is optional: links to other records, decisions or ledger files.
- **`archive/` is never read** unless the user asks. Only the user moves a record there.

## Decisions

Finance decisions use this format in `_adrs/`, in place of the **domain-modeling** skill's ADR format:

```md
---
date: <yyyy-mm-dd>
related-entities: [<ENTITY>]
advisors: [<role>]
status: accepted
superseded-by:
description: <one sentence stating the decision>
---

## Context
## Decision
## Alternatives
## Consequences
```

- **`status`** is `proposed`, `accepted` or `superseded`.
- **Sections:** `## Context` is the situation and constraints that forced a choice; `## Alternatives` the options weighed and why each lost; `## Consequences` the tax, accounting, cash-flow and governance effects, including anything to revisit.
- **Never rewrite an accepted decision.** To change one, write a new decision and mark the old one `superseded`, naming its replacement in `superseded-by`.
- **Read the decisions** before proposing a change to how something is booked, structured or paid, or when asked why it's done a certain way.

## The ledger

- **QBO is the authoritative ledger**; the files here are copies.
- **A stale export.** Before relying on a report in `ledger/current/`, check its `to_date` reaches the date the task needs. Missing or short, ask the user to export it again.
- **The chart of accounts** marks the entity's general journal clearing account in its Description: the account a check is written against.

## Procedures

A procedure has one shape:

```md
### <Title>

**<What it does and where it ends, in one line.>**

1. <A step. Name each skill it uses in bold, and each file it reads or writes by its path.>
2. ...

**Reply:** <what the final report must contain.>
```

Reference sections may follow the steps. Documents a procedure processes come from `_input/`, and what it produces for the user goes to `_output/`. Business facts stay in the docs a procedure names, not in the procedure: account numbers in the chart of accounts, terms in the glossary, outside parties in `resources/`.

## Resources

Read a resource only when another file links to it or the user asks.

## Tasks

```md
---
entity: [<ENTITY>]
owner: <user or role>
status: open
waiting-on:
created: <yyyy-mm-dd>
completed:
---

## Context
## Done when
```

- **Numbering.** `<nnnnnn>` is the next six-digit number after the highest in `todo/` and `done/` together. Never reuse or renumber.
- **Status.** `open` when the user can act now; `waiting` when blocked, with `waiting-on` naming by whom.
- **Sections.** `## Context` holds why it exists, its figures and links; `## Done when` a concrete finish line.
- **Completing.** Only once the user confirms it's done: set `completed`, add `## Outcome`, move durable facts into a record or the glossary, then move the file to `done/`.
