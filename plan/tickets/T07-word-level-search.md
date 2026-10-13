# T07: Word-level search to cut rank-48 residual mass

Issue: https://github.com/mulmlord/beyond-n-logn/issues/8 (status is tracked there)

## Goal
Get a gain that does not depend on packing a fixed word. #942's all-replica
bound, and T03 if it confirms the same for k8, show that owner packing
saturates once the word is fixed. Larger gains need a word with less
expensive residual mass.

## Background
- In #942 the `48` class (11086 residuals of rank 48) is the only high-rank
  class. #1030 gained by turning residual rank into capacity the packing
  could absorb (2400 rank-48 residuals).
- The levers depend on what T02's ranking shows. Likely candidates:
  - fewer rank-48 residuals
  - rank-48 → 44 adapters (the `44+3+2 → 48+1` whole-role edits of #845's context)
  - narrower helpers
  - more replicas per capacity unit
- #845 proves an annihilator-dimension obstruction for real scalars with fixed
  coordinate readers. Changing the readers or ports is outside that obstruction.

## Tasks
- Using T02's ranking, choose 1–2 structural targets and write the
  hypothesis for each in `docs/word-search.md` before searching.
- Build a search over local word variants: helper-end dimensions, residual
  adapters, gauge44 provider choices. Use the T02 evaluator as the objective,
  plus the local constraints: scalar, frame, phase, prefix ≤ 1024 bits (≤ 512
  is preferred), and row coefficient < 20161.
- For promising words, run the native 5/9/11-stage checks, then repack owners
  with T04 tooling.
- Record negative results in the same format upstream uses for scoped
  obstructions.

## Acceptance
- A word that, after repacking, beats the T01 base by more than the
  T03 packing ceiling gap, or
- a written obstruction for each target that was tried, with exact
  certificates.
