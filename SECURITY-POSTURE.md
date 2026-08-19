# Security Posture

> **What this document is:** what a public export of this scaffolding may and
> may not carry, and the standing rules that keep a private practice from
> leaking through a public template. It is **owned upstream** and overwritten
> by `bin/scaffold-update` -- do not hand-edit it.

## What a public export may never carry

- Real names, hostnames, usernames, IP addresses, or key paths -- of the
  operator, any machine, or any collaborator.
- A filled profile, plan, brief, ADR, or session log. Only `-TEMPLATE` files
  and generic method files cross into an export; anything with real content
  stays in the private root by omission, not by scrubbing.
- The private repo's own name or URL, anywhere a script or document would hand
  it to a stranger. See "The export rewrites" below.
- Credentials, tokens, or anything a `.env`-shaped file would hold.

A verification scoped to the files an export step just wrote is narrower than
the deliverable. Check the whole tree the export ships in, not just what that
step touched -- a leak in a pre-existing file outside the edit list is still a
leak (scaffolding session log 005).

**This check is not advisory, and it does not run after the fact.** Anything
that generates an export scans the *complete generated tree* against the
identifier list above before writing a single file to the target, and aborts
on any hit. Scanning afterward, or trusting the generator's own rewrites to
have covered everything, both fail the same way: the leak is already in the
tree a human is about to commit. `bin/scaffold-export` implements this as a
hard abort.

## The export rewrites, it does not copy

Some lines must be *rewritten* to stay correct downstream. Scrubbing is not
only removal.

The rule is about a class of line, not a known instance of one. Any
`UPSTREAM`-shaped default -- any variable naming the repo its own file should
pull from -- must point at the public repo in a public export. The private
root's value is correct there and wrong the moment it ships.

**Scope the rewrite to the pattern, never to a file.** The set of files an
export carries is open-ended and grows; a rewrite anchored to one path and one
variable name is correct exactly until the next script arrives carrying its
own upstream default. That is not hypothetical: the rewrite was written for
`bin/scaffold-update` alone, `bin/scaffold-freshness` was later added to the
export carrying `OPERATOR_UPSTREAM`, and the private repo's name shipped
publicly until a tree-wide grep caught it. The defect was the narrow scope,
not the missed file.

Copying such a line verbatim does two things wrong at once: it leaks the
private repo's name, and it hands a stranger a script pointed at a repo they
cannot read. (Diagnosed scaffolding session log 007; scope corrected after the
leak it missed. `bin/scaffold-export` implements the rewrite across every
staged file, with the tree-wide guard above as the backstop for whatever the
pattern doesn't reach.)

## No org-scoped GitHub features

Nothing in this scaffolding, or in a project built from it, may assume the
account it runs under is a GitHub organization. Confirm with
`gh api /user --jq .type` before designing around org-only features (org-wide
App installs, org template settings, org member access). A personal account
and an organization account differ in exactly the surface most security
tooling assumes exists, and the assumption has already cost one design pass
here.

## GitHub Apps are scoped to selected repositories, never all

An installed GitHub App with **all-repositories** access is invisible to `gh`
-- no CLI enumerates installations against a personal-access-token-authenticated
session; the endpoint requires a token issued by the App itself. It survives
key rotation and re-authentication, and it auto-extends to every repository
created after it was granted. Enumerate installed Apps in a browser, never
assume the CLI's silence means none exist, and re-check at every phase close.
See ADR-003.

## Nothing depends on an unverified external service

Git, pushed to the remote, is the only required transport for anything this
practice depends on. A convenience mirror -- a knowledge-base sync, a
dashboard, a cache -- is fine to use, but nothing may be *load-bearing* until
its actual behavior, not its configured intent, has been verified from inside
the environment that depends on it. The rule that named this cost two
sessions before it was written down: a knowledge base that showed
"Connected" was silently unable to serve a session that needed it. See
ADR-005.

## Version

See `VERSION`. Synced by `bin/scaffold-update`.
