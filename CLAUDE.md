# Personal preferences

## Line length

- **Don't churn lines to satisfy line length.** Line length is enforced almost nowhere in my codebases (some Python libraries excepted), so a long new line is fine. Never reflow or re-wrap existing lines to make room for an edit or to tidy up. Where a limit is genuinely enforced, break only the offending line, even if that leaves some very short lines, rather than touching neighboring lines to make it look even.
- **Never hard-wrap prose in Markdown files.** Hard wraps often break syntax highlighting. Write each paragraph or list item as one line. Wrap only where a line break is meaningful, e.g. inside a code block.

## Python environments

- **NEVER create a Python environment without asking me first.** This
  covers `conda create` / `conda env create`, `mamba create`,
  `python -m venv`, `conda install`, and `pip install` into any
  environment (including `--user`). Encountering an `environment.yml`
  or `requirements.txt` is not permission to build it — read it as
  "the env this expects", then ask. This also applies to what you tell
  subagents: a dispatch prompt saying "in the conda env from
  `environment.yml`" reads as permission to create it, so don't write
  it that way.

- **Don't survey my environments either — just ask.** No listing the
  conda-envs directory, no probing candidate interpreters to see what
  imports, no inferring from an `environment.yml` which existing env
  might satisfy it. If you need a Python environment and don't already
  have a confirmed answer for which one, your first move is a question
  to me, not investigation.

## Messages to me

I do not read messages from turns I didn't prompt — task notifications, subagent
completions, loop or cron ticks, hook-triggered turns, scheduled runs. Between those, say
little or nothing; the tool results carry the record. **Nothing can be deferred to a later
message, and nothing said in an unprompted turn has been delivered.**

**A dispatch is not a stopping point.** While any background work is in flight — a
subagent, a build, a long run — the turn is not finished, whatever the tooling says about
replying in the meantime. Write no substantive message until everything has come back: the
results land in a turn I don't read, so reporting early guarantees I get half the story,
and the half I get is the half that matters least. If something truly cannot wait, stop the
background work first and say that you stopped it.

Write your final message, once all work including background work is done, as if it is the
only one I will see, because it is. It carries:

- **Decisions you made without asking**, especially deviations from an approved plan or
  spec, and what they cost if they turn out wrong.
- **Corrections** to anything you told me earlier that would change my conclusions.
- **Commands I have to run**, and anything blocking.
- **Anything else important that the diff cannot tell me.**
- **Questions, numbered, at the bottom** — so I can answer "1. yes, 2. ..." without
  quoting. If you say there are questions, there must be questions.

**Never ask whether to move on from the thing you are asking me about.** If you have
questions about a piece of work, "approve this and start the next one?" is not one of
them: my answers may well change that work, so asking me to greenlight the next step in
the same breath asks me to approve something you have just told me might change. Ask the
substantive questions, and let my answers decide whether it is finished. This holds for
every phrasing of it — "shall I proceed", "ready for the next task", "anything else
before I continue".

It does **not** carry an account of what changed. I read the diffs myself. No
file-and-hunk inventories, no "summary of what landed", and no roll-call of checks that
passed — "I verified X, Y and Z" is a diff summary with a different verb. Report a check
only when it failed or when it changed a decision. Name a file only when naming it is
load-bearing for the point.

**Say only what I don't already know**, including from earlier in the same exchange. The
tell is a paragraph that re-states the reasoning behind a decision I have already
approved, however interesting that reasoning was the first time.

**State a finding as a sentence about behavior first**, then the evidence, then the
file:line. I know my own codebases; what I can't do is reconstruct your investigation from
a bare symbol name. Cut findings that don't change what I decide — brevity comes from
dropping items, not from compressing explanations into jargon.

## Commit messages

Commit messages are summaries, not documentation. **Cap the body at 200 words** (headline
and trailers don't count). If it takes more, the extra belongs somewhere else.

- **Never restate what a code comment already says.** Before writing a paragraph
  explaining a mechanism, check whether the explanation lives at the site. If it does, the
  message says only that the change happened. If it doesn't, write the comment — don't
  compensate in the log.
- **No derivations, algebra, or worked arithmetic.** A message that shows its work is a
  comment in the wrong file.
- **No unsourced numbers.** Figures in a message are permanent and read as established.
  If a number rests on an assumption with no citation, leave it out or say plainly that
  it is provisional and where it's tracked.
- **No development history.** Not "second review round", not what an earlier version of
  the change did, not which commits got squashed into this one.

Cover: what changed and why; deliberate divergences from a reference implementation or an
upstream convention; anything a future bisect would need. State verification status
honestly — including "not compiled, built or run" when that's the case.

Wrap the body at 72 columns.

## No ready-to-paste prose for humans

Don't write prose I could copy-paste to another person. When I need to produce
something for human readers, give bullet points (fragments, not full sentences)
covering the main ideas, and I'll write the actual text.

Applies to:
- Emails, messages, and other communication
- PR descriptions (writing them up is how I confirm I understand my own change)
- Standalone docs (READMEs, design docs, etc.)

Does not apply to (write these fully as normal):
- Commit messages
- Code comments and docstrings
- Error messages, log strings, CLI help text, and other text embedded in code

Rules:
- Bullets are incomplete sentences. Use a short full sentence only when no
  fragment can be unambiguous.
- Assume I'm the only audience. Don't tailor bullets to the eventual reader's
  tone or expectations; I'll handle that.
- Don't add extras (suggested structure, things I might forget, tone notes).
- Only write full prose when I explicitly ask for a draft or full text.

