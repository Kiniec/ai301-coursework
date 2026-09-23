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

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

**Verdict output**

 [Your skill's live-mode output for this issue, pasted verbatim and ending with the fenced JSON verdict block. A summary does not satisfy this field.] 

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

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

1st run - 17/20 \
2nd run - 12/20 \
3rd run - 14/20 \
4th run - 16/20 \
5th run - 18/20 \
6th run - 18/20 


**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

One scored was issue-01. The rubric's decision was accept, gold label as accept, the reasoning the rubric produced the result was it is an active repo as well as unclaimed.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

After running a canary with Issue-06, it required a change because of the contributing md. Changing  was the only way it would pass the test.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's of fixing a bug and an api fits my interests and to the time available.
2. The verdict weighed everything accordingly.
3. The anticipated difficulty and challenge,  I believe,  will be the api portion of the issue. 

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
