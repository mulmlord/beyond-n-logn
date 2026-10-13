# T03: Ceiling for the T16 seven-slot owner-packing family

Issue: https://github.com/mulmlord/beyond-n-logn/issues/4 (status is tracked there)

## Goal
Decide whether owner-packing search on the seven-slot k8 word still has
meaningful headroom. The #1028 → #1056 line gains about 10⁻⁸ per step, and
those gains may be approaching a ceiling.

## Background
#942 proved an all-replica bound for the U8 word. With word, capacities,
splitting rule and outer recipe fixed, no positive replica count beats T37
on the 10⁻¹⁸ grid. The proof relaxes chronology and physical feasibility and
prices bins with signed multipliers that support the moment inequality
(`research/community-frontier942-audit/ALL-T-BOUND.json`). #1010 (cbethin)
studies the sharp boundary of the T37 owner relaxation. #850 gives a continuum
owner bound for the 72-call inventory.

## Tasks
- Port the ALL-T-BOUND relaxation to the seven-slot k8 word and the T16
  capacity family. Compute an upper bound on κ over all owner maps and all
  replica counts.
- Compare the bound with the T01 base κ. Report the remaining gap in absolute
  terms and as a percentage.
- If the relaxation is loose, identify which relaxed constraint (chronology or
  physical feasibility) produces the looseness.

## Acceptance
- `docs/t16-ceiling.md` with the bound, its certificate, and a go/no-go call
  for T04:
  - gap < 10⁻⁸: drop T04 and put the effort into T05/T07.
  - otherwise: T04 proceeds, with the gap as its target.
- Includes an exact rational check of the bound (Fractions/sympy), not just floats.
