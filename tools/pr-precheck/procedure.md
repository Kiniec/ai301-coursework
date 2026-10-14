# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. Live mode only: read `scope.md` first. Confirm the PR targets the scoped repo and note any house rules. If the `Repo:` line is still a placeholder, stop and say so.
2. Read `rubric.md` and `references/evidence-guide.md`. List the checks and the verdict rule.
3. Read the whole package before grading anything, in this order:
   a. The issue. Note the symptom and what "fixed" would look like.
   b. The plan, with its `## Deviations`. Note the stated cause, the scope, the files it names, what it says it won't touch, and the test plan.
   c. The diff. Start with the file list (`--stat` in live mode), then the hunks. Mark each file as named in the plan, covered by a deviation, or neither.
   d. The test evidence.
   e. The PR title and description.
   f. What the repo asks of a PR. Eval mode: the repo-facts block (template asks, contribution policy, any AI policy). Live mode: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`. Note which checks the repo names and whether it states an AI policy.

   The plan comes before the diff because it's the promise. You can't spot drift until you know what was promised. The description comes last because you read it against both.
4. Live mode: the PR is what's committed on the branch. Get it from `git diff main...HEAD`. Don't count uncommitted files or other files in the working directory. Eval mode: the bundle is the whole world. Fetch nothing and run nothing.

## Evidence gathering

Pull exactly what each check names. Record one quote or fact per check.

1. **diff_matches_plan.** List every changed file. Match each one to the plan's files-to-touch or a deviation. Then list every promised change the diff doesn't contain. Record the unmatched files and the missing promises.
2. **description_matches_diff.** List each claim in Summary and Changes. Find it in the diff. Then list each substantive change in the diff the description doesn't mention. Record the unsupported claims and the unmentioned changes.
3. **repro_before_after.** Pull the repro steps from the plan's test plan. Find the same steps in the test evidence, once for before and once for after. Record the before result, the after result, and whether the steps match.
4. **repo_checks_run.** Take the list of checks from step 3f. The repo's own wording decides what's on it, so don't assume `make` targets or any tool. Find each one's output or stated result in the test evidence. Record which have output, which don't, and the reason for any failure. If the repo names no checks, record whether the test evidence shows the repo's own test suite result.
5. **diff_clean.** Scan the hunks for debug prints, commented-out code, unrelated edits, and stray files like `plan.md`, `comment.md`, `pr_draft.md`, or `test_evidence.md`. Record each with its file. Check whether the description discloses it.
6. **template_and_disclosure.** Compare the description's sections to the ones the repo's template asks for. Record any section that's empty or skipped, whether the issue is referenced, which boxes are ticked and whether the evidence supports each one, and where any AI-use disclosure sits. Record whether the repo states an AI policy. If it has no template or no AI policy, record that ask as absent.
7. **title_and_branch.** Live mode only. Pull the branch name and PR title. Record the prefix, the issue number, and what the title says. Eval mode: skip it. The bundle holds no branch name.

Live mode: if a fact lives in a file or page the evidence guide names, read it there. Eval mode: quote the bundle's lines.

## Check execution

1. Run the checks in the rubric's table order. In eval mode, skip `title_and_branch` and leave it out of the output.
2. Grade each one `pass`, `fail`, or `unclear`. Add a one-line quote or fact that decided it.
3. `unclear` means the package doesn't hold the evidence. It doesn't mean you didn't look. Grade it `unclear` and say what's missing. Example: the description claims tests passed and the test evidence is empty.
4. Check disclosure before you fail a gap or a deviation. If the plan's `## Deviations` and the description both state it, don't fail it. If it's only in one, or only in the diff, fail it.
5. Fail an ask only if the repo makes it. If the repo has no template, no named checks, or no AI policy, don't fail the PR for missing what doesn't exist.
6. A check may be graded without re-reading the whole package if the evidence you gathered covers its pass condition.
7. The rubric decides. If a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary.
8. Grade the PR itself, not its polish or length.
9. If the procedure doesn't tell you where to find something, name the gap in the summary. Don't invent a step.

## Verdict assembly

1. Apply the rubric's verdict rule to the grades. Accept only if every `required` check passes.
2. A `required` check graded `unclear` counts as `fail`.
3. `preferred` checks never change the verdict. Mention them in the summary.
4. The result is `accept` or `reject`. Never a third option.
5. If the verdict is `reject`, quote the first failing `required` check in rubric order as the deciding check. Put its evidence line first in the summary.
6. Then write the summary. One line per check. Voice-guide notes (live mode only). Procedure gaps.
7. End the reply with the JSON block from `SKILL.md`. It's valid and last, with nothing after it.