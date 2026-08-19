# The Closeout Ritual

> The end-of-session discipline that keeps progress durable. This is the reusable
> pattern -- it works for any project, in any domain. Its substance also lives
> inside PROJECT-INSTRUCTIONS.md so it loads every session.

## The principle

Continuity across sessions is preserved by the repo documents, not by any tool's
memory. The documents ARE the memory. There is no background automation for the
thinking half -- deciding what changed and writing it down needs a brain in the
loop. So the ritual is manual by necessity, and it works exactly as well as the
discipline behind it.

This applies to the collaboration as much as the project. A correction about how
the work goes is state too, and it evaporates the same way if nobody writes it
down.

## Trigger

When you say "let's close out," OR when the chat is getting long. The assistant
should offer it proactively in the second case -- not wait to be asked.

## The four things produced

1. **Updated handoff brief** -- rewrite only what changed; say plainly when
   something didn't.
2. **Session log additions** for the layer or workstream worked on.
3. **Working-agreement entries** -- any correction about *how the work goes* that
   came up this session. If one has recurred or is clearly general, promote it
   into PROJECT-INSTRUCTIONS.md so it loads automatically next time. This is the
   step that stops the same correction being rediscovered every few sessions.
4. **A one-line summary** of what changed and what's still open.

   Before writing the session log, read the OBJECTIVE line in `master-plan.md`
   and ask whether this session served it. If it did not, the log says so in
   one sentence. A session spent on the scaffolding rather than the subject is
   legitimate; a run of them unnoticed is not.

## The fifth thing: upstream candidates

The four outputs above keep *this* project's progress durable. They stop at the
project boundary. A rule that would be true of any project, for any operator, is
worth more than one project's worth of use -- and if it only ever lands in this
repo, the next project starts by rediscovering it.

So at closeout, ask one more question: **did anything this session survive having
every personal and domain detail stripped out of it?** If yes, log it under
"Upstream candidates" in WORKING-AGREEMENT.md then edit the root repo and push.

The bar is high on purpose. Most corrections are operator habits, not universal
method -- those belong in OPERATOR-PROFILE.md, where they follow you between
projects without bloating the file everyone downstream loads. A rule earns tier 3
only when the cost that produced it would have been paid by a stranger too.

Also cheap and worth doing here: run `bin/scaffold-update` to see whether the
method files have moved upstream since the last session.

## Where a correction goes

Not everything that comes up is a working preference. Route by kind:

- **How the work goes, here** -> WORKING-AGREEMENT.md.
- **How this operator works, anywhere** -> OPERATOR-PROFILE.md, once it has held
  in more than one project.
- **How anyone should work, anywhere** -> upstream, into PROJECT-INSTRUCTIONS.md.
- **A domain rule for this project** -> PROJECT-PROFILE.md.
- **A project fact** -> handoff brief.
- **A decision with alternatives** -> ADR.
- **A teaching moment** -> session log.

Two failure modes to watch:

**Silent repetition.** The same correction three sessions running means the
harvest isn't happening. Three occurrences is the threshold -- write it down or
stop calling it a preference.

**Instruction bloat.** A one-off doesn't earn a line in the instructions file.
That's what the working agreement's correction log is for. If the instructions
grow past what loads usefully at the start of every session, consolidate --
several specific corrections usually collapse into one general principle.

## Then

5. Save and commit to the repo with a git message that names the session.
6. Before ending, state the single next step, so the next session opens with no
   guessing.
7. **Last: re-paste the Instructions field.** Required, not an open item --
   see below. This is deliberately the final step in this list so it cannot
   be buried under whatever comes after it.

## The commit pattern

```
git add docs/ *.md
git commit -m "session NNN: short description"
git push
```

## The required last step: re-paste the Instructions field

**This is not an open item, and it does not get logged for later.** It has
already been identified and skipped across multiple consecutive sessions --
not because it's hard, but because it always sat last in a list of
carryovers that felt optional. It isn't optional. It is the last thing this
ritual asks for, on purpose, so nothing that follows it in a session can
bury it again.

**No tool performs this step.** `PROJECT-INSTRUCTIONS.md`, `OPERATOR-PROFILE.md`,
and `PROJECT-PROFILE.md` live in git; the AI project's Instructions field has
no API. Nothing on any machine you own can read or write it. The only
transport is a human pasting. `bin/scaffold-freshness` checks the other two
hand-moved documents in this practice -- it cannot check this one; see
ADR-007's "Known limit."

So the assistant's part of this step is not "do it." It is:

1. **Output the current, post-commit text of all three files** --
   `PROJECT-INSTRUCTIONS.md`, `OPERATOR-PROFILE.md`, `PROJECT-PROFILE.md` --
   in full, ready to paste, at every closeout. Not a diff, not a summary of
   what changed in them -- the complete text, every time, because a partial
   paste is a new way to get this wrong.
2. **State plainly: the session is not closed until these are pasted.** Not
   "when convenient." Not carried forward as an open item -- naming it as an
   open item is exactly how it has been skipped before. It is named as the
   literal last thing standing between this session and done.
