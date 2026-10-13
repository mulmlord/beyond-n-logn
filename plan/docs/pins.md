# Pins

## Upstream base

| Item | Value |
|---|---|
| Upstream | `CrocSwap/integer-mult-bounds` `main` |
| Fork | `mulmlord/beyond-n-logn` `main` = upstream `main` + `plan/` |
| Commit | `abdc6a7002abdbcd9e21bfc5e1a795784deacfdf` (2026-10-13T13:34:12-04:00, "Record 10 verified GitHub merge states for batch1047 checkpoint 2") |
| Selected result | #942, κ = 1661960547713947/10¹⁸ |
| `certificates/selected-result.json` sha256 | `1d35283cb0ce3f8db1f285683933517f9e87475d295e2b6316399ad9928c81c3` |
| `research/community-frontier942-audit/ASSEMBLY.json` sha256 | `4b2894956e594e408e111d806c842f2ed2c32aefcadff93fad69ff0b46f1991a` (matches `certificate_sha256` in the selected record) |

## Local checkout

```sh
cd ~/Projects
git clone git@github.com:mulmlord/beyond-n-logn.git
git -C beyond-n-logn remote add origin-upstream https://github.com/CrocSwap/integer-mult-bounds.git
mkdir beyond-n-logn-work
echo '.claude/' >> beyond-n-logn/.git/info/exclude   # local-only ignore
```

Replays pin the upstream commit above, not the fork's `main`. Run them from
a detached checkout of that commit, or check that `plan/` is the only
difference: `git diff --stat abdc6a70 main` should list only `plan/`.

## Syncing the fork

The fork's `main` carries `plan/`, so it can't be fast-forwarded. Merge
upstream into it instead. Upstream never touches `plan/`, so the merge
should not conflict. From the checkout root:

```sh
git fetch origin-upstream main
git switch main
git pull --ff-only origin main
git merge --no-edit origin-upstream/main
git push origin main
```

Push over SSH. `gh repo sync` is refused when upstream commits touch
`.github/workflows/` and the gh token lacks the `workflow` scope.

Pushes to the fork run upstream's workflows (Actions are enabled). A big sync
starts about 26 of them; a `plan/`-only change starts the four with no path
filter (`verify.yml`, `bit-elim-144.yml`, `bit-reuse-147.yml`,
`graded-box-convolution.yml`). Actions minutes are free on public repos.

## Branches for upstream PRs

```sh
git fetch origin-upstream main
git switch -c <topic> origin-upstream/main
```

Never branch from the fork's `main`. That would put `plan/` into the upstream PR.
