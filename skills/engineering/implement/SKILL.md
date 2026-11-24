---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

If the user passes a ticket reference, fetch it (`gh issue view <n> --json title,body,labels,comments`) and state its title before starting. If the reference is ambiguous, ask. If the ticket doesn't carry `ready-for-agent`, say so and wait for the user's go-ahead: that label is the work queue.

Call the Skill tool with "tdd" where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, call the Skill tool with "code-review" to review the work.

Commit your work to the current branch.
