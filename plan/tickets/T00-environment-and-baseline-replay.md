# T00: Environment and cold replay of #942

Issue: https://github.com/mulmlord/beyond-n-logn/issues/1 (status is tracked there)

## Goal
Have a working, pinned upstream checkout on which the selected result's cold
replay passes locally, so that every later claim is measured against a known-good
toolchain.

## Tasks
- The fork already exists at `mulmlord/beyond-n-logn`. Its last push was
  2026-10-10, so it is behind upstream. Sync it with `CrocSwap/integer-mult-bounds`
  `main` (confirm with the project owner first). Clone it as the
  project directory (see `plan/README.md`), with the original repo as the `origin-upstream` remote.
- Record the pinned commit in `docs/pins.md`.
- Install a C++17 compiler, Boost headers (Boost.Multiprecision), and
  Python 3.11+ with `numpy sympy scipy`. Capture the versions in `docs/environment.md`.
- Run `make frontier942-verify` cold in a fresh work directory. Record wall-clock
  time, peak memory, and the final PASS line.
- Note any steps that need network access or `/tmp` paths. The #942 review
  mentions `/tmp/batch952-baseline799` and `/tmp/frontier741-composed-fresh`.

## Acceptance
- `make frontier942-verify` passes and reproduces κ = 0.001661960547713947.
- `docs/environment.md` and `docs/pins.md` let a second machine repeat the run.
