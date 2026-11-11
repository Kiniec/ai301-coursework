# Contribution: Docs: recurring events on the Nth weekday of the month #10908

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Mar Kiniec Carlisle
**GitHub Username:** Kiniec
**Issue:** <https://github.com/ChurchCRM/CRM/issues/10908>
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built issue-scout with my own search strategy and rubric**

 This week I built issue-scout's search strategy and rubric. The strategy runs six gh search issues queries (good first issue, open, unassigned, recently updated, in Python, JavaScript, Java and TypeScript, plus a docs query), then ranks the results by fewest comments and caps grading at the top 5. Running it hit GitHub's secondary rate limit (HTTP 403) and had to be paced, and the first scan's top 5 had 3 issues from one repo, with brand-new owner-filed issues favored by the "fewest comments" ordering. Grading two hand-picked issues also showed that an umbrella issue (blazingmq#87) can be accepted because issue_scope_small is only preferred, so I would make scope required and cap issues per repo.

**Unit 6: Added a voice guard to my claims and fixed a rubric that fought it**

This week I wrote the upstream rules for my voice guide and installed the voice guard hook, which now reads every comment before it goes out. It stopped an early claim draft for having no rough window, and once refused to post because it looked for my draft in the wrong folder. The bigger snag was in repro-check, where my rubric said a claim should promise no timeline while my voice guide said it needs a rough window, so I loosened the rubric to allow a window and still rule out dated deadlines. I also wrote a local memory file for the ChurchCRM docs repo, keeping only the rules I could get wrong, like opening the PR against main with the Current milestone and never committing screenshots, and pointing to the repo's own guides for the rest.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I found this issue on the Issue Selection site and graded it, along with a few other picks, with my scout. Most of the others fell apart on a closer look because they were already claimed, were umbrella issues, or lived in C# repos. ChurchCRM issue #10908 came out as accept with a moderate difficulty note. It asks for one clear thing, updating the docs for the new "Nth weekday of the month" recurring event pattern, and the code behind it already shipped in 7.8.3. It fits me because it's small and documentation-adjacent with no application code, and I hope to learn how to follow an unfamiliar project's rules, here a separate docs repo with a release-milestone workflow. I claimed it here: https://github.com/ChurchCRM/CRM/issues/10908#issuecomment-6786399202. The scout held up only after patching, since it first accepted an umbrella issue, missed claim comments, and never told me the docs live in a different repo.
**Toolkit**

- Tool: issue-scout, with my own search strategy and rubric, run once as a scan and then in direct mode on picks from the Issue Selection site.
- What it produced: A ranked scan, then graded read-outs for each pick. For ChurchCRM#10908, every required check passed, giving accept with a moderate difficulty note.
- Difficulties: It accepted an umbrella issue (blazingmq#87) because scope was only a preferred check. Its claim check only looked at linked PRs, not claim comments. It also passed a one-week-old repo with two commits and no outside reviews, and it couldn't see that the docs live in a separate repo.
- What changed: I swapped my scope check for the scope-feasible row with a difficulty note, and widened not_claimed to include assignees and recent claim comments. I would still add a per-repo cap on scan results and a check for whether a maintainer has ever answered an outside contributor.


---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

- OS: macOS 27.0.1, arm64
- Tools: git 2.50.0, curl, gh CLI (Node v25.2.1 is installed but I did not build the site)
- Docs repo: `ChurchCRM/docs.churchcrm.io`, shallow clone of `main` at commit `296ac7821c64475380cc32aad6f2a7f3616bad3c` (2026-11-10)
- Docs pin: `crm-release.json` says `{"version": "7.8.3"}`, the same release the issue's feature (PR #10907) shipped in
- ChurchCRM source: tag `7.8.3`

**Steps to Reproduce**

1. Clone the docs repo and check what it is pinned to.

   ```
   git clone --depth 1 https://github.com/ChurchCRM/docs.churchcrm.io.git
   cd docs.churchcrm.io
   cat crm-release.json
   ```

2. Search the docs for the new pattern.

   ```
   grep -rniE 'monthly-weekday|nth weekday|RecurWOM|RecurDOW|on a weekday|1st.{0,6}5th' docs/
   ```

3. Read what the Ministry Calendar tab page says about the Repeats choices.

   ```
   sed -n '50p' docs/user-guide/ministries/events-and-calendar.md
   ```

4. Check whether the Repeat Events editor is documented.

   ```
   grep -nEi 'repeat|recurrence|pattern|monthly|weekly' docs/user-guide/events.md
   ```

5. Confirm the feature exists in 7.8.3 (the `-s` flag keeps curl quiet).

   ```
   curl -fsSL https://raw.githubusercontent.com/ChurchCRM/CRM/7.8.3/src/event/views/repeat-editor.php | grep -nE 'monthly-weekday|RecurWOM'
   curl -fsSL https://raw.githubusercontent.com/ChurchCRM/CRM/7.8.3/docs/openapi/generated/private-api.yaml | grep -nE 'monthly-weekday|RecurWOM'
   ```


**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:** [if applicable]
- **My findings:** 
  I reproduced part of the issue, and one part does not look like a gap.
  - **Ministry Calendar tab: reproduced.** The shipped dialog offers a "Monthly, on a weekday" choice (the issue's wording), but the page's Repeats row lists only Weekly, Monthly on a day of the month, and Yearly.
  - **Repeat Events editor: reproduced, with a caveat.** The new "Every month on the [1st-5th] [weekday]" row has no docs, but the editor's recurrence options are not documented anywhere in `events.md` either. So this may mean writing new text, not fixing an existing sentence.
  - **API (`POST /api/events/repeat`): not reproduced as a gap.** The generated `private-api.yaml` at 7.8.3 already lists `monthly-weekday` and `RecurWOM`. The docs repo only holds `docs/api/` index pages and downloads the specs from the pinned release at build time (`scripts/download-openapi.sh`), so the published API reference should already show these fields. I did not build the site to confirm the rendered page.
  - **"Event types cannot store this pattern": no docs mention it.** I found no sentence about it. Line 96 of `events.md` says event types set "the recurrence frequency", which could mislead, but I haven't confirmed that against the app.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
