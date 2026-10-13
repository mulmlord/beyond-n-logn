# T08: Compose winning changes and run strict admission

Issue: https://github.com/mulmlord/beyond-n-logn/issues/9 (status is tracked there)

## Goal
Turn the best result from T04, T05 and T07 (combined where they compose) into one
candidate that passes upstream's full strict admission, ideally from a cold
ancestry rebuild.

## Tasks
- Freeze the candidate's word, owner data, PLAN/SPEC and all input hashes.
- Run the complete replay:
  - scalar/frame/phase checks
  - owner and controller invoices
  - both moment engines, accepting the endpoint and rejecting the next 10⁻²⁴
    grid point
  - all 47 outer inequalities
  - bootstrap cutoffs
- Run a cold ancestry rebuild (#741 → #799 → word) in addition to the checked
  reuse path. State clearly which one each receipt covers.
- Run upstream's mutation/corruption controls and add targeted mutations
  for whatever we changed.

## Acceptance
- A PASS line with the new κ from a fresh work directory, both cold and reuse,
  with environment receipt (`VALIDATION.json`).
- κ above the best open claim at the time (T11 check done the same day).
