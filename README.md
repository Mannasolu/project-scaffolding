# Project Scaffolding

**Turn an idea into buildable structure.** This is a template repository: click
**Use this template** and you start a new project with a complete documentation
skeleton already in place -- planning, specs, decision records, session logs, and
a ritual that keeps progress durable across work sessions.

The problem it solves: ideas lose momentum in the gap between "I know what I
want" and "it's actually being built." Progress evaporates when a work session
ends, decisions get re-litigated because nobody wrote down why, and context has
nowhere to live. This scaffolding gives every project the same disciplined shape
from day one, so a person -- or an AI agent -- who has never seen it can read the
docs and know what it is, why it exists, what's built, what's decided, what's
open, and what to do next.

Nothing here is code. The output is *structure*, and the structure is reusable
across any project, in any domain.

## Quick start

1. Click **Use this template** to create your project repo (or clone this one).
2. Fill in `OPERATOR-PROFILE.md` -- how *you* work. Do this once, then copy the
   file into every project you start after this one.
3. Fill in `PROJECT-PROFILE.md` -- what this project is and any rules specific
   to its domain.
4. Paste all three of `PROJECT-INSTRUCTIONS.md`, `OPERATOR-PROFILE.md`, and
   `PROJECT-PROFILE.md` into your AI project's Instructions field.
5. Fill in `docs/planning/master-plan.md` -- even rough. It's the "what and why."
6. Start working. Run the **closeout ritual** (`CLOSEOUT-RITUAL.md`) at every
   stopping point so progress commits durably instead of evaporating.

Periodically, and at closeout:

```
bin/scaffold-update --check
```

## What's inside

```
README.md                  -- this file
PROJECT-INSTRUCTIONS.md    -- the method. Upstream-owned; do not hand-edit
OPERATOR-PROFILE.md        -- how YOU work. Yours; carry it between projects
PROJECT-PROFILE.md         -- purpose, subject, domain rules. This project only
CLOSEOUT-RITUAL.md         -- the end-of-session discipline
WORKING-AGREEMENT.md       -- this project's log of corrections
CHANGELOG.md / VERSION     -- what changed upstream, and which version you're on
bin/scaffold-update        -- pull newer method files from upstream
docs/
  planning/
    master-plan.md         -- what's being built and why
    handoff-brief.md       -- current state; pasted into a fresh session
  specs/
    component-spec-TEMPLATE.md   -- one per component, precise enough for an agent
  decisions/
    adr-TEMPLATE.md              -- one per significant decision (ADR)
  session-logs/
    session-log-000-TEMPLATE.md  -- narrative + teaching, by layer/workstream
```

## The three project documents (they do different jobs -- don't collapse them)

- **Master plan** (`docs/planning/master-plan.md`) -- what's being built and why.
  Scope, model, phases, open questions. Rewritten as v2, v3 when the definition
  changes; never patched with addenda. An addendum that opens by saying the
  previous version no longer describes the project is a rewrite avoiding itself.
- **Handoff brief** (`docs/planning/handoff-brief.md`) -- current state.
  Machines, credentials, what's built, what's decided, what's next, working
  preferences. This is what gets pasted into a new session. Overwritten, never
  accumulated.
- **Session logs** (`docs/session-logs/`) -- narrative and teaching. Organized by
  layer or workstream, NOT by day. A log stays an open draft until its subject
  completes, then one editing pass turns it into a coherent chapter. Numbered
  **within a repo**, not globally.

## Two more, for when a project gets to building

- **Component specs** (`docs/specs/`) -- one file per component, precise enough to
  hand to an agent to build without you in the room. The bridge between the
  master plan and construction. Spec-driven: agree the spec, build to it, then
  update it to match what shipped so the two never drift apart.
- **Decision records** (`docs/decisions/`) -- ADRs. One small file per significant
  decision: what you chose, the alternatives, the cost you accepted. Pulls the
  important calls out of session logs, where they're hard to find and easy to
  re-litigate.

## The documents that govern how you work

- **PROJECT-INSTRUCTIONS.md** -- the generic method. Owned upstream and
  overwritten by the sync, so don't hand-edit it.
- **OPERATOR-PROFILE.md** -- how *you* work: preferences, correction word,
  machines, standing postures. Never synced. Copy it into your next project and
  the scaffolding arrives already educated.
- **PROJECT-PROFILE.md** -- purpose, subject, domain rules. This project only.
- **CLOSEOUT-RITUAL.md** -- the end-of-session ritual that makes progress durable.
- **WORKING-AGREEMENT.md** -- where corrections about *how you work* land. The
  project documents capture the project; none of them capture the collaboration.
  Without a home, a correction stated in chat is gone when the chat ends and gets
  rediscovered at full cost a few sessions later.

## The scaffolding learns

A correction is worth more than the session that produced it. Each one rises as
far as it earns:

1. **This project** -- WORKING-AGREEMENT.md, and PROJECT-PROFILE.md if it's a
   domain rule.
2. **You, on any project** -- OPERATOR-PROFILE.md, once the rule has held in more
   than one project. This is what stops you re-teaching your scaffolding from
   scratch every time you start something new.
3. **Anyone, on any project** -- back upstream into this template, so every
   project made from it inherits the rule.

Tier 3 is why the sync exists. A GitHub template repo shares no git history with
the projects made from it, so there is no `git pull upstream` -- the unit of sync
has to be a file, and you can't safely overwrite a file people hand-edit. Hence
the split: `bin/scaffold-update` overwrites the method and the `-TEMPLATE` files
and never touches your profiles, your planning documents, or your working
agreement.

**A `-TEMPLATE` suffix means upstream-owned and never edited.** Copy from those
files; don't fill them in. Files without the suffix are yours.

## The test of good scaffolding

A person who has never seen the project should be able to read the documents and
know: what it is, why it exists, what's been built, what's been decided, what's
unresolved, and what to do next. If any of those is missing, the scaffolding is
incomplete.
