# T04: Owner-map search beyond #1056

Issue: https://github.com/mulmlord/beyond-n-logn/issues/5 (status is tracked there)

## Goal
Find an owner map for the seven-slot k8 word that beats the best open claim.
The search keeps the local word, widths, call order and source-event times fixed.

## Background
#1050/#1053/#1055 use LNS on `data/{OWNERS,PLAN,SPEC}`. #1056 adds repeated
whole-helper exchanges. Both change only frozen owner data. The verifier
does not change, so a better map can be admitted by rerunning the strict replay.

## Tasks
- Build the search on the T02 evaluator, using exact rational scoring for
  the final candidates.
- Try moves the existing line has not tried:
  - multi-helper k-exchanges (k ≥ 3)
  - ejection chains
  - an exact ILP/CP-SAT re-solve of a window of replicas with everything else fixed
- Use T03's dual prices to guide moves when available, since they show where
  the bound is loose.
- Run the strict replay (69 admission controls, 12 bit controls, 15 controller
  mutations, 6 owner controls, all 47 outer inequalities) on every candidate
  that beats the current best.

## Acceptance
- A strict replay passes with κ above the best open claim at the time
  (check T11).
- The search is reproducible from a fixed seed and documented in
  `research/<name>/README.md`, in the upstream package layout.

## Dropped if
T03 shows the remaining gap is < 10⁻⁸.
