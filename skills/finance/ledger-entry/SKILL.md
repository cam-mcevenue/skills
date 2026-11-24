---
name: ledger-entry
description: Write a ledger check or journal entry for the user to enter manually in QBO.
disable-model-invocation: true
---

Generate the appropriate entry using the exact Markdown format below.

## Rules
- Use the check format for checks and the journal entry format for journal entries.
- Include HST in the HST column only; never create a separate HST line.
- Leave the HST cell empty when no HST applies.
- For checks, prefix all amounts with + or -.
- A check's **ACCOUNT** is the entity's general journal clearing account, from its chart of accounts.
- Do not include explanations outside the entry unless clarification is needed.

# Check
```markdown
| Account | Description | Amount | HST |
| --- | --- | ---: | ---: |

**DATE:** <date>
**ACCOUNT:** <the entity's general journal clearing account>
**MEMO:** 
<Concise descriptive memo>
```

# Journal Entry
```markdown
| Account | Debit | Credit | Description | HST |
| --- | ---: | ---: | --- | ---: |

**DATE:** <date>
**MEMO:** 
<Concise descriptive memo>
```
