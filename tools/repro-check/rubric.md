# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment_recorded| Repro report's Environment: line, read against the Repo | Names concrete tool version + runtime/OS; if the tested version differs from the issue's stated/latest target, the report says so explicitly | required |
| steps_followable | Repro report's Steps list, read against the Issue's own stated reproduction steps| Every step is a literal command/snippet from a named starting state to the issue's exact trigger - no paraphrased setup, no substituted or simplified input   |required 
|behavior_matches_issue | Pasted output/error/log inside the repro report's steps, read against the Issue's stated actual/current result | The artifact's own text (error message, exit code, log line) shows the exact symptom the issue describes, not an adjacent or milder failure | required 
|claim_backed_by_evidence | The repro report's stated conclusion (reproduced / cannot reproduce), read against the artifacts pasted in that same report | Every reproduced-or-not claim is backed by an artifact in the report; an honest cannot-reproduce that names what differed passes,confident language with no matching artifact fails | required
|claim_comment_specific |Candidate claim comment, read against the Issue section |Names a detail specific to this issue (a symptom, a version, a step, a next question) rather than boilerplate that would read the same on any issue | required
ai_disclosure_compliant | Repo facts block's contribution-policy line, read against the claim and repro comment text | If the stated policy requires disclosing AI assistance, the comment discloses it in its own words; if the policy has no such requirement, this passes by default | required
 promises_investigation_only |  Candidate claim comment | Comment promises investigation/next steps only — no fix, no timeline, no date | preferred



## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept if every required check passes. Any required check failing or unclear holds the package as reject. preferred checks never change the verdict — they're informational only. unclear on any check is treated the same as fail: evidence you can't verify isn't evidence the package is ready to post.