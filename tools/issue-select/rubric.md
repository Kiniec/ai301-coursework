# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|   maintainer_active| Last 5 default-branch commit dates(repo-facts block)  |  At least 1 commit within the last 90 days |  required |
| repo_in_use | Archived flag + last push to any branch (repo-facts block) | Repo is not archived AND last push within 365 days (of the capture date in eval mode; of today in live mode) | required |
| scope-feasible | Issue body: the work it asks for | The issue describes one identifiable piece of work someone could start: a behavior, a gap, or a task you can point at. It fails only when there is no single piece of work in it: a codebase-wide checklist, an "improve X everywhere", or a container issue tracking many sub-tasks. An open design edge, an "etc.", or several files involved never fails this check; that raises the difficulty note instead. | required |
| not_claimed | Comment thread, assignees, linked PRs (Development box / "linked PRs" in the repo-facts block) | No linked open PR (unchanged), AND no assignee, AND no claim comment ("I'll take this", "can I work on this", "working on this") posted within the last 60 days that the claimant did not later withdraw. A claim a maintainer answered counts as active at any age. | required |
| allows_ai_contributions| Contribution policy line in repo-facts block| Policy text does not prohibit AI-generated code/documentation| required |

## The difficulty note

With each accepted candidate, report a one-line difficulty note in
the read-out summary:

- **straightforward**: the issue names where the change lives and the
  change is bounded.
- **moderate**: the location is yours to find, or several files are
  involved.
- **ambitious**: an open design edge, or an unfamiliar subsystem;
  name the edge, because claiming this issue means raising it with
  the maintainer early.

The note is information for the chooser, never a verdict input: it
does not appear in the fenced JSON block, it never changes accept or
reject, and in eval mode it is skipped entirely.

## Verdict rule

 Accept if all required checks pass. Any required check that fails or is unclear rejects the issue. preferred checks never change the verdict — they only break ties when ranking multiple accepted issues