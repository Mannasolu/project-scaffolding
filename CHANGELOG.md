# Changelog

Versions are stamped in `VERSION`. Downstream projects check with
`bin/scaffold-update --check` and pull with `bin/scaffold-update`.

Each entry names the rule **and the cost that produced it**. A rule without its
cost gets deleted later by someone who doesn't know why it's there.

## 1.1.0

- `SECURITY-POSTURE.md` added: what a public export may and may not carry, the
  "rewrite, don't copy" rule for `UPSTREAM` lines, the no-org-features rule,
  and the GitHub-Apps-are-browser-only-visible rule. *Cost: these rules
  existed only as prose scattered across ADR-003, ADR-005, and two session
  logs, with no single synced home.*
- `bin/scaffold-freshness` added: checks a commit-hash stamp against the
  upstream `OPERATOR-PROFILE.md` and against this repo's own newest decision,
  so a stale copy or a stale brief is one command away instead of five turns
  of inference. *Cost: a knowledge base served a two-session-stale brief
  (session log 007), and separately, a brief kept pointing at a task ADR-005
  had already closed (session log 008) -- the same defect, twice, with
  nothing that would have caught either.*
- `bin/scaffold-export` shipped in the private root (not synced -- private-repo
  tooling): generates the public export from this repo instead of the export
  being hand-maintained. *Cost: an org-placeholder fix landed as an
  uncommitted patch directly in the public clone, with no source for it in
  this repo -- exactly the defect class this script exists to close.*

## 1.0.2

No change to synced files. Version bumped alongside the promotion-loop
closeout (scaffolding session log 004) for consistency with the repo's
release cadence.

## 1.0.1

- Removed dangling `CONTRIBUTING.md` references left in `CLOSEOUT-RITUAL.md`,
  `PROJECT-INSTRUCTIONS.md`, and `README.md` after the file itself was deleted
  as premature. *Cost: deleting a file is cheap; deleting a file other files
  still point at is not.*

## 1.0.0

First public version.

- Four governance documents split into five: the method (upstream-owned) is now
  separate from the operator profile (yours, carried between projects) and the
  project profile (this project only). *Cost: a single instructions file cannot
  be both synced from upstream and hand-edited locally -- one of the two always
  loses.*
- `bin/scaffold-update` added: overwrites only files no project edits. *Cost: a
  GitHub template repo shares no history with projects made from it, so
  `git pull upstream` is unavailable and the sync unit has to be a file.*
- Correction harvest extended from two tiers to three, with an "Upstream
  candidates" table in `WORKING-AGREEMENT.md`. *Cost: a rule that stops at the
  project boundary gets rediscovered, at full price, by the next project.*
- `handoff-brief.md` template added -- the README had promised it without
  shipping one.
- `-TEMPLATE` suffix defined as meaning upstream-owned and never edited, so the
  sync set is legible from the filename alone.
