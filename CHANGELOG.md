# Changelog

Versions are stamped in `VERSION`. Downstream projects check with
`bin/scaffold-update --check` and pull with `bin/scaffold-update`.

Each entry names the rule **and the cost that produced it**. A rule without its
cost gets deleted later by someone who doesn't know why it's there.

## 1.5.0

- `CLOSEOUT-RITUAL.md`, Then/step 5 and The commit pattern: the closeout now commits in two commits -- WORKING-AGREEMENT.md, ADRs, and session logs first; the handoff brief second, stamped with the hash of the first commit. The stamp is bumped as part of writing the brief, never by hand afterward.
  *Cost: a single-commit closeout requires the brief to be stamped before the commit carrying it exists, so the stamp names the parent while bin/scaffold-freshness compares against the child, and the ancestry test can never pass. One project left the check red for six consecutive sessions, twice attempting to fix it by amending the commit and re-stamping, and drafted two code changes to the tool before the ritual was identified as the actual defect.*

## 1.4.0

- `PROJECT-INSTRUCTIONS.md`, Standing conventions: added a verification-comparison rule requiring an expected hash, count, or checksum to be generated from a real read, never recalled or retyped.
  *Cost: two comparisons in the same session were checked against a fabricated expected value rather than one computed from the actual file; both apparent "mismatches" were the fabrication, not a real error, but the pattern is indistinguishable from a genuine verification failure until traced back.*
- `PROJECT-INSTRUCTIONS.md`, added near the OBJECTIVE-drift check: a project should periodically check its own settled methods against current outside practice, not only its own internal consistency.
  *Cost: nineteen sessions of internally consistent reasoning about backup strategy, secrets handling, and provisioning tooling had never been checked against what practitioners currently do; one of the four items checked was confirmed as the most serious open risk in the project.*

## 1.3.0

- `PROJECT-INSTRUCTIONS.md`, Standing conventions: the session-numbering rule
  is widened to any identifier that is unique only within a repo, with ADR
  numbers named explicitly; a citation to either must now carry its repo.
  *Cost: two different decisions in two different repos carried the same ADR
  number, and a reader in one repo who looked the other one up found either
  nothing or a confident wrong answer -- the same defect the session-number
  rule was written to prevent, on a second kind of identifier nobody had
  extended it to.*
- `PROJECT-INSTRUCTIONS.md` and `CLOSEOUT-RITUAL.md`: the OBJECTIVE-line
  drift check now reads the line wherever it lives -- `master-plan.md` by
  default, `PROJECT-PROFILE.md` when a project carries no master plan by
  design -- instead of a filename hard-coded to one file. *Cost: a project
  with a legitimately absent master plan carried its OBJECTIVE line in
  `PROJECT-PROFILE.md` instead, and the closeout ritual's drift check had no
  branch for that case -- it silently didn't run for two sessions running.*

## 1.2.0

- `CLOSEOUT-RITUAL.md`: re-pasting the Instructions field is now a **required
  last step**, not an open item -- output the current text of all three
  pasted files and state plainly the session isn't closed until they're
  pasted. *Cost: identified and skipped across multiple consecutive
  sessions, because logging it as a carryover made it feel optional. It is
  the one step no tool can perform; demoting it to a list item is how it
  kept not happening.*
- `PROJECT-INSTRUCTIONS.md`: closeout summary now states the same rule, so
  it loads every session without requiring a read of `CLOSEOUT-RITUAL.md`
  itself.

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
