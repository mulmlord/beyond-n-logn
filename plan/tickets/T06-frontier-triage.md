# T06: Triage open PRs for profile-changing mechanisms

Issue: https://github.com/mulmlord/beyond-n-logn/issues/7 (status is tracked there)

## Goal
Upstream has more than 30 open PRs and gets many more each day. Most only
reduce bit-circuit ADDs, which cannot move κ while the complex supplier
binds. Find the few mechanisms that change the **complex rank profile**,
helper widths or capacities, and that could stack with our base.

## Tasks
- For each open PR, record in `docs/triage.md`:
  - which side it touches (complex/bit)
  - whether it changes the recursive rank profile
  - the claimed Δκ
  - which word it was built on
  - whether it can be composed with the k8/T16 base
- Look first at:
  - #1060: P111 COPY word with a smaller paid recursive moment
  - #1011: jointly restored X4 target shears, saving 256 beyond one shear
  - #969: deferred swaps, 560 primitives per CK/JP8 orientation
  - #1034: common dual mixed owner assembly across 71 provider records
  - #1004/#1005: mutable-leaver cells
  - #1018: triangle hybrid
- For each composable candidate, estimate Δκ with T02 before spending any
  effort on replays.
- Also list the scoped negative results (#845, #1008, #1014, #1033) as
  directions not to retry.

## Acceptance
- `docs/triage.md` with a ranked shortlist (estimated Δκ, composition effort)
  and a "do not retry" list with reasons.
- The shortlist feeds T07/T08.
