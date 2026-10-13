# T11: Upstream frontier sync (recurring)

Issue: https://github.com/mulmlord/beyond-n-logn/issues/12 (status is tracked there)

## Goal
Upstream received dozens of κ-claiming PRs on 2026-10-13 alone. This ticket
keeps us from optimizing a stale base or submitting below someone else's
open claim.

## Tasks (each time)
- `gh pr list -R CrocSwap/integer-mult-bounds --state open --limit 100` and the
  merged list since the last sync. Extract the claimed κ values from titles and bodies.
- Update the "Open frontier claims" table in `docs/landscape.md` and the
  targets in `README.md`.
- If a new claim beats our base, decide whether to rebase onto it (repeat
  the T01 replay) or keep going. Record the decision in `docs/frontier-base.md`.
- Check whether `certificates/selected-result.json` on upstream `main` has changed.

## When
- Before starting any search run in T04/T05/T07.
- On the day of T08 admission.
- Immediately before T10 submission. This check gates T10.
