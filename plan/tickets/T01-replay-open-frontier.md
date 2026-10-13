# T01: Replay the strongest open claim (#1056 chain)

Issue: https://github.com/mulmlord/beyond-n-logn/issues/2 (status is tracked there)

## Goal
Use the best *unreviewed* construction as our working base, and confirm that it
actually replays. The seven-slot k8 / T16 line (#1005 → #1018 → #1022 → … →
#1050 → #1056) is about 0.62% above #942. Starting anywhere lower wastes effort.

## Tasks
- Check out the PR heads for #1005, #1018, #1050, #1055 and #1056. Pin the commit SHAs.
- Run each package's reproduction command. #1056 runs `verify.py` and reuses
  checked #1018 native replay and the #1005 chain. Record whether each step
  is a cold rebuild or reuses an earlier replay.
- Confirm the claimed κ values: #1056 = 0.001672267698427438,
  #1055 = 0.001672251604432734.
- Extract the complex rank profile, owner map (`data/OWNERS.json.gz`), PLAN
  and SPEC from #1056 into a form T02 can read.
- Write `docs/frontier-base.md`: which PR we build on, its pins, its
  reproduction cost, and any replay discrepancies.

## Acceptance
- At least one of #1056/#1055 replays to its claimed κ on our machine, or the
  failure is documented with logs and we fall back to the highest claim that
  does replay.
- The base profile and owner data load in the T02 evaluator.

## Notes
These PRs are unreviewed. If one fails its strict verifier, record the
finding. A correct negative report is itself a contribution upstream values.
