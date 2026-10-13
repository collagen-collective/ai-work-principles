# Keeping the record

You build, measure and keep the record (`PRINCIPLES.md`). This is how the record is kept: a log of
what was tried and what happened, written so that whoever comes to the work cold, whether the person
after a week away, the next session or an agent it starts, can tell what was decided, by whom, and
why. It came from the design logs of games built with an agent, one of which reached four hundred
entries in its first two weeks, and its examples are from those games.

## The log

**One file, in past tense, oldest first.** What was tried and what happened. The project's agent
file says where it is. A statement of what is settled, such as a charter, a spec or a README, states
conclusions; it cannot hold the reasoning that produced them, or the dead ends, or the places where
solving one problem quietly changed the answer to another one upstream. Read end to end, the log is
the story of how the work got where it is.

**Append only.** Never edit an old entry to make it agree with current thinking, because an entry is
a historical account, and a historical account cannot go stale. If today contradicts an old entry,
that is a new entry. It also keeps the log's cost flat: a record that is only ever added to never
has to be reconciled with itself, and reconciliation is where earlier ways of tracking work broke
down. The one exception is something that should never have been written down at all, such as a
credential or a patient's identifier: remove it, and say in a new entry what kind of thing was
removed and why, without repeating it. It is still in the history, so treat a credential as exposed.

**In order of time, not by subject.** The chronology is the part that is hard to reconstruct, and
grouping is the part a search recovers for free.

**What earns an entry.** A decision that was reversed. A decision that cost something. A thing that
was built and then deleted. A sitting. A merge of work built apart. And any moment where solving one
problem changed an answer somewhere else. Not routine implementation, and not decisions nobody has
ever questioned: those belong with what is settled.

## The heading

```
### YYYY-MM-DD · A title that says what happened `[tag]` `[tag]`
```

Get the date from the system (`date +%F`) rather than guessing it.

The title is a sentence, not a label: "The ban was on telling, and the signs stay", not "Sign
placement". Two clauses is the house rhythm, and the second usually carries the surprise.

**If the entry is a sitting, say so in the title, and date it to when the sitting happened.** Begin
the title with *Sitting:*. A tag alone is not enough: the headings are how the log is skimmed, and a
sitting titled by the conclusion it reached disappears into the index. In one game's log, eleven
entries in two days were sittings, each titled by what that stretch of play concluded, and a reader
of the headings came away thinking the game had gone unplayed for three days. It had been played
repeatedly.

## Tags

