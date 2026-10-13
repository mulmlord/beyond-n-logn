# T02: κ evaluator and profile sensitivity tool

Issue: https://github.com/mulmlord/beyond-n-logn/issues/3 (status is tracked there)

## Goal
A fast tool that maps a candidate complex supplier (rank profile, prefix bits,
row coefficient) to κ. It runs without the multi-minute full replay, so that
search tickets can score thousands of candidates and rank the profile changes
that are worth the most.

## Background
- κ = ⌊s/(1+s)⌋ on a 10⁻¹⁸ grid, where s is the binding supplier endpoint
  (verified against #942: residual ≈ 9·10⁻¹⁹). Outer assembly:
  `research/*/engines/outer.py`. Moment engines: `engines/moment.py`,
  `engines/base_two_moment.py` in the #942 audit package.
- The complex supplier binds. The bit endpoint is 0.0017334, and it takes over
  at κ ≈ 0.0017304.

## Tasks
- Wrap upstream's two moment engines and the outer assembly in
  `tools/kappa_eval.py`. Import them from the pinned checkout. Do not
  re-implement the math, so our numbers stay comparable.
- Inputs: rank profile `{rank: count}`, prefix bit allowance (512 or 1024),
  row coefficient. Outputs: complex endpoint (both engines), κ, all 47
  slacks, bootstrap cutoffs, and the bit-binding margin.
- Sensitivity report: the Δκ from moving one unit of rank mass between
  classes (e.g. 48→44, 8→7, 2→1). Also the Δκ from cutting one rank-48
  residual and from one unit of helper width. Rank the results by Δκ per unit.
- Quantify the cost of the 1024-bit prefix charge compared with 512 bits.
  #942 charges 1024 and #1030 fits in 512. Decide whether prefix reduction
  is worth a ticket.
- Add a warning when a candidate is within 1% of the bit endpoint.

## Acceptance
- Reproduces #942 (0.001661960547713947) and the T01 base (#1056 or fallback)
  exactly from their profiles.
- One evaluation takes under 1 s on a laptop.
- `docs/sensitivity.md` lists the ranked levers with numbers. T03–T07 use it
  to choose targets.
