# [PROJECT NAME] -- Handoff brief

> **What this document is:** current state, pasted into a fresh session to
> resume with full context. Overwritten at every closeout, never accumulated.
> Replace every bracketed placeholder; `bin/scaffold-brief-check` must exit 0
> before the brief is committed.

**Written:** [YYYY-MM-DD], end of [project] session [NNN]

**Stamped:** [short-sha] ([YYYY-MM-DD])

## Objective, quoted verbatim from master-plan.md

> **OBJECTIVE:** [the OBJECTIVE paragraph from docs/planning/master-plan.md, copied verbatim]

This brief quotes; it never paraphrases. `bin/scaffold-brief-check` fails the
brief commit if this paragraph drifts from `docs/planning/master-plan.md`.

## Where things stand

Read from the repo, not asserted.

| Repo | Version | State |
|---|---|---|
| [repo] | [VERSION] | [last commit and what it holds] |

## What was settled

- [A decision made this session that should not be reopened without new information.]

## Open

Item numbers are kept stable across sessions.

1. **[An open item.]** **Waits on:** [what resolves it].

## Single next step

[The one next action, concrete enough to start cold.]

## Opening the next chat -- [project] session [NNN+1]

**Project:** [project]
**Session:** [NNN+1]

**1.** Print the three profiles and their digest:

    cd ~/[project] && git pull && cat PROJECT-INSTRUCTIONS.md OPERATOR-PROFILE.md PROJECT-PROFILE.md && printf '\ninstructions-digest: %s\n' "$(cat PROJECT-INSTRUCTIONS.md OPERATOR-PROFILE.md PROJECT-PROFILE.md | sha256sum | cut -d' ' -f1)"

**2.** Paste that output into the **Instructions field**, replacing what is
there.

**3.** Print this brief and a fresh digest:

    cd ~/[project] && cat docs/planning/handoff-brief.md && cat PROJECT-INSTRUCTIONS.md OPERATOR-PROFILE.md PROJECT-PROFILE.md | sha256sum | cut -d' ' -f1

**4.** Open a new chat in the project. Paste that output as the **first chat
message**, followed by:

    Session [NNN+1]. Before anything else: echo the last line of the
    Instructions field verbatim -- the instructions-digest line -- and compare
    it to the digest above. Report both. A mismatch, or a missing digest line,
    stops the session: the Instructions field is stale.
