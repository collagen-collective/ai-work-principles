# In Claude Code

`PRINCIPLES.md` is written for any agent. This is what is particular to Claude Code, learned the
same way, by paying for it, and checked against Claude Code's documentation in October 2026. Where
something is what one project observed rather than what the documentation says, it says so.

## Where the principles go

The principles only help if they are re-read. A designer, choosing where they should live: *"The
principles only work if you can remind yourself to slow down and think things through, so I think
the frequency with which CLAUDE.md is re-read makes it the proper candidate."*

- **Files in `.claude/rules/` load like `CLAUDE.md`.** A rule file without `paths:` front matter
  loads at the start of every session, with the same priority as `.claude/CLAUDE.md`, and comes back
  from disk after the context is compacted. A file that `CLAUDE.md` imports with `@path` loads at
  the start too, but the documentation does not say that an import comes back after compaction, so
  the rules folder is the safer home for anything that has to stay in mind for a whole session.
- **Rules in `~/.claude/rules/` load in every project on the machine**, and commit nothing to any of
  them. Where a project carries its own copy of the principles as well, keep one of the two: Claude
  may follow either of two instructions that disagree, and two copies drift apart.
- **Sub-agents start with the session's `CLAUDE.md` files and rules**, so a brief does not need to
  repeat the principles. The built-in Explore and Plan agents skip them, as does an agent defined
  with `omitClaudeMd: true`: if a principle must reach one of those, put it in the brief. It is also
  why a trial of guidance runs each arm as a fresh session rather than a sub-agent (the README's
  *Changing the principles*).

## Calls that wait for the person

In one game's day of 38 sub-agents in auto mode, every Bash call that stopped for the person's
approval had changed code and run it in a single call: a heredoc and then Python, `sed -i` and then
`bash`, a wrapper made with `printf` and `chmod +x` and then run. Each ask held its agent, and any
stage waiting on it, until the person came back, some of them for hours. A later run, briefed to
keep the two apart, made over a thousand calls and asked nothing. That is strong evidence rather
than a controlled test, and the documentation does not describe the behaviour. So, in the session
and in every brief:

- Write a script with the Write tool, and run it in a call of its own.
- Change source with Edit, and undo with git.

An allow list does not fix it: replayed against those calls, a list of the agents' routine commands
would have passed none of them.

## An allow rule allows every flag its command takes

A `*` in a Bash rule matches any text, spaces included, so read a command's flags before you list
it.

- `git diff`, `git log` and `git show` take `--output=<file>`, which writes wherever it is told,
  `.claude/settings.json` included. A deny rule, `Bash(git * --output*)`, refuses it. It also
  refuses any git command whose text contains ` --output`, a commit message among them, and
  `git commit -F <file>` gets round that.
- Leave `git apply` off a list, since a patch can rewrite any file in the checkout, and `git grep`,
  whose `-O` runs any program it is given.
- A rule for a test runner, the build, lint or a script runner runs code from the checkout, so an
  agent that has written code there can have it run without review.
- A project's allow rules apply only once its folder has been trusted; its deny and ask rules apply
  at once.

## Sub-agents in parallel

Principle 8's last *Looks like* line, in Claude Code's terms:

- **A sub-agent's worktree is cut from the default branch,** not from the branch the session is on,
  unless `worktree.baseRef` is set to `"head"` in settings. So a sub-agent can start from code the
  session has long since moved past: have each check that its worktree holds your latest commit
  before it starts. *A builder in one game measured code that was no longer there.*
- **Each sub-agent running a browser wants about two cores.** Past what the machine can carry, every
  capture slows, tests fail on their time limits, and the batch finishes later than smaller batches
  would have.
- **A container restart takes uncommitted work with it.** Have each sub-agent commit as it goes, on
  a branch of its own.

## Raising a lesson from a cloud session

To open an issue on another repository, this one included, add that repository to the session so
that the GitHub tools can reach it, and stop there: an issue needs no clone. In one session,
attaching, cloning and registering a repository moved the session's working directory out of the
project, and from the next restart the project's hooks and settings stopped loading, for the session
and every agent it started, with nothing to say so. Afterwards, and after any restart, check that
the session's primary working directory is still the project.

## Skills

When the same tool has been built twice, make it a skill: `.claude/skills/<name>/SKILL.md`, whose
`description` says what it does and when to use it, since that is how Claude decides to load it.
Then try it on a planted defect, with it and without it. Plant the defect in a commit with no
parent, so that no history gives it away, and compare the time taken as well as the verdicts. A
skill can make an agent faster, or make it trust a wrong answer sooner, and only the trial shows
which: *one skill found a planted defect in about half the time, and on a case it was blind to it
was slower than no skill at all, because the agent believed it first.* What the agents without it
build for themselves is what the skill was missing, and a skill's *nothing wrong* is a claim to
check like any other.
