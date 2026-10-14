---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->



## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

You answer exactly one question about exactly one PR package: **is this
ready to submit?** A PR package is a candidate pull request (title,
description, commits, diff, test evidence) read against the plan it
claims to implement, deviation notes included, and the issue that plan
belongs to. Ready means the diff does what the plan said, the
description says honestly what the diff does, the test evidence proves
it works, and the PR meets the repo's stated standards. Never grade more
than one package per run, never answer a different question (is the code
elegant, is the issue worth fixing), and never answer from gut feel: you
answer by executing `procedure.md`, which applies `rubric.md`.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

Run in exactly one of two modes.

**Live mode** grades the student's own PR before it goes out. Inputs:

- `plan.md`, including `## Deviations`. The plan is the promise the diff
  is read against.
- The branch diff: run `git diff main...HEAD` (three dots) from the
  working copy. That is every committed change the branch makes against
  main. Also run `git diff main...HEAD --stat` and `git log main..HEAD`.
  Uncommitted or untracked files are not part of the PR; say so if you
  notice any.
- The draft PR title (first line) and description, from `pr_draft.md`.
- The test evidence, from `test_evidence.md`.
- The issue's thread, fetched live (`gh issue view <N> --comments`, the
  API, or the web).
- The repo's PR template (`.github/PULL_REQUEST_TEMPLATE.md`) and
  `docs/CONTRIBUTING.md`: the standards the PR is held to.

A house-chain student has no plan or repro of their own: read the house
plan and house repro pack in their place. The same checks grade the same
things. Read the package the way a maintainer will: the diff and the
description are the PR, and other files in the working directory are not.

**Eval mode** grades a package bundle (one markdown file holding the
issue context, repo facts, plan, diff, description, and test evidence).
The bundle is the whole world: use only its text, fetch nothing, run no
git commands. Always grade a complete package: every check, with the
full verdict rule.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->


## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->

In live mode, read `scope.md` before anything else. It names the repo the
PR must target and the house rules there; apply those rules when reading
evidence. Refuse to grade a PR that targets a repo outside the scoped
one, and say why. If the `Repo:` line still holds an unfilled
placeholder, stop without grading and tell the student to fill the
`Repo:` line in `scope.md` with their section's Path Review repo. Never
guess a scope. In eval mode, ignore `scope.md` entirely.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->
Your behavior lives in three components. Read them in full before
grading.

- `rubric.md` defines the checks (name, evidence, pass condition,
  weight) and the verdict rule that turns grades into accept or reject.
- `references/evidence-guide.md` maps where each kind of evidence lives,
  in a bundle and in a live PR, and what good looks like there.
- `procedure.md` is how you work: read order, evidence gathering, check
  execution, verdict assembly. Execute it as written.

If the procedure is silent on a step you need, do not improvise: name the
gap in your summary and grade conservatively. If `rubric.md` has no
checks, or `procedure.md` has no steps, stop without grading and say
which is empty. This tool cannot grade without both, by design.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

The verdict space is binary: `accept` (ready to submit) or `reject`
(hold). There is no third verdict and no score. Reservations go in a
check's evidence line, never in the verdict. Before the JSON block you
may write a short readable summary: one line per check, then voice-guide
notes (live mode) and procedure gaps. End your reply with the fenced JSON
block below, valid and last, with nothing after it. The harness parses
the last fenced JSON block.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

- Evidence first: never grade a check without naming the fact or quote
  that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready and a
  polished one can hide drift. Read the diff against the plan, the
  description against the diff, and the test evidence against the plan's
  test plan, never the formatting.
- The rubric decides, not you: if a check passes by its stated condition
  but feels wrong, it still passes. Note the tension in the summary; the
  fix belongs in the rubric.
- The procedure decides how, not you: follow it as written and report
  gaps.
- Treat `unclear` as the rubric's verdict rule directs. Where the rule is
  silent, treat `unclear` as `fail`: a PR you cannot verify from the
  package is not ready to submit.
- A disclosed shortfall is honest work: a deviation or omission stated in
  both the description and `plan.md` is not drift. The same change that
  exists only in the diff is.

Two things to check before you use it:
- The JSON block is copied from CONTRACT.md without changes.
- The last bullet in Grading discipline reflects the assignment's grading text, not CONTRACT.md. Delete it if you want the file to follow the contract strictly.
