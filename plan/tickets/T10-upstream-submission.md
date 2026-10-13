# T10: Package and submit the upstream PR

Issue: https://github.com/mulmlord/beyond-n-logn/issues/11 (status is tracked there)

## Goal
A PR to CrocSwap/integer-mult-bounds that a maintainer can review and replay
with one command.

## Tasks
- Branch from `origin-upstream/main`, not the fork's `main`, which carries
  `plan/` (see `plan/docs/pins.md`).
- Lay out `research/<name>/` like recent accepted packages:
  - `README.md`, `PROOF.md` / `CONSTRUCTION.md`, `NOTICE.md`
  - `MANIFEST.json`, `SOURCE.json`, `RESULT.json`, `VALIDATION.json`
  - `data/`, plus a `reproduce.py` / `verify.py` that ends in a single PASS line
- Pin every upstream source by commit and sha256. Leave `upstream/` and
  existing packages untouched. Edit generators under `scripts/` only if needed.
- Write the PR description:
  - claimed κ and the exact gain over the parent
  - mechanism, plus validation scope (cold vs reuse, environment, hosted CI separate)
  - retained assumptions; no claim of an unconditional theorem or a Lean proof
  - credits for every predecessor PR
  - disclosure of substantial AI assistance
- Run `make verify` plus the affected targets.
- **Confirm with the project owner before pushing the branch or opening the
  PR.** Both actions publish the work.

## Acceptance
- The PR is open upstream and its reproduction command passes on a clean
  clone of our branch.
