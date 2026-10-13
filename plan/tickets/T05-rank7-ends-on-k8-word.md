# T05: Port rank-seven helper ends (#1030) onto the k8 word

Issue: https://github.com/mulmlord/beyond-n-logn/issues/6 (status is tracked there)

## Goal
Combine two mechanisms that, on paper, change different parts of the
construction:
- #1030's helper-end reduction, a **word** change: helpers 588/589 finish in
  dimension 7 instead of 8.
- The T16 **owner packing** of the #1056 line.

## Background
On U8/T37, #1030 cut helper width per call from 3778 to 3776 and local rank
mass from 5634 to 5632. The two released units absorb exactly 2400 rank-48
residuals. Its prefix bound is 257 bits, inside the 512-bit allowance, and κ
rises by about 3.9·10⁻⁵ relative to #942. It was built on the U8 word and
has not been tried on the seven-slot k8 word.

## Tasks
- Check whether the seven-slot k8 word has helper ends whose final dimension
  can drop from 8 to 7 under the same frame and early-cleanup conditions
  (#1030 `PROOF.md`, `END-RECIPE.json`). #988's end-of-B rank-eight analysis
  is relevant.
- Rebuild the word with those ends. Re-run T04, or the #1056 exchanges, to
  repack owners into the released capacity.
- Score with T02, then run the strict replay. Check the prefix bound and the
  physical row coefficient (< 20161).

## Acceptance
- One of these outcomes, with numbers:
  - a strict-replay-admitted κ above the T01 base, or
  - a documented obstruction explaining why the k8 word cannot take rank-7 ends.
- Attribution covers both AlexS-scale (#1030) and the k8/T16 lineage.
