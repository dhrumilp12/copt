# copt

A small C project to explore compiler optimizations by building and comparing different optimization levels (e.g., `-O0` vs `-O3`) and their outputs. The repository includes source code, build rules, test script(s), prebuilt reference binaries, and logs to help validate behavior across optimization settings.

## Table of Contents
- Overview
- Repository layout
- Build
- Run
- Testing and validation
- Artifacts and logs
- Development notes
- License

## Overview

This project centers around `copt.c`, a C program intended to be compiled under different optimization flags and then executed to observe behavioral and performance differences. You can build locally using the provided `Makefile`, run the resulting binaries, and compare outputs to reference binaries. A PDF (`copt.pdf`) appears to provide report or documentation about the project.

## Repository layout

- [copt.c](https://github.com/dhrumilp12/copt/blob/main/copt.c) — Main C source file.
- [Makefile](https://github.com/dhrumilp12/copt/blob/main/Makefile) — Build rules to compile the project.
- [test_orig.sh](https://github.com/dhrumilp12/copt/blob/main/test_orig.sh) — Test script to run the binaries and collect outputs/logs.
- [copt.pdf](https://github.com/dhrumilp12/copt/blob/main/copt.pdf) — Report or documentation PDF for the project.
- [._copt.pdf](https://github.com/dhrumilp12/copt/blob/main/._copt.pdf) — Auxiliary/metadata file (may be an artifact from macOS Finder).
- [copt_O0](https://github.com/dhrumilp12/copt/blob/main/copt_O0) — Prebuilt binary compiled with `-O0`.
- [copt_O3](https://github.com/dhrumilp12/copt/blob/main/copt_O3) — Prebuilt binary compiled with `-O3`.
- [copt_O0_ref](https://github.com/dhrumilp12/copt/blob/main/copt_O0_ref) — Reference binary for `-O0`.
- [copt_O3_ref](https://github.com/dhrumilp12/copt/blob/main/copt_O3_ref) — Reference binary for `-O3`.
- [mine_O0.log](https://github.com/dhrumilp12/copt/blob/main/mine_O0.log) — Log from running your `-O0` build.
- [mine_O3.log](https://github.com/dhrumilp12/copt/blob/main/mine_O3.log) — Log from running your `-O3` build.
- [ref_O0.log](https://github.com/dhrumilp12/copt/blob/main/ref_O0.log) — Log from running the reference `-O0` binary.
- [ref_O3.log](https://github.com/dhrumilp12/copt/blob/main/ref_O3.log) — Log from running the reference `-O3` binary.
- [.gitattributes](https://github.com/dhrumilp12/copt/blob/main/.gitattributes) — Git attributes configuration.

## Build

Requirements:
- GCC (or compatible C compiler)
- Make

Build steps:
1. Clone the repository:
   ```sh
   git clone https://github.com/dhrumilp12/copt.git
   cd copt
   ```
2. Use the `Makefile` to build:
   ```sh
   make
   ```
   This should produce binaries for different optimization levels (e.g., `copt_O0`, `copt_O3`). If your environment requires specific flags or targets, inspect and adjust the `Makefile` accordingly.

Manual build (example):
```sh
# Build with no optimizations
gcc -O0 -o copt_O0 copt.c

# Build with aggressive optimizations
gcc -O3 -o copt_O3 copt.c
```

## Run

Execute the binaries directly:
```sh
./copt_O0
./copt_O3
```

If your program expects input arguments or reads from stdin, pass them as needed. Refer to `copt.c` for the exact interface if unsure.

## Testing and validation

Use the provided script to run and compare outputs:
```sh
bash test_orig.sh
```

The script is expected to:
- Run your built binaries (`copt_O0`, `copt_O3`)
- Optionally run the reference binaries (`copt_O0_ref`, `copt_O3_ref`)
- Capture outputs to log files for comparison

After running, check the generated or updated logs:
- mine_O0.log vs ref_O0.log
- mine_O3.log vs ref_O3.log

A simple diff can help verify equivalence:
```sh
diff -u ref_O0.log mine_O0.log
diff -u ref_O3.log mine_O3.log
```

## Artifacts and logs

Prebuilt/reference binaries:
- `copt_O0`, `copt_O3` — Current builds (or example artifacts)
- `copt_O0_ref`, `copt_O3_ref` — Reference builds to compare against

Logs:
- `mine_O0.log`, `mine_O3.log` — Output from your local builds
- `ref_O0.log`, `ref_O3.log` — Output from reference binaries

If outputs differ, investigate:
- Compiler version differences
- Undefined behavior in code that optimization may expose
- Platform-specific behavior (e.g., floating-point, library versions)

## Development notes

- Primary code changes happen in `copt.c`.
- If adding new tests or inputs, consider updating `test_orig.sh` to automate runs and log generation.
- Keep `Makefile` targets consistent for reproducible optimization comparisons.

## License

No explicit license file is present. If you intend others to use or modify this project, consider adding a LICENSE file (e.g., MIT, Apache-2.0, GPL-3.0) to clarify terms.

---
For questions or improvements, open an issue or PR. Refer to [copt.pdf](https://github.com/dhrumilp12/copt/blob/main/copt.pdf) for background or detailed write-up if applicable.
