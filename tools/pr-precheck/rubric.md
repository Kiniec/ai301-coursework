# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks
| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diff_matches_plan | The diff's changed files and hunks, read against the plan's scope, files-to-touch, and `## Deviations`. | Every changed file and hunk traces to the plan or a recorded deviation. Nothing the plan promised is missing without a note. A change that's only in the diff fails. So does an undisclosed gap. A change or shortfall recorded in Deviations and the description passes. | required |
| description_matches_diff | The Summary and Changes bullets, read against the diff. | Every claim is visible in the diff. Every substantive change in the diff is mentioned. If the description claims more than the diff does, or says it follows the plan when the diff doesn't, it fails. | required |
| repro_before_after | The test evidence, read against the plan's test plan and the repro steps. | The original repro steps are re-run. A concrete before result and a concrete after result (output, error, or exit code) are shown, and the diff could plausibly produce the change. "Works now" with no output fails. | required |
| repo_checks_run | The test evidence, read against the checks the repo names. Eval mode: the repo-facts block (PR template asks and contributing guide). Live mode: the PR template and `docs/CONTRIBUTING.md`. | Every check the repo names has real pasted output or a stated result, like "312 passed" or "fmt and clippy clean". A failing check passes this test if the output is shown and the reason is stated. So does an expected stop like "no tests ran". A check the repo names that's missing from the evidence fails. A ticked box with nothing behind it fails. If the repo names no checks, a stated result from its own test suite passes. | required |
| diff_clean | The full diff and the file list. Look for debug lines, commented-out code, unrelated edits, and stray files like `plan.md` or `pr_draft.md`. | The diff holds only the change the plan describes. Any debris or unrelated hunk fails unless the description discloses it. Debris that buries the real change fails either way. | required |
| template_and_disclosure | The description, read against what the repo asks. Eval mode: the repo-facts block (template asks, contribution policy, any AI policy). Live mode: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`. | Every section the repo's template asks for is filled with real content, not boilerplate. The issue is referenced. Only boxes the evidence supports are ticked. An AI-use disclosure is present if the repo states an AI policy. If the repo has no template or no AI policy, that ask doesn't exist: don't fail the PR for missing it. A skipped template section, an unsupported tick, a missing issue reference, or a missing disclosure the repo asks for fails. | required |
| title_and_branch | Live mode only: the branch name and PR title. Eval mode: skip. The bundle holds no branch name. | The branch has a type prefix, the issue number, and a short description, like `fix/1234-null-check`. The title says what the change does. | preferred |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if every `required` check passes. A `required` check that fails or is `unclear` means reject. `unclear` counts as `fail`, because a PR you can't verify isn't ready to submit. `preferred` checks never change the verdict. Note them in the evidence lines. In eval mode, don't grade `title_and_branch`, and leave it out of the JSON.

Judge outcomes, not shape. A short PR that meets every pass condition is ready. An honestly disclosed shortfall doesn't hold a PR on its own.
