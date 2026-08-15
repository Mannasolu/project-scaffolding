# Working Agreement -- [PROJECT NAME]

> **What this document is:** the log of corrections about *how we work*, as
> distinct from what we're building. When a working preference gets stated,
> violated, or corrected mid-session, it lands here. At closeout, anything that
> has earned its place gets promoted -- to OPERATOR-PROFILE.md if it follows the
> operator between projects, or to PROJECT-INSTRUCTIONS.md if it is true for any
> operator.
>
> **Why it exists:** the other documents capture the project. None of them
> capture the collaboration. Without a home, a correction stated in chat is
> gone when the chat ends -- and gets rediscovered, at full cost, a few sessions
> later.

**Last updated:** [YYYY-MM-DD]

---

## Active rules
> Currently in force. Operator-tier rules also appear in OPERATOR-PROFILE.md and
> propagate to every project; universal ones live in PROJECT-INSTRUCTIONS.md.
> This section is the reasoning, those files are the load-bearing copies.

| Rule | Why it exists | Session |
|---|---|---|
| [A rule currently in force for this project] | [The reasoning or cost behind it] | [session number] |

---

## Upstream candidates

> Rules that look universal -- true for any operator on any project, not just
> this one. Logged when noticed; promoted by editing the root repo and pushing.
> Once a rule is upstream, delete the row and take the new version with
> `bin/scaffold-update`; keeping a local copy of a synced rule is how the two
> drift apart.

| Rule (personal and domain details stripped) | The cost that produced it | Sent? |
|---|---|---|
| [A candidate rule, generalized] | [What it cost to learn] | [Not yet / version it shipped in] |

---

## Correction log
> Raw entries, newest first. A correction earns promotion when it recurs, or when
> it's clearly general rather than one-off.

### [YYYY-MM-DD] -- [Short description of what happened]

**What happened:** [The situation, what was done, and what correction followed.]

**Why it cost something:** [The turns, rework, or confusion the mistake produced.]

**Rule proposed:** [The rule extracted from the incident, and whether/where it
was promoted.]

---

## Retired
> Rules that stopped applying, and why. Keeping them prevents re-adoption of
> something already tried and abandoned.

| Rule | Retired because | Session |
|---|---|---|
| [A rule that no longer applies] | [What changed that made it obsolete] | [session number] |

---

## Standing notes on drift
> Written instructions reduce drift; they don't eliminate it. Compliance decays
> over a long session regardless of what's on file. Two mitigations, both cheap:
>
> - **A one-word correction.** Enforcement has to cost less than tolerating the
>   drift, or it won't happen. If correcting takes a paragraph, it won't get
>   done.
> - **Closeout before the session gets long.** Most drift shows up late. Closing
>   out earlier is a fix, not just hygiene.
