# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

**Where it lives**
- Eval bundle: the **Plan context** section holds the repro evidence, the plan's steps, "Not in scope", the files list and the test plan. The **Diff** and **Commits** under **Candidate PR** show what changed. The **Description** holds the claims.
- Live mode: `plan.md` (scope, files, `## Deviations`) in the top folder of your clone. The diff comes from `git diff main...HEAD` (and `--stat` for the file list). The claims come from `pr_draft.md` (Summary and Changes).

**What good looks like**
- Every changed file and hunk falls inside the plan's files and scope, or a deviation note covers it.
- Nothing the plan promised is missing without a note.
- Every claim in the description is visible in the diff.
- Drift runs both ways: more than the plan, or less with no note. A description that claims more or less than the diff delivers is drift too.
- A deviation stated in the plan and the description re-ties a mismatch. A mismatch that's only in the diff doesn't.

## Test evidence (harness category: not-tested)

**Where it lives**
- Eval bundle: **Test evidence** under **Candidate PR**. Read it against the plan's test plan and the repro steps in **Plan context**. The checks the repo names are in **Repo facts** (PR template asks and contribution policy). They differ by repo: `cargo test` and clippy, `go test ./...`, `pytest`, and so on.
- Live mode: `test_evidence.md`, read against the test plan in `plan.md` and your unit 2 repro steps. The checks come from `.github/PULL_REQUEST_TEMPLATE.md`. For Path Review that's `make test-unit`, `make test-integration`, `make lint` and `make typecheck`.

**What good looks like**
- The original repro steps are re-run, with a concrete before result and a concrete after result (output, error or exit code).
- Every check the repo names has pasted output or a stated result, like "1462 passed" or "fmt and clippy clean".
- A failing check with its output shown and the reason stated counts as evidence. So does an expected stop like "no tests ran" from `make test-integration`.
- If the repo names no checks, a stated result from its own test suite is enough.
- "Tests pass" or "works now" with no output doesn't count. Neither does a ticked box with nothing behind it.

## Diff quality (harness category: unreviewable)

**Where it lives**
- Eval bundle: **Diff** and **Commits** under **Candidate PR**.
- Live mode: `git diff main...HEAD`, `git diff main...HEAD --stat`, and `git log main..HEAD`.

**What good looks like**
- The fix is visible, and nothing unrelated rides along.
- Debris tells: debug prints, commented-out code, dead code, formatting churn, drive-by edits, and stray files like `plan.md`, `comment.md`, `pr_draft.md` or `test_evidence.md`.
- In live mode, `--stat` should list only the files your fix changes.
- Debris the description discloses is still a note, but debris that buries the real change fails either way.

## Standards and comms (harness category: standards-wall)

**Where it lives**
- Eval bundle: **Repo facts** states the PR template asks, the contribution docs and any AI policy. **Thread highlights** shows direction from maintainers. The **Title** and **Description** under **Candidate PR** show how the PR answers them.
- Live mode: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` in your Path Review repo, and the issue thread. Your answers are in `pr_draft.md`. Your branch name comes from `git branch`.

**What good looks like**
- Every section the repo's template asks for is filled with real content, not boilerplate. Read the repo's own section names: "Description", "Type of changes", "User-facing changes", a requirements checklist, a changelog entry.
- The issue is referenced. Live mode with Path Review: `Closes #N`.
- Only boxes the evidence supports are ticked. CI stays unticked until the PR is open.
- An AI-use disclosure is present if the repo states an AI policy. Live mode with Path Review: Notes for Reviewers.
- Maintainer direction in the thread is engaged, not ignored.
- A repo with no template, no named checks or no AI policy has nothing to fail on that point. Don't invent asks the repo doesn't make.
- Live mode only: the branch has a type prefix, the issue number and a short description, like `fix/1234-null-check`. Eval bundles have no branch name, so skip it there.
- Boilerplate, empty sections or a visibly ignored ask fail.
- Whether the claims match the diff belongs under plan fidelity, not here.
