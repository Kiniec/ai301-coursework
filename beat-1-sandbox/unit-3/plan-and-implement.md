# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile - no @, no
profile URL. Your comment upstream is identified by this name, and it is
the only thing that ties it to you. Several students may plan the same
house issue, so this is what keeps their comments off your score and
yours off theirs.]

Kiniec

**Plan comment**

[Link to the comment where you posted your plan on the issue. Use the comment's own
permalink. **Then paste the text of that comment underneath the link** — the pasted text is
what this field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-6029652765

Plan for #72:

I've reproduced it on my fork at commit 7928bea. Earlier reports on this thread used 2f4e82f; a git diff of core/security.py between the two commits is empty, so it's the same code.
The cause is in verify_password(), at core/security.py:37. It calls pwd_context.verify() with nothing around it. Hand it "not_a_valid_bcrypt_hash" and passlib raises UnknownHashError, which escapes instead of coming back as False. I saw this by running test_verify_with_wrong_hash_format with --runxfail:

core/security.py:37: in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
E   passlib.exc.UnknownHashError: hash could not be identified

A wrong password against a valid hash still returns False, so the problem is the stored hash's format.
My plan is to catch UnknownHashError in verify_password() and return False. I'd also remove the strict xfail on that test. That touches core/security.py and tests/unit/test_security.py, and nothing else. I'm leaving hash_password(), the passlib and bcrypt versions, and the login route alone.
To check it, I'll re-run my repro. Today the test shows 1 xfailed and a direct call raises. After the fix I expect 1 passed and False. The right-password and wrong-password controls should still give True and False, and the rest of tests/unit/test_security.py should pass.
I haven't tried other malformed inputs, such as a truncated hash or an empty string. If one raises a different exception, I'll post that here before widening the catch. One side effect: the login route will report bad credentials for a corrupted stored hash. I'm not adding logging for that in this change.
I used an AI assistant (Claude) to help draft this plan; I've checked it against my repro.


---

## Your branch

**Branch**

[The name of the branch you built the change on, exactly as it appears in your fork. The
naming shape is a type prefix, then the issue number, then a short description. **The issue
number in the branch name must be the number of the issue you claimed** — a name carrying
any other number does not satisfy this field.]

fix/72-verify-password-unknown-hash

**Evidence**

[Your Unit 2 reproduction steps re-run against the built change: the before, then the
after. Paste both, including the commands you ran and their output.]


*Before:*
```
python -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --disable-warnings
================================================================================= test session starts ==================================================================================
platform darwin -- Python 3.13.7, pytest-9.1.1, pluggy-1.6.0 -- /Users/xxx/xxx/ai301_ai_capstone_open_source_cap_stone/pathreview-ai301-fa26-s3/.venv/bin/python
cachedir: .pytest_cache
hypothesis profile 'default'
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /Users/xxx/xxx/ai301_ai_capstone_open_source_cap_stone/pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: platformdirs-4.12.2, hypothesis-6.168.3, cov-7.1.0, asyncio-1.4.0, benchmark-5.3.0, pytest_httpserver-1.1.5, anyio-4.15.1
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 1 item tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL (issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning...) [100%]

============================================================================ 1 xfailed, 1 warning in 0.37s =============================================================================
```


*After: with fix applied,  marker still on:*
```
 python -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --disable-warnings
================================================================================= test session starts ==================================================================================
platform darwin -- Python 3.13.7, pytest-9.1.1, pluggy-1.6.0 -- /Users/xxx/xxx/ai301_ai_capstone_open_source_cap_stone/pathreview-ai301-fa26-s3/.venv/bin/python
cachedir: .pytest_cache
hypothesis profile 'default'
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /Users/xxx/xxx/ai301_ai_capstone_open_source_cap_stone/pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: platformdirs-4.12.2, hypothesis-6.168.3, cov-7.1.0, asyncio-1.4.0, benchmark-5.3.0, pytest_httpserver-1.1.5, anyio-4.15.1
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 1 item tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format FAILED                                                                                             [100%]

======================================================================================= FAILURES =======================================================================================
___________________________________________________________________ TestSecurity.test_verify_with_wrong_hash_format ____________________________________________________________________
[XPASS(strict)] issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
=============================================================================== short test summary info ================================================================================
FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - [XPASS(strict)] issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
============================================================================= 1 failed, 1 warning in 0.29s ============================================================================= 
```

*After: marker removed:*
```
python -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --disable-warnings
================================================================================= test session starts ==================================================================================
platform darwin -- Python 3.13.7, pytest-9.1.1, pluggy-1.6.0 -- /Users/xxx/xxx/ai301_ai_capstone_open_source_cap_stone/pathreview-ai301-fa26-s3/.venv/bin/python
cachedir: .pytest_cache
hypothesis profile 'default'
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /Users/xxx/xxx/ai301_ai_capstone_open_source_cap_stone/pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: platformdirs-4.12.2, hypothesis-6.168.3, cov-7.1.0, asyncio-1.4.0, benchmark-5.3.0, pytest_httpserver-1.1.5, anyio-4.15.1
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 1 item tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED                                                                                             [100%]

============================================================================= 1 passed, 1 warning in 0.29s =============================================================================
```

*After: direct call and controls:*
```
python -c '
from core.security import hash_password, verify_password
good = hash_password("password")
print("control, right password ->", verify_password("password", good))
print("control, wrong password ->", verify_password("nope", good))
print("malformed hash ->", verify_password("password", "not_a_valid_bcrypt_hash"))
'
(trapped) error reading bcrypt version
Traceback (most recent call last):
  File "/Users/xxx/xxx/ai301_ai_capstone_open_source_cap_stone/pathreview-ai301-fa26-s3/.venv/lib/python3.13/site-packages/passlib/handlers/bcrypt.py", line 620, in _load_backend_mixin
    version = _bcrypt.__about__.__version__
              ^^^^^^^^^^^^^^^^^
AttributeError: module 'bcrypt' has no attribute '__about__'
control, right password -> True
control, wrong password -> False
malformed hash -> False
```

*Unknowns*
```
python -c '
from core.security import verify_password
for h in ["", "$2b$12$abc"]:
    try:
        print(repr(h), "->", verify_password("password", h))
    except Exception as e:
        print(repr(h), "->", type(e).__name__, e)
quote> '
'' -> False
'$2b$12$abc' -> ValueError salt too small (bcrypt requires exactly 22 chars)
```
*Full File:*
```
python -m pytest tests/unit/test_security.py -v --disable-warnings
================================================================================= test session starts ==================================================================================
platform darwin -- Python 3.13.7, pytest-9.1.1, pluggy-1.6.0 -- /Users/xxx/xxx/ai301_ai_capstone_open_source_cap_stone/pathreview-ai301-fa26-s3/.venv/bin/python
cachedir: .pytest_cache
hypothesis profile 'default'
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: /Users/xxx/xxx/ai301_ai_capstone_open_source_cap_stone/pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: platformdirs-4.12.2, hypothesis-6.168.3, cov-7.1.0, asyncio-1.4.0, benchmark-5.3.0, pytest_httpserver-1.1.5, anyio-4.15.1
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 25 items tests/unit/test_security.py::TestSecurity::test_hash_password_returns_bcrypt_hash PASSED                                                                                         [  4%]
tests/unit/test_security.py::TestSecurity::test_verify_password_correct PASSED                                                                                                   [  8%]
tests/unit/test_security.py::TestSecurity::test_verify_password_incorrect PASSED                                                                                                 [ 12%]
tests/unit/test_security.py::TestSecurity::test_verify_password_case_sensitive PASSED                                                                                            [ 16%]
tests/unit/test_security.py::TestSecurity::test_hash_same_password_different_hash PASSED                                                                                         [ 20%]
tests/unit/test_security.py::TestSecurity::test_create_access_token_returns_string PASSED                                                                                        [ 24%]
tests/unit/test_security.py::TestSecurity::test_create_access_token_is_jwt PASSED                                                                                                [ 28%]
tests/unit/test_security.py::TestSecurity::test_decode_access_token_valid PASSED                                                                                                 [ 32%]
tests/unit/test_security.py::TestSecurity::test_decode_access_token_invalid_token PASSED                                                                                         [ 36%]
tests/unit/test_security.py::TestSecurity::test_decode_access_token_malformed PASSED                                                                                             [ 40%]
tests/unit/test_security.py::TestSecurity::test_decode_access_token_empty_string PASSED                                                                                          [ 44%]
tests/unit/test_security.py::TestSecurity::test_roundtrip_token_with_data PASSED                                                                                                 [ 48%]
tests/unit/test_security.py::TestSecurity::test_create_access_token_with_custom_expiry PASSED                                                                                    [ 52%]
tests/unit/test_security.py::TestSecurity::test_access_token_includes_expiration PASSED                                                                                          [ 56%]
tests/unit/test_security.py::TestSecurity::test_password_hash_different_for_different_passwords PASSED                                                                           [ 60%]
tests/unit/test_security.py::TestSecurity::test_verify_password_with_empty_strings PASSED                                                                                        [ 64%]
tests/unit/test_security.py::TestSecurity::test_verify_password_with_special_characters PASSED                                                                                   [ 68%]
tests/unit/test_security.py::TestSecurity::test_token_with_empty_data PASSED                                                                                                     [ 72%]
tests/unit/test_security.py::TestSecurity::test_token_with_special_characters_in_data PASSED                                                                                     [ 76%]
tests/unit/test_security.py::TestSecurity::test_token_with_unicode_data PASSED                                                                                                   [ 80%]
tests/unit/test_security.py::TestSecurity::test_hash_password_long_input PASSED                                                                                                  [ 84%]
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED                                                                                             [ 88%]
tests/unit/test_security.py::TestSecurity::test_token_tampering_detection PASSED                                                                                                 [ 92%]
tests/unit/test_security.py::TestSecurity::test_create_token_consistency PASSED                                                                                                  [ 96%]
tests/unit/test_security.py::TestSecurity::test_password_with_whitespace PASSED                                                                                                  [100%]

============================================================================ 25 passed, 1 warning in 5.93s =============================================================================
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

agreement: 19/20 scored items  (bar: 18/20: PASS) one run.

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

pkg-01 (wrong-cause), httpie/cli#1838

- gold label: reject
- my rubric: reject
- agree: yes

The plan's diagnosis says the cause is the request-item tokenizer in httpie/cli/requestitems.py, whose regex "fails to recognize header1:xyz and x=1". It calls the Python-version difference "a red herring". The repro evidence contradicts this in three places:
- Step 4: --debug shows the error is raised by argparse's parse_args "while consuming positionals; the request items are never handed to HTTPie's item parser." So the tokenizer never runs on the failing input.
- Step 2: the same items parse fine on 3.11 when the -v flag is removed, so the tokenizer handles them.
- Step 3: the same command works on 3.13.5, so the Python version does matter.

diagnosis_matches_repro asks that the cause explain the exact quoted symptom and not contradict the evidence. This plan names a specific file and regex, so it passes the "names a cause" half. But it contradicts the repro, so the check fails and the rubric rejects the package. The plan would also rewrite the wrong code and leave the bug in place.

---

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/plan-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

`diagnosis_matches_repro | The plan's stated cause, read against the repro evidence it quotes | The cause explains the exact quoted symptom and names a cause (file, function, or  condition), not just the symptom. It doesn't contradict the evidence.| required`

I wrote it this way because the wrong-cause packages share one pattern: the plan patches where the error shows up instead of what produces it. That's why the check reads the plan's cause against the repro's own quoted output, and why the pass condition asks for a named file, function, or condition. A plan that restates the symptom ("it raises an exception") gets rejected. A plan that traces it to a cause ("verify_password() calls pwd_context.verify() with no handling") passes. I based this on my unit 2 behavior_matches_issue check, which also read an artifact against a stated symptom. I dropped the structure-shaped checks I had considered, such as "has a Cause section", because the template warns those make graders disagree with themselves.


**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

With pkg-20, the one disagreement in my final run (19/20, thread-convention 1/2) is as follows: The gold label is reject: the repo's AI_POLICY requires disclosing any AI use, and the plan comment never discloses it. My rubric graded the package accept, because its diagnosis, scope, and test plan are sound, and those are the only things my three checks read. I accepted this miss because adding a comms check could loosen or tighten other packages. If I added one, I'd re-run pkg-20 and pkg-04 with --only, plus a canary from each other category.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
