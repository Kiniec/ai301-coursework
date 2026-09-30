# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

@Kiniec

---

## Posted upstream

**Claim comment**

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5903937276 

I'd like to work on issue 72 as my first path review contribution. This issue has been claimed previously; therefore, I will be doing my own setup and posting my own report.

The issues: verify_password() in core/security.py raises passlib's
UnknownHashError on an unrecognizable stored hash instead of returning
False. Covering test: tests/unit/test_security.py::test_verify_with_wrong_hash_format
(strict xfail, H-05). I haven't run anything yet.

Next: set up via docs/SETUP.md, run that test with --runxfail plus a
valid-hash control, and call verify_password() directly to confirm the
exception surfaces outside pytest too. I'll post the environment,
commands, and output here either way.

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5904756583 

Reproduction report for #72. Result: reproduced on my fork.

Environment

    macOS 27.0 (build 26A428), arm64
    Python 3.13.7
    passlib 1.7.4, bcrypt 4.3.0, pytest 9.1.1
    Code: commit 7928bea, my fork. Note: earlier reports on this thread
    tested at 2f4e82f; I'm on a later commit, flagging the difference
    since I haven't diffed the two for this file.
    Installed via pip install -e ".[dev]" in a venv. No Docker,
    Postgres, or frontend needed — this bug is entirely in
    core.security and the covering test doesn't touch any service.

Steps

source .venv/bin/activate

# 1. As shipped, the strict xfail hides the error
python -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --disable-warnings
# -> 1 xfailed, 1 warning in 1.04s

# 2. Same test with the xfail marker ignored
python -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --runxfail --tb=short --disable-warnings

Output of step 2:

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format FAILED [100%]

=================================== FAILURES ===================================
_______________ TestSecurity.test_verify_with_wrong_hash_format ________________
tests/unit/test_security.py:227: in test_verify_with_wrong_hash_format
    result = verify_password("password", wrong_hash)
core/security.py:37: in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
.venv/lib/python3.13/site-packages/passlib/context.py:2343: in verify
    record = self._get_or_identify_record(hash, scheme, category)
.venv/lib/python3.13/site-packages/passlib/context.py:2031: in _get_or_identify_record
    return self._identify_record(hash, category)
.venv/lib/python3.13/site-packages/passlib/context.py:1132: in identify_record
    raise exc.UnknownHashError("hash could not be identified")
E   passlib.exc.UnknownHashError: hash could not be identified
========================= 1 failed, 1 warning in 0.20s =========================

3. Control — a wrong password against a valid bcrypt hash, to confirm the failure is specific to hash format, not verification in general:

python -m pytest tests/unit/test_security.py::TestSecurity::test_verify_password_incorrect -v --disable-warnings
# -> 1 passed, 1 warning in 0.68s

4. Direct call outside pytest, to confirm this isn't a pytest-harness artifact:

from core.security import hash_password, verify_password
good = hash_password("password")
print(verify_password("password", good))   # True
print(verify_password("nope", good))         # False
verify_password("password", "not_a_valid_bcrypt_hash")  # raises

Output:

control, right password -> True
control, wrong password -> False
malformed hash -> passlib.exc.UnknownHashError: hash could not be identified

Expected: verify_password() returns False when the stored value is
not a usable bcrypt hash — the same answer it gives for a wrong password.

Actual: for "not_a_valid_bcrypt_hash", passlib.exc.UnknownHashError
escapes from core/security.py:37. The control test above shows a normal
wrong-password check returns False correctly, so the failure is
specific to an unrecognizable stored hash.

Not part of this bug, noted so nobody chases it: passlib prints a
trapped AttributeError: module 'bcrypt' has no attribute '__about__'
on first load of bcrypt 4.3.0 — unrelated, and it doesn't affect the
result above.

Next I'll look at handling UnknownHashError inside verify_password,
check whether other malformed-but-bcrypt-shaped inputs raise a
different exception, and confirm the rest of tests/unit/test_security.py
still passes before opening a PR. 

I used an AI assistant (Claude) to help run and write this up; I've read and checked the output.



## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

1st run 20/20
Matches the agreement: 20/20 scored items (bar: 18/20: PASS) line in eval-run.txt.

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

pkg-20. Gold label: reject (category: disclosure). My rubric's verdict:
reject, agree. The repro report is excellent on every proof check —
environment, steps, and behavior all pass — but `ai_disclosure_compliant`
fails it: ghostty's stated AI policy requires disclosing all AI usage,
and the candidate comments don't disclose. This is the one-package
category the assignment calls out as the floor's whole point — a
rubric with no conventions check could pass this package on repro
quality alone and still miss the one thing it exists to catch.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

`ai_disclosure_compliant | Repo facts block's contribution-policy line,
read against the claim and repro comment text | If the stated policy
requires disclosing AI assistance, the comment discloses it in its own
words; if the policy has no such requirement, this passes by default |
required`

I made this its own required check, separate from `claim_comment_specific`,
because disclosure is a binary compliance question (did the repo's policy
get followed), not a specificity judgment. Making it conditional — pass
by default when no policy exists — keeps it from unfairly rejecting
packages from repos with no AI policy at all (most of the eval set),
while still catching the one repo that has one.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

ai_disclosure_compliant only reads the repo-facts contribution-policy
line; it would miss a repo whose AI-disclosure norm is unwritten and
only enforced informally by maintainers in the thread, since the
evidence guide points at the stated policy text, not thread conventions.
Separately, environment_recorded only requires that a version/commit
deviation be named, not that it be small — a report could honestly flag
a huge deviation (testing a version many releases old) and still pass
this check, even though a maintainer might reasonably still reject it
on those grounds. Nothing changed on this run: it agreed 20/20 on the
first pass, so no revision loop was needed.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
