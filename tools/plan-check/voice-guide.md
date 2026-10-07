# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

II'm an early-career dev doing this as my first open-source contribution, working through CodePath.org. I've reproduced but not yet fixed this codebase before. Readers should expect me to be precise about what I checked and cautious about what I claim: I am not a maintainer, nor an expert in this repo. I am proposing a plan, not announcing a fix.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

- Rule: no bare confirmations 
  - Wrong: "Can confirm, seeing this too!" 
  - Right: "Reproduced on `version` with `artifact`; differs from the report in `X`."
- Rule: no timeline promises 
  - Wrong: "I'll have a fix up by Friday." 
  - Right: "Next I'm going to look at [specific next step]."
- Rule: name the version explicitly 
  - Wrong: "using the latest version" 
  - Right: "v3.2.4 (pip), Python 3.12.4."
- Rule: hedge only with evidence 
  - Wrong: "I'm 100% sure this is the root cause." 
  - Right: "This looks consistent with [X], but I haven't ruled out `Y`."
- Rule: disclose AI use when the repo asks for it 
  - Wrong: (silence) 
  - Right: "I used an AI assistant to help organize this report; I ran and verified every step myself."
- Rule: name the files and the test
  - Wrong: "I'll make a fix and test it."
  - Right: "Touching sync_controller.go only. I'll re-run my repro steps; step 3 should show the pushed color."
- Rule: don't promise a PR, ask first
  - Wrong: "Will send a PR shortly."
  - Right: "If this approach looks right to you, I'll open a PR. Happy to adjust first."


## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- just installed and got the same issue" with no repro
- claiming certainty about root cause without an artifact
- piggybacking ("same as above, can confirm") on someone else's repro
- promising a PR before the maintainer has seen the approach