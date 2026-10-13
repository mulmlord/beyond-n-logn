# T09: Independent re-verification of our candidate

Issue: https://github.com/mulmlord/beyond-n-logn/issues/10 (status is tracked there)

## Goal
Catch our own mistakes before reviewers do. Upstream reviews regularly reject
claims at binding or source-integrity checks.

## Tasks
- Recompute the endpoint and κ with code that shares nothing with the
  upstream engines: a separate exact-rational moment evaluation and an
  independent 47-inequality check, in the style of #1051/#1052.
- Replay on a second environment, ideally Linux CI in our fork, using
  different Python and Boost versions.
- Check every hash pin in our manifests against the actual bytes. Compare the
  decompressed payloads of regenerated `.gz` artifacts, not their container hashes
  (CONTRIBUTING, reproducibility note).
- List every inherited assumption the result still depends on.

## Acceptance
- The independent computation matches κ exactly.
- The second-environment replay passes.
- `docs/assumptions.md` lists the remaining conditional interfaces.
