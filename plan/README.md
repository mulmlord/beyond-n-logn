# beyond-n-logn

Goal: raise the conditional exponent saving κ in

$$T(n) = O\big(n(\log n)^{1-\kappa}\big)$$

beyond the best value in
[CrocSwap/integer-mult-bounds](https://github.com/CrocSwap/integer-mult-bounds),
then submit the construction upstream as a reproducible, attributed PR.

## Targets (snapshot 2026-10-13)

| Reference | κ | Source |
|---|---|---|
| Reviewed selected result | 0.001661960547713947 | #942 (T37 owner packing on U8 word) |
| Best *open, unreviewed* claim | 0.001672267698427438 | #1056 (whole-helper exchanges, T16 owner map, seven-slot k8 word) |
| Bit-supplier ceiling | ≈ 0.0017304 | where the bit supplier (0.0017334) starts binding |

**Success means** a strict full replay that beats the best open claim at
submission time, not only the reviewed value. The frontier moves daily. Re-check
it before starting a search and before submitting ([T11](tickets/T11-upstream-sync.md)).

## How κ is set (what actually moves the number)

- The outer assembly (47 strict inequalities) gives
  κ = ⌊s/(1+s)⌋ on a 10⁻¹⁸ grid, where s is the **binding supplier endpoint**.
  For #942, s = 0.001664727258740678… and s/(1+s) − κ ≈ 9·10⁻¹⁹. The outer
  recipe has no slack worth chasing.
- The **complex supplier binds**. The bit supplier is about 4.1% above it, so
  bit-circuit ADD savings do not change κ. Many upstream "no new kappa" PRs
  fall into this category.
- The complex endpoint comes from the **recursive rank profile**
  (e.g. #942: `{1:848490, 2:112554, 3:148518, 4:53946, 5:23976, 8:2664, 48:11086}`).
  Two rational moment engines evaluate it. Changes to the word (helper widths,
  helper-end dimensions, residual adapters) and to the owner packing (how
  residuals are assigned to replicas) move this profile.

See [docs/landscape.md](docs/landscape.md) for the lineage, open PRs and known
obstructions.

## Layout

This `plan/` folder lives on the fork's `main`, alongside the upstream
sources. Upstream never touches `plan/`. Local setup:

```
<project dir>/            e.g. ~/Projects/beyond-n-logn
├── upstream/             checkout of this fork (contains plan/)
├── .venv/                Python environment for replays
└── work/                 replay work directories (verifiers refuse paths inside the checkout)
```

The checkout directory is named `upstream/`, which clashes with the repository's
own `upstream/` folder (the pinned manuscript snapshot). Inside these docs,
`upstream/` means the checkout unless a path says otherwise.

Branches for upstream PRs must start from `origin-upstream/main`, never from
the fork's `main`, so `plan/` stays out of them. See [docs/pins.md](docs/pins.md).

## Tickets

Work is tracked in [`tickets/`](tickets/README.md). Start with T00–T02. They
produce the replay environment and the evaluator that every later ticket uses
to decide what is worth searching.

## Ground rules (inherited from upstream CONTRIBUTING)

- Never modify upstream sources in place. Pin every input by commit and sha256.
- Preserve attribution for every construction we build on. Disclose
  substantial AI assistance.
- Report results as conditional finite certificates. Do not describe them as a
  formal proof of the multiplication theorem.
- Pushing branches, opening PRs and commenting upstream are outward-facing.
  Confirm with the project owner first.
