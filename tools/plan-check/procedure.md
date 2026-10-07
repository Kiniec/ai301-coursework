# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. Read scope.md (live mode only). Confirm the issue is in the scoped repo and note any house rules. Stop if the Repo: line is still a placeholder.
2. Read rubric.md and references/evidence-guide.md. List the checks and the verdict rule.
3. Read the whole package before grading, in this order:
   a. The issue.
   b. The repro evidence. Note the exact symptom and the steps that trigger it.
   c. plan.md: the diagnosis, scope, files, approach, test plan, and unknowns.
   d. comment.md.

   Reading the repro first lets you judge whether the plan's cause fits it.
4. In live mode, read only what the drafts contain and quote. Don't use other files in the working directory.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

1. For each check, pull exactly the evidence the rubric names.
   - Diagnosis: the plan's stated cause and the repro evidence it quotes.
   - Scope: the scope statement and files list.
   - Test plan: its steps and expected results, set against the original repro steps.
   - Comment: the thread highlights and the repo's conventions.
2. Live mode: gather the issue-side facts from the places the evidence guide names. Eval mode: quote the lines from the bundle and fetch nothing.
3. Record one quote or fact per check.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Run the checks in table order.
2. Grade each one pass, fail, or unclear, with a one-line quote or fact.
3. unclear means the evidence is absent from the package, not that you didn't look. If it's absent, grade unclear and say what's missing.
4. The rubric decides. If a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary.
5. Grade the plan itself, not its polish or length.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

Apply the rubric's verdict rule to the grades. The result is accept or reject, never a third option.
2. Treat unclear as the rule directs. If the rule is silent, treat it as fail.
3. In live mode, check the comment against voice-guide.md and report any broken rule in the summary. This never changes the verdict.
4. Output a short summary, then a final fenced JSON block (item, checks, verdict). Quote the evidence for the deciding check.