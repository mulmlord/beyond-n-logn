# Tickets

GitHub issues on [mulmlord/beyond-n-logn](https://github.com/mulmlord/beyond-n-logn/issues)
are the source of truth for status and discussion. The tracking issue is
[#13](https://github.com/mulmlord/beyond-n-logn/issues/13). The files here are
the original ticket text. If a scope change lands in an issue, mirror it here.

| Ticket | Title | Depends on | Phase |
|---|---|---|---|
| [T00](T00-environment-and-baseline-replay.md) · [#1](https://github.com/mulmlord/beyond-n-logn/issues/1) | Environment and cold replay of #942 | — | Foundation |
| [T01](T01-replay-open-frontier.md) · [#2](https://github.com/mulmlord/beyond-n-logn/issues/2) | Replay the strongest open claim (#1056 chain) | T00 | Foundation |
| [T02](T02-kappa-evaluator-and-sensitivity.md) · [#3](https://github.com/mulmlord/beyond-n-logn/issues/3) | κ evaluator and profile sensitivity tool | T00 | Foundation |
| [T03](T03-t16-packing-ceiling.md) · [#4](https://github.com/mulmlord/beyond-n-logn/issues/4) | Ceiling for the T16 seven-slot owner-packing family | T01, T02 | Go/no-go |
| [T04](T04-owner-map-search.md) · [#5](https://github.com/mulmlord/beyond-n-logn/issues/5) | Owner-map search beyond #1056 | T01, T02, T03 | Quick win |
| [T05](T05-rank7-ends-on-k8-word.md) · [#6](https://github.com/mulmlord/beyond-n-logn/issues/6) | Port rank-seven helper ends (#1030) onto the k8 word | T01, T02 | Composition |
| [T06](T06-frontier-triage.md) · [#7](https://github.com/mulmlord/beyond-n-logn/issues/7) | Triage open PRs for profile-changing mechanisms | T02 | Composition |
| [T07](T07-word-level-search.md) · [#8](https://github.com/mulmlord/beyond-n-logn/issues/8) | Word-level search to cut rank-48 residual mass | T02, T03, T06 | Research |
| [T08](T08-compose-and-admit.md) · [#9](https://github.com/mulmlord/beyond-n-logn/issues/9) | Compose winning changes and run strict admission | T04 and/or T05, T07 | Integration |
| [T09](T09-independent-verification.md) · [#10](https://github.com/mulmlord/beyond-n-logn/issues/10) | Independent re-verification of our candidate | T08 | Integration |
| [T10](T10-upstream-submission.md) · [#11](https://github.com/mulmlord/beyond-n-logn/issues/11) | Package and submit the upstream PR | T08, T09, T11 | Delivery |
| [T11](T11-upstream-sync.md) · [#12](https://github.com/mulmlord/beyond-n-logn/issues/12) | Upstream frontier sync (recurring) | — | Ongoing |

## Critical path

```
T00 ─┬─ T01 ─┬─ T03 ─┬─ T04 ─┐
     │       └─ T05 ─┼───────┼─ T08 ─ T09 ─ T10
     └─ T02 ─┬─ T06 ─┴─ T07 ─┘
             └──────────────────(used by every search ticket)
T11 runs throughout and gates T10.
```

T04 and T05 are the cheapest routes to a new κ. T07 is the route to a
gain that is not just a small increment. T03 decides how much effort T04 deserves.
