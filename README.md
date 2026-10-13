# ai-work-principles

Principles for a person and an AI agent working together, where the agent does most of the typing
and the person decides what the work is for: a program, a game, an analysis. They came from games
built that way, and are written here for any work.

## What is here

- **[`PRINCIPLES.md`](./PRINCIPLES.md)**: how we work. The stance, then eight principles, each a
  trigger and an action for a kind of problem, with its reason, *Looks like* lines for code and for
  data analysis, and one example from the games. It ends with the few terms these files use. It is
  the file an agent reads every session.
- **[`RECORD.md`](./RECORD.md)**: keeping the record. An append-only log of what was tried and what
  happened, whose words are whose, writing up a sitting with the person, and handing work over.
- **[`CLAUDE-CODE.md`](./CLAUDE-CODE.md)**: what is particular to Claude Code. Where the principles
  go so that they stay read, calls that wait for the person, allow rules, sub-agents and skills.

## Where they came from

They began in a game project that reached a thousand commits and fifty thousand lines of production
code, with as much again in tests, before anyone checked whether it was fun. Every automated check
passed throughout. The build at the end booted into two zones and one quest that was already
complete when it loaded. An audit found forty modules that nothing in the game reached, under six
thousand lines of passing tests, and an enemy damage event that nothing subscribed to, which had
left the player invulnerable in every green build for weeks. A throwaway prototype of under nine
hundred lines, judged on nothing but whether it was fun, was a better game.

