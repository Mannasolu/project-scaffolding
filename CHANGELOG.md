# Changelog

Versions are stamped in `VERSION`. Downstream projects check with
`bin/scaffold-update --check` and pull with `bin/scaffold-update`.

Each entry names the rule **and the cost that produced it**. A rule without its
cost gets deleted later by someone who doesn't know why it's there.

## 1.8.0

- `bin/scaffold-update`: new files are diffed against `/dev/null` so their full content prints during review; `fetch()` keeps stderr instead of discarding it, and a failed fetch no longer claims the file is "not present upstream"; the script prints its **target** directory and remote URL before anything else.
  *Cost, three defects in one file. Manna-Solutions-llc's first install printed seven empty `=== ` sections and then asked `[y/N]` -- seven files approved with none of their content on screen, because `diff -u "$f"` against a file that does not exist yet errors and `2>/dev/null || true` swallowed both the error and the silence. `fetch()` had the same suppression on both the gh and curl paths, so an auth failure printed an assertion about upstream's contents that the script had no evidence for. And a stray shell prompt in a paste sent this script into an unidentified repo, where it listed six governance files and offered to overwrite them; what stopped it was a version number in scrollback disagreeing, not any control. The script had announced only where it read from since it was written.*

- `PROJECT-INSTRUCTIONS.md`, How to respond: the verification-comparison rule now covers a tool's or an agent's **summary** of a check, not only a recalled value.
  *Cost: a verification `grep` typed at the Claude Code prompt instead of the plain shell. An agent ran it and reported a summary containing a truncating ellipsis; the summary read as confirmation and verified nothing (Manna-Solutions-llc session 001). The same shape appeared twice more in the session that shipped this: `/memory` output was read as proving an import re-reads live when it proves only that the import resolves, and a hand-written patch was checked by re-reading it rather than by running a counter over it -- the re-reading missed what the counter caught in one run.*

- `PROJECT-INSTRUCTIONS.md`, The document set: names `SECURITY-POSTURE.md` and corrects the count.
  *Cost: the section said "four governance documents at repo root" and then listed five, omitting a sixth that `SYNCED` installs. Its ownership -- upstream-owned and overwritten, or project-local -- was determinable only by reading the sync script, while every other installed file's ownership was stated.*

- `docs/specs/component-spec-TEMPLATE.md`: adds `**Executor model:**`.
  *Cost: a bare `claude` command handed over for a site-wide content change; the stronger model was selected only because Claude Code's startup banner suggested it. The operator rule landed at that closeout -- a field in the artifact is a control, a rule in a profile is a reminder.*

- `docs/session-logs/session-log-000-TEMPLATE.md`: adds `**Repo:**` under the title.
  *Cost: session logs are numbered within a repo, and a log that ends up in the wrong repo carried nothing inside it saying where it belonged. An operator preference directing all session logs to one repo made that concrete. With the line, `git grep -n '^\*\*Repo:\*\*' docs/session-logs/` finds misfiled logs from any repo.*

## 1.7.0

- `CLOSEOUT-RITUAL.md`, The required last step / item 1: the closeout now hands over the command that prints the three Instructions files **and appends a sha256 digest of exactly those three**, rather than the assistant's own reproduction of their text. The next session echoes that digest line verbatim and the operator compares it to one generated fresh in one command.
  *Cost: the Instructions field is the one hop no tool can check, and the session-open check added in 1.6.0's era could only ever pass on one of the three files -- PROJECT-INSTRUCTIONS.md defers its version to `VERSION` and carries no value, PROJECT-PROFILE.md has no version line at all. It caught a reported mismatch only because the third file happens to carry a dated line. Separately and worse: that reported mismatch was itself produced without reading the loaded file, and cannot now be confirmed or refuted, because the field was re-pasted before anyone looked at the old text. This is the second recorded cost of the 1.4.0 rule (a verification comparison value must come from the artifact, not memory) -- the rule was loaded, and was broken in the session's second turn. A rule that must be recalled at the right moment is not a control. A digest is: a stale field carries a stale digest, and 64 hex characters cannot be produced from memory.*

- `CLOSEOUT-RITUAL.md`, Then/step 6: the closeout now runs the export check, when the project has an export, and generates the export if it differs. The re-paste step moves to 8.
  *Cost: a release that stops at the source repo has shipped nothing, because downstream projects read the export. A synced file sat a version behind in the export for a day and was found by accident; the release before this one was caught by the export's own leak guard only because the check was run by hand. The check works every time it is run, and nothing runs it.*

## 1.6.0

- `bin/scaffold-freshness`, OPERATOR-PROFILE.md check: compares content three-way with the stamp as merge base, instead of comparing the stamp alone. Reports fresh, stale (re-copy safe), or diverged (re-copy not safe -- promote local edits upstream first). The stamp line is stripped before hashing, since upstream never carries one.
  *Cost: a stamp cannot distinguish "upstream moved" from "local copy was edited" from "both moved." The tool reported an edited copy as fresh, and for the both-moved case prescribed a re-copy that would silently discard local edits. One project's copy carried a stamp comment asserting its contents were identical to upstream; they were not, and the tool agreed with the false claim.*

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
