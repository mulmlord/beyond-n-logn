# Replays

## #942 cold replay: PASS (2026-10-13)

`make frontier942-verify` at upstream `abdc6a70`, in the environment described
in [environment.md](environment.md).

```
PASS_T37_STRICT_WITH_SOURCE_BOUND_ANCESTRY 0.001661960547713947
PASS_COMPLETE_PR942_COMPOSITION 0.001661960547713947
```

- **Cold rebuild**: `reused_completed_baseline = false`. The #799 baseline and its
  #741 ancestry were rebuilt from source, not reused.
- **Counts match the #942 review**: 167,832 helper roles, 333 calls, a 779-bit
  prefix charged at 1024 bits, physical row coefficient 17495.
- **Cost**: 1918 s wall clock (32 min), with peak system memory around 16.8 GB
  (including other processes on the machine; sampled every 15 s).
- Receipt: [receipts/frontier942-cold-20261013.json](receipts/frontier942-cold-20261013.json).

| Stage | Seconds |
|---|---:|
| baseline799-cold | 1408.9 |
| u8-native | 338.7 |
| strict | 64.1 |
| discovery | 63.2 |
| check-parent | 13.9 |
| independent-owners | 10.3 |
| final-binding | 5.6 |
| build-parent | 4.2 |
| frozen-construction | 2.2 |
| other six stages | < 1 each |

### Reusing the baseline

About 73% of the time goes to rebuilding the #799 baseline. Later replays can
pass the checked baseline instead of rebuilding it. The verifier rechecks it
with `check_selected` before reuse:

```sh
# P = project dir, as in environment.md
PATH="$P/.venv/bin:$PATH" python3 -B "$P/upstream/scripts/verify_frontier942.py" \
  --work "$P/work/<fresh-dir>" \
  --baseline799 "$P/work/integer-mult-frontier942.PBXIxp/replay/replay/baseline799"
```

Receipts produced this way record `reused_completed_baseline = true` and must
be reported as reuse, not as cold replays. The 92 MB work directory is kept
in `$P/work/` (outside the checkout) for this purpose.