So [`ts-game-template`](https://github.com/collagen-collective/ts-game-template) started with no
code, kept the design in three short documents, and put a build the person could play seconds away.
Each game built from it since sent back what it paid for. The template merged those lessons, pruned
them into eight principles, and tried the result on fresh agents (*Changing the principles*, below).

Little of what they taught is about games. A check that passes while the work fails at what it is
for is the same failure in an analysis as in a game, and the person's judgment is as scarce. This
repository holds what applies to any work, with cues for code and for data analysis, and the
template keeps the cues that are about games.

## Using them in a project

The files are used as they are, like a package: a project copies them in unedited and keeps its own
lessons beside them, so that an update can replace the copies whole.

**In Claude Code,** copy `PRINCIPLES.md` and `CLAUDE-CODE.md` into
`.claude/rules/ai-work-principles/`. Files there load at the start of every session and come back
after the context is compacted, which the documentation does not promise of a file that `CLAUDE.md`
imports (`CLAUDE-CODE.md` has the detail). `RECORD.md` is needed only when the log is written, so it
goes beside the log rather than into every session's context. Then say in the project's `CLAUDE.md`
where the two are, and give the project a section of its own:

```markdown
## How we work

How we work is in `.claude/rules/ai-work-principles/`, from
[ai-work-principles](https://github.com/collagen-collective/ai-work-principles). The log is
`docs/LOG.md`; read `docs/RECORD.md` before writing an entry.

### This project's own

*None yet. A lesson this project learns goes here as a* Looks like *line under the principle it
extends, named by number and title, or as a new principle in the same shape, ending with the log
entry it came from.*
```

**For your own sessions rather than one project's,** copy `PRINCIPLES.md` and `CLAUDE-CODE.md` into
`~/.claude/rules/` instead, and `RECORD.md` into a project when it starts keeping a log. The two
then load in every project on that machine, and nothing is committed to any repository, which suits
work whose repositories you cannot or would rather not change. Where a project carries its own copy
as well, use one of the two.

**With another agent,** put the text of `PRINCIPLES.md` in the file it reads at the start of every
session (for many agents, `AGENTS.md`), keep `RECORD.md` where it can read it, and say in that file
where `RECORD.md` and the log are.

**Then ask the person** whether any principle plainly does not fit the project, and log the answer.
Pruning is expected over time, as a project learns which principles it needs. A principle set aside
is set aside under *This project's own*, with its reason, rather than deleted from the copy.

## Taking in what they gain

Copy the new files over the old ones. Since the project never edits them, there is nothing to merge,
and `git diff` shows exactly what changed. Read it before committing, as you would a colleague's
proposal rather than a dependency bump: a change to a principle changes how every session works from
then on. Then read *This project's own* against the new text, line by line, as you would your own
code against a shared package's:

- **It now says nothing the principles do not:** delete the project's line. Its log entry stays
  where it is.
- **It says more, and the more would serve any project:** raise the difference here (*Raising a
  lesson*, below), and keep the line until an update brings it in.
- **It says more, but the more is about this project alone:** keep that part.

Log the update if it changed anything about how the project works.

## Raising a lesson

**What to raise.** A lesson, a check or a way of working that would have saved any project the same
cost. Not what is about one project's subject, and not what is about one kind of work: a lesson
about games goes to `ts-game-template`, which keeps the games' cues.

**Write it into the project first,** under *This project's own*, with its log entry. The project
needs it while this repository decides, and a lesson left only in the log is filed where nobody
looks before acting.

**Ask the person before sending anything.** What leaves a project is theirs to decide, and a lesson
they settled for one project may not be one they want stated for every project. This repository is
public. From work done in confidence, nothing that identifies the work goes with a lesson: no
organisation, product, target, dataset or person, and no number or detail that would point to them.
A lesson that cannot be told without them stays in the project.

**Then open an issue,** one per lesson, titled `Lesson:` and the lesson in a sentence, so that
matching lessons from different projects can be found together. Brief it the way principle 8 says to
brief another agent: which project it came from, where that can be said; what happened and what it
cost; which principle it extends, or that none does; what is measured and what is a guess; and its
log entry. You don't need to check whether another project has raised it first: matching issues is
this repository's job.

**What happens to it.** Lessons are triaged, and one is folded in once it clears the bar: it has
come up in more than one project, or it would be expensive to work out again. Most become a sharper
reason, a *Looks like* line or a better example under a principle. Written in, a lesson names no
project, and the person in its example is named by their role, such as *a designer*. Which project
raised it stays in the issue and in the commit that closes it, and every project receives it at its
next update.

## Changing the principles

The person who keeps this repository and an agent change the principles together. Either may propose
adding, rewording or pruning one; the change is made once both have worked it through, and its pull
request records why.

**The shape.** Each principle is a bold line, a trigger and an action written for a kind of problem
(*before you trust a result*), not for one incident (*after a subsystem was switched off*); then its
reason, stated so that it holds for work nobody has done yet, and so that when the principle is
inconvenient the argument starts from the reason rather than from scratch; then *Looks like* lines,
and at most one example. An example is one real scene that shows what the moment looks like. It is
not evidence, so it carries no tally. Ten principles at most: adding one means merging or retiring
another.

**The *Looks like* lines carry behaviour.** In the trial that settled the game template's wording
([`ts-game-template#22`](https://github.com/collagen-collective/ts-game-template/pull/22)), fresh
sessions said what they would do next in fifteen situations from other games, graded blind against
forty-four behaviours. A version that had cut its *Looks like* lines to the hardest few scored 32.3,
against 37.0 for the longer text it replaced and 24.0 for no guidance at all. It had lost eight
behaviours the longer text produced, and sessions with no guidance missed seven of the eight in
every run: agents did not work them out from the principles, or unaided. Putting five lines back
recovered all eight. So before cutting a concrete line, ask whether an agent would work it out from
the principle alone; that trial says it often will not.

**Try a change the same way:** fresh sessions for each arm (the current text, the proposed one, and
none at all), situations the text was not written from, blind grading against the behaviours it
should produce, a planted ideal answer and a planted weak answer as the graders' controls, and
predictions written down before the round runs. Its limit is any trial's: a line shown to be read
and applied in the situations that prompted it is not yet shown to reach situations worded
differently.
