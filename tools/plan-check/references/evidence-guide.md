# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

- Where it lives: The plan's Cause: line, read against the repro evidence's Steps and Actual lines. Live mode: the Cause in plan.md and your posted unit 2 repro comment.
- Good looks like: The cause names a specific mechanism that explains the exact symptom in the repro evidence (in calib-01, step 3 versus step 4). It doesn't treat the symptom itself as the cause, and it doesn't contradict a repro step.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

- Where it lives: The plan's Change: line, specifically its In and Out clauses and the named files.
- Good looks like: One change to the diagnosed cause, in the named files, with an explicit Out line (calib-01 has one). A drive-by rewrite touches files or behavior the cause doesn't explain.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

- Where it lives: The Change: line, which holds the file path, function, and action. Live mode: files touched and approach in plan.md.
- Good looks like: A stranger could open the named file and function and know what to edit without asking. Vague phrases like "fix the refresh logic" fail.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

- Where it lives: The Test: line, read against the repro evidence's Steps and Expected.
- Good looks like: It re-runs the repro steps and names the observable result at a specific step (calib-01: "at step 3 the color must flip"). It also covers any related paths the plan itself says share the code.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

- Where it lives: Hedges and unknowns in the plan and comment. Live mode: the risks and unknowns section and the ## Deviations heading at the end.
- Good looks like: Claims the repro evidence can't prove are flagged as unverified. A plan that states an untested cause as fact, or that lists no unknowns at all, reads as false confidence.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->


- Where it lives: The plan comment, read against Repo facts (bug template, contribution policy, AI-disclosure line) and Thread highlights.
- Good looks like: It refers to something specific in this thread or repo (calib-01 cites the review-bandwidth note), follows any stated policy, and doesn't promise more than the plan contains. "Same approach as above" fails.