Tags exist to be searched, so **reuse one rather than coining a synonym**. Before inventing a tag,
see what is already in use (with the project's own path to the log):

```bash
grep -o '`\[[a-z-]*\]`' docs/LOG.md | sort | uniq -c | sort -rn
```

Three transfer to any project and are worth using from the first entry: `[process]` for how the work
itself is done, `[build]` for the tooling the work runs on, and `[sitting]` for an entry that writes
one up. The rest of the vocabulary is the project's own and accumulates one subject at a time: coin
a tag when a second entry wants it, not in advance. And when two that look alike mean different
things, write down which is which. One game's log used `[playtest]` for a sitting and `[play]` for
anything a person playing it said, in a sitting or out of one, and kept the two apart for a week
before anything said so.

### Two status tags, and they describe the new entry

Those are subject tags. Two more say what an entry does to the questions left open:

- **`[later]`**: this entry parks a question that cannot be answered yet, usually because what it is
  about does not exist yet. It must carry **what good and bad would look like** and **what has to
  exist first**, because that second thing is the trigger that makes it findable at the right
  moment. A parked question that does not say what good looks like is a note to self. To find the
  ones still open, set the `[later]` headings against the **Resolves** lines:
  `grep -nE '\[later\]|[Rr]esolves\.' docs/LOG.md`.
- **`[resolved]`**: this entry closes a question an earlier entry left open, and names which. Not
  only `[later]` ones: an entry that ends by naming what it did not settle, or that writes a cost
  down as a bill for later, has left a question open just as squarely. **What does not earn it is a
  citation.** A log references its own past constantly, and almost none of that is resolution. The
  test is whether the earlier entry named something as open and this one closes it.

**Both tags go on the new entry, and neither is ever added to an old one.** That is the append-only
guideline: a tag added to an old entry is still an edit to a historical account, and the fact that
it is only an index does not make it not an edit.

## `Resolves`, and why entries need no ids

A closing entry carries one more label, first, before **Problem**:

```
**Resolves.** `2026-09-25 · The animals' instruments become a skill, and the gulls it passed as
healthy were spinning on the spot` — *what they picture a flock doing once it is up*.
```

**The id is the heading.** Date and title together are unique across the log, so they identify one
entry exactly, a person can read them, and `grep` finds the entry in one hop. Anything shorter, a
number or a slug, would have to be written into the entry it names, and retrofitting ids onto
entries that already exist is the same edit to history as tagging them, spread over every entry
instead of one. A derived id costs nothing and cannot disagree with what it names.

Quote enough of the title to be unique, with its date (a distinctive fragment is fine), and after a
dash, the question it closes, in the earlier entry's words where it has them. An entry that closes
only part of a question says **Partly resolves.** and names the part.

**And because the id is the heading, granularity is free.** Nothing asks for one entry per day or
per session: a date can carry as many entries as it needs, and each is still addressable. Split when
a session did things on different axes, and keep it together when the parts only make sense in
sequence. The only question worth asking is which one a reader would rather find.

## The beats

Most entries move through five, as bold labels at the start of a paragraph:

- **Problem.** What was actually wrong or unanswered, written as it looked at the time, not as it
  looks now that you know the answer.
- **Attempt.** What was built or decided, specifically enough to picture.
- **Outcome.** Held, removed on a date, reversed, or still in progress: say which. Be willing to
  write down that it failed. A log that only records successes is advertising, and nobody consults
  advertising.
- **Learned.** The transferable part, stated so it can be applied to something else.
- **Changed elsewhere.** What this forced, allowed or invalidated somewhere else. If the honest
  answer is nothing, write nothing, but check twice, because this is where the expensive couplings
  hide.

It is a voice, not a form: expect about half of entries to drop a beat they do not need, and many to
carry a label of their own where the entry has a second half worth naming. **Found and left** is one
worth having: something noticed on the way and out of the entry's scope, written down so that nobody
chases it again unawares. Follow the shape of what happened rather than filling the boxes.

When that second half is a decision made with the person, label it **The decision**, and give it in
their own words where they gave them. A ruling is handed down by a judge; these are worked out
together. One game's log called them *the ruling* for its first ten days, and nothing in its
guidelines told an agent to treat the person as a judge: the label, copied from entry to entry, did
it anyway.

Two beats are worth protecting:

- **Changed elsewhere** is why the log exists. It is where solving one problem quietly changed the
  answer to another, and it is the only place those loops are visible. If a decision changed what is
  settled, or moved an open question, say which. **And if the decision removed something, search
  everything the project keeps for what cited it before closing the entry.** Most sentences in a
  statement of what is settled are a conclusion and a reason; retire the reason and the conclusion
  reads perfectly well forever, so nothing will ever tell you. The moment of the decision is the
  only cheap time to catch it, because it is the only time you still know the word to search for.
- **Learned** should still be true about the next problem nobody has thought of yet. If it only
  restates the outcome, the entry is not finished. A Learned has a trigger and a verb or it has
  neither: "after a scripted edit, search for the new text" fires on its own, and "the instrument
  was missing what the question needed" cannot, because there is nothing in it to obey. **If it is a
  lesson about how to work, write it where the principles are kept as well**, under *This project's
  own*, as `PRINCIPLES.md`'s *When you learn something* says: propose it to the person, work out its
  wording with them, end it with this entry's heading, and say so under **Changed elsewhere**. A
  lesson a principle already says needs no second copy: name the principle in this entry instead.
  The log is append only and read backwards, and a lesson left only here has been filed where nobody
  looks before acting, which is how the same lesson gets written three times.

## Whose words are whose

A week on, a log that mixes the person's decisions with an agent's calls reads as though every
sentence carried the same authority, and nothing in it says otherwise. So keep them apart where they
are written:

- **Their decisions, in their words.** Quote them. A paraphrase is your reading of what they said,
  and it is the reading that will be cited.
- **An agent's own calls, listed as the agent's**, each with the reason it protects. A call written
  down without its reason can only be defended or thrown out whole. One game's first entry listed
  seven of them under a title that said why: *so they stay distinguishable*.
- **The work's readings**, where their words left an edge open and the work had to choose one. Say
  so, and name the value that decided it, so they can move it.
- **What they did not say.** Silence is not a decision, and a general "yes" closes nothing in
  particular. Write down which open questions it did not answer, and ask.

If they ask you to fill something in on their behalf, say once that it will read as settled later,
then do what they asked, and write down that it was drafted by an agent rather than decided.

## The shapes entries have grown into

These are a voice too, not forms. They are written down because a convention that lives only in the
entries spreads by imitation: an agent told to match the last few entries learns whatever they
happen to say, which is how *the ruling* travelled. Written down, a shape can be chosen rather than
caught.

**A sitting.** By its second week, one game's sittings had settled into a shape worth starting from:

- **Resolves.**, first, when the sitting answers a question an earlier entry left for it.
- **What they tried.** When, which version (the commit), and which part of the work.
- **What worked, and it is the half to protect.** In their words, one thing at a time. It is the
  half that gets skipped, and the only half that tells the next change what not to break.
- **What they expected.** What they thought would happen, before what did. It is the sentence worth
  most, because an agent can find a defect and cannot find an expectation.
- **What they must have been able to see to say it.** A complaint that the *second* beacon did not
  light is evidence that the first one was legible at range, that they could tell two apart at a
  distance, and that they were reading the network rather than the scenery.
- **Not said.** What the sitting did not reach or did not answer, so that nobody reads silence as a
  decision.
- **What it asked for**, and **The decision**, where one was made.

If their notes do not say whether they used the thing itself or judged it from something standing in
for it, such as pictures of a screen or a summary of a result, ask before writing it up as a
sitting. A sitting written up from stand-ins drops out of the count of how often the work has been
tried, and that count is the one thing the log cannot rebuild. When they agree to something from a
stand-in, say so: it still wants trying.

**A build or a result.** Ends on **What it needs from a person**: a few things worth trying or
reading in a minute, with where to find them; what good and bad would look like; and the number most
likely to be wrong, labelled as a measurement rather than a judgment. Offered, not assigned.

**A merge.** What came in. What each side's log said the other would need, read from both sides'
**Changed elsewhere**, and done or handed on. What the merge made untrue. And any collision that was
behaviour rather than text, which no merge tool can see: two actions on one key, or a fix that has
to be made again in a file the other side rewrote.

**A brief picked up from another session.** Who handed it on, and what it asked. What its numbers
came to when rebuilt, and **Where the brief was wrong**, if it was: notes written from reading code
tend to be right about where things are and wrong one step past that.

**A plan.** Says that it is a plan, and that nothing is built yet. The entry that reports the round
built resolves it, and ends on what is left, measured, for the person to choose from.

## Handing the work over

A pull request, or any summary of a stretch of work, is read by someone outside the session, coming
to it cold or back to it after a while. It says why the work was done, what is now settled and why,
and what is still open, in the words they would use. What is settled is a black box: how it works
and how it got there are in the commit log and the log, for whoever returns to that part. Every
sentence is one that reader needs now. One shape has held up:

- **What changed.** Why the work exists, which is most of this section: the goal it served and where
  it started (a plan, a report, a sitting). Then, in a paragraph or two of prose, what someone using
  it can now do that they could not: an overview, not an itemization by commit or by feature, and as
  they would notice it rather than how it works. "Shores slope more gently now, which moved a few
  docks", not "The shore uses a falloff curve (a1b2c3d), which moved seed 12's dock, so the dock
  tests moved to seed 30 (d4e5f6a)." Things are called what a newcomer would call them, not by the
  code's or the session's names for them. A commit is named only where a reader may need to revert
  it. The whole section is 250 words at most, however much the work holds.
- **Needs a person.** Changes to what was settled, questions only they can judge, and decisions the
  work is waiting on, each in two sentences at most: the question, and only what it takes to answer
  it. "Night as the default came up but isn't done yet. Here, or in its own PR?" A decision already
  made is said with its reason, not with the history of how it was made. "Nothing" is an answer.
- **Tried.** How the sittings went, in a sentence: how many, and whether they brought back a lot or
  a little. Then the few things they changed most, each told as why: "The first boats turned on the
  spot, which didn't feel like sailing, so a boat now has to be moving to turn." If nobody has tried
  it yet, what someone trying it should look at.
- **Measured.** The few numbers a reader needs now: those an open question or a decision rests on,
  and any cost the change brings, each with what it means and where it was taken. "An island takes 4
  s to build, up from 2 s (seeds 1–10): the price of the new shores", not a table of every count
  taken along the way. Measurements, not judgments. "Nothing" is an answer.
- **Verification.** How the final run went: the gate on the last commit, and CI's result, read after
  the push. An earlier run belongs here only if it left something open, such as a failure that went
  away with no cause found.
- **Not in this.** What was left out, or found and not fixed, and why.

## Before writing

Read the last three entries. The register is specific, argumentative and unhedged, with every guess
labelled as one, and it is easier to match than to describe. Match their register, and check their
labels against this file before you copy them.

If there are none yet, a good first entry is the project's founding decisions, written down the day
they are made, while the reasoning still seems too obvious to record.
