# Upstream landscape (snapshot 2026-10-13)

Upstream: https://github.com/CrocSwap/integer-mult-bounds (Apache-2.0,
maintained by Douglas Colkitt). The work is conditional on the OpenAI
*Integer multiplication below n log n* framework (#109) and retains its
analytic, all-size/compiler, realization, hosting, precision/tape and
bit-interface (H1–H5) assumptions.

## Selected result: #942

- κ = 1661960547713947/10¹⁸. Cold replay: `make frontier942-verify`
  (needs a C++17 compiler, Boost headers, `numpy sympy scipy`).
- Record: `certificates/selected-result.json`. Assembly:
  `research/community-frontier942-audit/ASSEMBLY.json`.
- Complex endpoint 0.001664727258740678855772 (**binding**). Bit endpoint
  0.001733427039589844234749 (#589 on #555, unchanged).
- Lineage: Jeremy Kothe's U8 word (#869/#870), Hao Yan's owner construction
  (#858), Chafik Boukhalfa's #890 T21 composition, Jonathan Capalbo's T37
  packing.
- 779-bit complex prefix, charged 1024 bits. The bit side is charged 512.
  Physical row coefficient 17495 < 20161.
- **Known obstruction:** #942's all-replica bound shows that, for the fixed U8
  word, capacities, splitting rule and outer recipe, no positive replica count
  improves on T37 at the 10⁻¹⁸ grid. Gains need a different word, a
  different capacity or a different splitting rule.

## Open frontier claims (unreviewed)

| PR | Author | κ claimed | Mechanism |
|---|---|---|---|
| #1056 | rohanarun | 0.001672267698427438 | whole-helper exchanges on the T16 owner map (parent #1050) |
| #1055 | jeremykothe2 | 0.001672251604432734 | improved T16 owner packing, seven-slot k8 word |
| #1053/#1050/#1031/#1028 | jeremykothe2 | 0.00167216–0.00167225 | earlier steps of the same line |
| #1022 | — | 0.001672081255752945 | sixteen-replica seven-slot word |
| #1018 | — | 0.00167166528321877 | triangle hybrid (on #987) |
| #1005 / #1004 | jeremykothe2 | 0.001671387… / 0.001664233… | mutable-leaver all-K cells, U8 hybrids, frame re-optimisation on #799 word |
| #1030 | AlexS-scale | 0.00166202617947539 | two rank-seven helper ends on U8 (helpers 588/589 finish in dim 7) |
| #1060 | aliromman | — | exact complex P111 COPY word with a smaller paid recursive moment |

The seven-slot k8 / T16 line is about 0.62% above #942. Its chain is
#1005 → #1018 → #1022 → … → #1050 → #1056.

## Mechanisms that do *not* move κ today

- Bit-circuit ADD reductions (prefix resynthesis #904/#936/#952, frame
  schedules, helper stars #967, R420/R480 circuits). The bit supplier is not
  binding, and these changes leave the recursive rank histogram unchanged.
- Outer-recipe tuning. κ already equals ⌊s/(1+s)⌋ to within 10⁻¹⁸.
- Precision interface work (#877, #905, #951, #1025, #1054). These are
  interface contributions and do not install a new supplier.

## Useful upstream entry points

- `docs/research/current-status.md`: current selection and review status.
- `docs/research/pr-ledger.md`: per-PR review state.
- `docs/research/community-batch952-review.md`: review of #942 and its obstructions.
- `docs/research/community-batch970-*.md`: latest review batches.
- `CONTRIBUTING.md`: submission requirements.
