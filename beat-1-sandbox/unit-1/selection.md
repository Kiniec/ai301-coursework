# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72


**Verdict output**

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```

  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
    "checks": [
      {"name": "maintainer_active", "grade": "pass", "evidence": "last commit 2026-09-16, 7 days before today (2026-09-23), within 90 days"},
      {"name": "repo_in_use", "grade": "pass", "evidence": "archived: no; last push 2026-09-16, 7 days before today, within 365 days"},
      {"name": "issue_scope_small", "grade": "pass", "evidence": "names two specific files (core/security.py, tests/unit/test_security.py), estimated effort 1-2 hours, no rewrite/redesign language"},
      {"name": "not_claimed", "grade": "pass", "evidence": "no linked open PR in timeline; student claim comment does not block per Path Review house rule"},
      {"name": "allows_ai_contributions", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI-generated-code restriction"}
    ],
    "verdict": "accept"
  },
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1st run - 17/20 \
2nd run - 12/20 \
3rd run - 14/20 \
4th run - 16/20 \
5th run - 18/20 \
6th run - 18/20 


**Issue analysis**

One scored was issue-01. The rubric's decision was accept, gold label as accept, the reasoning the rubric produced the result was it is an active repo as well as unclaimed.

**Check rationale**

`not_claimed` (required). Pass condition: "No linked open PR (unchanged), AND no
assignee, AND no claim comment ("I'll take this", "can I work on this", "working
on this") posted within the last 60 days that the claimant did not later withdraw.
A claim a maintainer answered counts as active at any age."

My first version only checked for a linked open PR, so it passed issues that were
already assigned or claimed in a comment. I added assignees and claim comments,
and a 60-day window so an abandoned claim does not block an issue.

**Trade-offs**

After running a canary with Issue-06, it required a change because of the contributing md. Changing  was the only way it would pass the test.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Issue #72 is a small bug fix in `core/security.py` and
   `tests/unit/test_security.py`, estimated at 1-2 hours, which fits my time.
   The issue matches my interest for backend development.
2. All five checks passed: last commit 2026-09-16, repo not archived, scope named
   two files, no linked open PR, and no AI restriction in `docs/CONTRIBUTING.md`.
3. I expect the hardest part to be utilizing Claude Code to find the issue.
---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
