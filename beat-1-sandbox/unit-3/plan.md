# Plan

## Diagnosis

`verify_password()` at `core/security.py:37` calls `pwd_context.verify()` with no error handling. When the stored value isn't a recognizable bcrypt hash, passlib raises `UnknownHashError` and it escapes instead of `verify_password()` returning `False`.

Repro evidence I'm relying on (commit `7928bea`, my fork):

- Step 2, the covering test with the strict `xfail` ignored (`--runxfail`):

  ```
  core/security.py:37: in verify_password
      return bool(pwd_context.verify(plain_password, hashed_password))
  E   passlib.exc.UnknownHashError: hash could not be identified
  ```

- Step 3, control: `test_verify_password_incorrect` passes. A wrong password against a valid bcrypt hash returns `False`, so the failure is specific to the stored hash's format, not to verification in general.
- Step 4, direct call outside pytest:

  ```
  control, right password -> True
  control, wrong password -> False
  malformed hash -> passlib.exc.UnknownHashError: hash could not be identified
  ```

What I haven't proved: whether other malformed inputs (truncated hash, empty string) raise a different exception. I'll check that during the build.

## Scope

- **In:** catch `UnknownHashError` inside `verify_password()` and return `False`. Remove the strict `xfail` marker from `test_verify_with_wrong_hash_format`, since it is the issue's own covering test.
- **Out:** `hash_password()`, the passlib/bcrypt versions, the `bcrypt.__about__` warning (unrelated, noted in my repro), and the login route.

## Files that will be touched

- `core/security.py`: `verify_password()` only.
- `tests/unit/test_security.py`: remove the `xfail` marker on `test_verify_with_wrong_hash_format`.
- I'll read but not change `api/routes/auth.py:80`, which calls `verify_password()` on login.

## Approach

1. Import `UnknownHashError` from `passlib.exc` in `core/security.py`.
2. Wrap the `pwd_context.verify()` call in `try/except UnknownHashError: return False`.
3. Remove the `xfail` marker from `test_verify_with_wrong_hash_format`.
4. Run the target test, then all of `tests/unit/test_security.py`.

## Test Plan

I'll re-run my unit 2 repro steps.

- **Before (from my repro):** step 1 shows `1 xfailed`, step 2 shows `UnknownHashError`, step 4 shows `malformed hash -> UnknownHashError`.
- **After the fix, I expect:**
  - `test_verify_with_wrong_hash_format` with the marker removed: `1 passed`.
  - The step 4 direct call prints `False` for `"not_a_valid_bcrypt_hash"`.
  - The controls are unchanged: right password `True`, wrong password `False`.
  - The rest of `tests/unit/test_security.py` still passes.

## Risks/Unknowns

- Other malformed-but-bcrypt-shaped inputs may raise a different exception. I'll test a truncated hash and an empty string, and report what I find.
- Catching only `UnknownHashError` is the narrowest fix. Catching `ValueError` as well would be broader. I'm starting narrow and will widen only if the other-inputs check shows I need to.
- Returning `False` hides a corrupted stored hash from the login route, which will just report bad credentials. I'm treating logging a warning as out of scope and a possible follow-up.
- I tested at `7928bea`, while earlier reports on the thread used `2f4e82f`. `git diff 2f4e82f 7928bea -- core/security.py` is empty, so `core/security.py` is unchanged between them. I haven't checked `tests/unit/test_security.py`.

## Deviations


[What changed between the plan you posted and the change you built, and
why. If nothing changed, say so in your own words - "nothing changed;
the plan held" earns these points in full. Leaving this blank does not.]

Nothing changed, the plan held true.

