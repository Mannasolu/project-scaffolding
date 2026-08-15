# Changelog

Versions are stamped in `VERSION`. Downstream projects check with
`bin/scaffold-update --check` and pull with `bin/scaffold-update`.

Each entry names the rule **and the cost that produced it**. A rule without its
cost gets deleted later by someone who doesn't know why it's there.

## 1.0.2

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
