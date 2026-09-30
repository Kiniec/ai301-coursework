# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->
Where it lives: in an eval bundle, the `Environment:` line at the top
  of the **Candidate repro report** (e.g. "Environment: HTTPie 3.2.4
  (pip), Python 3.12.4, multidict 6.6.0, macOS 14.5 (arm64)"). Read it
  against the **Repo facts** block's `latest release` line and any
  version named in the **Issue** section. In live mode: the equivalent
  line in the student's draft repro report file, read against the
  version stated in the issue thread and the repo's actual latest
  release (GitHub releases page).
- What good looks like: the line names concrete, checkable facts (tool
  version, language/runtime version, OS and architecture) — enough to
  place the run, not "recent version" or "my machine." If the version
  used differs from what the issue targets or from the repo's current
  latest release, the report names that difference explicitly rather
  than letting it pass in silence (pkg-01 and pkg-07 both run a newer
  version than the issue was filed against and say so; pkg-16 runs an
  old, already-superseded version against an issue confirmed on latest
  and does not flag the gap — that silent deviation is what fails it).

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->
 Where it lives: the **Steps** list inside the **Candidate repro
  report** (numbered actions, exact commands or code snippets, any
  control/comparison run), read against the **Issue** section's own
  stated repro steps or minimal reproduction code. In live mode: the
  draft repro report's steps, read against the issue body's steps and
  any trigger condition named in the thread.
- What good looks like: every step is a literal, paste-able command,
  code snippet, or concrete UI action — never a paraphrase like "set up
  the project" or "install dependencies" with no commands shown. The
  starting state is named (fresh install, specific config, specific
  input) and the trigger matches the one the issue names, not a
  substituted or simplified stand-in (calib-03 swaps an `=` for a `:`
  in the input and calib-08... pkg-08 unbinds a variable instead of
  using the issue's exact expression — both produce a different,
  milder failure than the one reported, because the step that should
  trigger the bug was quietly changed).

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->
 Where it lives: the output blocks pasted inside the **Candidate
  repro report**'s steps (terminal output, console error, log excerpt,
  screenshot description), read against the **Issue** section's stated
  "current/actual result" or described error text. In live mode: the
  pasted artifact in the draft repro report, read against the issue
  body's description and any narrowing detail from the thread.
- What good looks like: the artifact's own text — the exact error
  message, exit code, or log line — matches the symptom the issue
  describes, not a nearby or milder failure that the write-up narrates
  as a match. A control run (the same steps without the trigger, or on
  a known-good input) strengthens the read when present. Judge the
  artifact itself, not the writer's confidence about it (pkg-02
  narrates a graceful arg-validation error, exit 1, as the issue's
  reported capacity-overflow crash, exit 101; pkg-08 narrates a compile
  error from an unbound variable as the issue's runtime "Invalid path
  expression" — in both, the pasted text itself is the tell, regardless
  of how certain the surrounding prose sounds).


## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->
Where it lives: cross-read the **Candidate claim comment** and the
  **Candidate repro report**'s stated "expected"/"actual" or
  conclusion against the artifacts pasted in that same report. In live
  mode: the same cross-read within the student's own draft files —
  does the confidence in the prose match what the pasted output
  actually shows?
- What good looks like: an honest cannot-reproduce is a pass, not a
  fail, when it names the specific difference or step that didn't
  trigger the bug and, ideally, a hypothesis for what would (pkg-09 and
  pkg-10 both fail to reproduce and are accepts, because they show a
  real attempt and name exactly what differed). Confident language
  ("guaranteed reproducible," "I verified this race condition") is not
  itself evidence and fails this check when no artifact in the report
  backs it (pkg-13 and pkg-15 assert certainty with zero pasted
  evidence). Judge whether the claim is backed by an artifact in the
  same report, never the tone it's delivered in.
## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->
Where it lives: the **Candidate claim comment** text, read against
  the **Issue** section (does it name something specific to this
  issue?) and the **Repo facts** block's `contribution policy` line
  (does the repo's stated policy require AI-use disclosure, and if so
  does the comment disclose it in its own words?). In live mode: the
  draft claim/repro comment, read against the issue thread, the repo's
  actual CONTRIBUTING.md / bug-report template / AI-usage policy
  fetched live, `scope.md`'s house rules, and the student's own
  `voice-guide.md`.
- What good looks like: the comment names a detail specific to this
  issue (a symptom, a version, a step, a next question) rather than
  interchangeable boilerplate that would read the same on any issue
  (pkg-19 fails on an assign-me comment promising a guaranteed two-day
  fix — specific but in the wrong way: it promises an outcome, not an
  investigation). When the repo's policy requires disclosing AI
  assistance, the comment discloses it plainly in the comment itself,
  not just in spirit (pkg-07 and pkg-20 have reproductions of similar
  quality; disclosure is the only difference between the accept and
  the reject). A claim comment promises investigation and next steps
  only — never a fix, a timeline, or a date.