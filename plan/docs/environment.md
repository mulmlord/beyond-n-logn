# Replay environment

| Component | Version |
|---|---|
| OS | Omarchy (Arch-based), Linux 7.2.5-3-omarchy x86_64 |
| CPU / RAM | AMD Ryzen 7 7840HX, 24 threads / 30 GB |
| C++ | GCC 16.2.1 20260810 (`c++`/`g++`); clang 22.1.8 also present |
| Boost | 1.92.0 (pacman `boost`, headers in `/usr/include/boost`) |
| Make | GNU Make 4.4.1 |
| Python | CPython 3.14.7 in `.venv` (uv) |
| Python packages | numpy 2.5.4, sympy 1.14.0, scipy 1.18.1 |

## Setup

```sh
sudo pacman -S --needed boost
uv venv .venv --python 3.14
uv pip install --python .venv/bin/python numpy sympy scipy
```

## Running a replay

Verifiers refuse work directories inside the checkout, so use `work/` in the
project directory (see the layout in [../README.md](../README.md)):

```sh
P=$(git -C <checkout> rev-parse --show-toplevel)/..   # project dir
PATH="$P/.venv/bin:$PATH" TMPDIR="$P/work" make -C "$P/upstream" frontier942-verify
```

Use absolute paths in scripted runs. A relative `cd upstream` did not land in
the checkout in one of our background runs.

## Results

See [replays.md](replays.md).
