# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

[Link to the pull request you opened. It must be the pull request's own page on the Path
Review repo, not your fork's branch page.]

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/227

**Branch**

[The name of the branch the pull request comes from, exactly as it appears in your fork.
The naming shape is a type prefix, then the issue number, then a short description. **The
issue number in the branch name must be the number of the issue the pull request fixes** —
a name carrying any other number does not satisfy this field.]

fix/72-verify-password-unknown-hash

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

agreement: 17/20 scored items  (bar: 18/20: below the bar) 1st run.
agreement: 20/20 scored items  (bar: 18/20: PASS) 2nd run.

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

pkg-01 (standards-wall, pandas-dev/pandas#66657)

- gold label: reject
- my rubric: reject
- agree: yes

The repo-facts block says the PR template "is a required checklist: closes #xxxx with the issue number, tests added and passed, all code checks passed (pre-commit), type annotations added to new arguments, and an entry in the latest doc/source/whatsnew/vX.X.X.rst when fixing a bug."

The code and tests are fine. The description never names issue #66657, and the PR has no whatsnew entry and no pre-commit result.

My rubric rejected it on those gaps. `template_and_disclosure` says "A skipped template section, an unsupported tick, a missing issue reference, or a missing disclosure the repo asks for fails." `repo_checks_run` says "A check the repo names that's missing from the evidence fails."


**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/pr-precheck/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

`template_and_disclosure`, as it reads in `tools/pr-precheck/rubric.md`:

> | template_and_disclosure | The description, read against what the repo asks. Eval mode: the repo-facts block (template asks, contribution policy, any AI policy). Live mode: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`. | Every section the repo's template asks for is filled with real content, not boilerplate. The issue is referenced. Only boxes the evidence supports are ticked. An AI-use disclosure is present if the repo states an AI policy. If the repo has no template or no AI policy, that ask doesn't exist: don't fail the PR for missing it. A skipped template section, an unsupported tick, a missing issue reference, or a missing disclosure the repo asks for fails. | required |

In my first run this check failed pkg-02, pkg-05 and pkg-08, all clear-accepts. It was failing them on asks their repos don't make: none of the three states an AI policy. I changed it so each ask applies only when the repo makes it. The failure conditions stay, so pkg-01 and pkg-20 still fail.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

Making `template_and_disclosure` and `repo_checks_run` repo-neutral fixed pkg-02, pkg-05 and pkg-08, and my second run agreed on all 20.

The cost is that both checks can only fail an ask written in the repo-facts block. If a repo has a rule that block doesn't capture, my rubric will miss it. `title_and_branch` is skipped in eval mode because bundles have no branch name, so the eval never tests it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
