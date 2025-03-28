> [!NOTE]
> This is a community-maintained fork of a MIT-licensed student project in the *Effective Programming with Effects* course in winter semester 2024/2025.
> Be warned that this is not an officially endorsed project, the code in this repository may be not idiomatic Effekt.
> 
> The original repository is https://github.com/TheDying0fLight/FairSweeper

# FairSweeper

## Table of contents

- [FairSweeper](#fairsweeper)
  - [Table of contents](#table-of-contents)
  - [Setup](#setup)
  - [Progress](#progress)
    - [Extra](#extra)
    - [Week 6/7 1.1.2025 - 16.1.2025](#week-67-112025---1612025)
    - [Week 4/5 -31.12.2024](#week-45--31122024)
    - [Week 3](#week-3)
    - [Week 2](#week-2)
    - [Week 1](#week-1)
  - [Development](#development)
    - [FFI](#ffi)
  - [Useful commands](#useful-commands)
    - [Effekt commands](#effekt-commands)
    - [Nix-related commands](#nix-related-commands)
  - [Example projects using this template](#example-projects-using-this-template)
  - [Repository structure](#repository-structure)
  - [CI](#ci)
  - [Used Template](#used-template)
  - [Related](#related)

---

## Setup

The game can be run by using the the VS _Effekt_ extension. You have to download the newest version of Effekt and click
on the _Run_ button above the _main_ function in the _main.effekt_ file. The game will start in a terminal with
instructions on how to play

On Windows some characters won't show correctly in the CLI to fix this you can follow this [post](https://stackoverflow.com/questions/57131654/using-utf-8-encoding-chcp-65001-in-command-prompt-windows-powershell-window/57134096#57134096) (does not work for my Win10 Laptop idk)

## Progress

### Extra
- changed grid to 1-D array improving speed by up to 3x (4.3.2025)

### Week 6/7 1.1.2025 - 16.1.2025
- See https://github.com/TheDying0fLight/FairSweeper/pull/38

### Week 4/5 -31.12.2024
- See https://github.com/TheDying0fLight/FairSweeper/pull/34

### Week 3
- See https://github.com/TheDying0fLight/FairSweeper/pull/23

### Week 2
- See https://github.com/TheDying0fLight/FairSweeper/pull/22

### Week 1
- some simple tests
- Board
- CLI interactions
- print board
- reveal squares and propagate through field until bombs are nearby
- working bombs
- flag squares

## Development

All relevant files are contained in the _src_ folder.

Core files:
- _board_: The board and solver logic
- _boards_: Boards for tests and difficulty presets
- _main_: User interaction logic
- _utils_: Some helper functions mainly used for board and solver logic

The _benchmark.effekt_ file contains a function to test the speed of the solver and some statistics from previous tests.

_test.effekt_ contains a few tests to test the correctness and speed of solvers

In _solver.effekt_ is a unused and incomplete alternative to the currently used _getProbabilities_ function in _board.effekt_. There is a possibility to combine the two solver functions for more efficient solution finding.

### FFI

Currently only _BigInt_ with some related functions is implemented through FFI it is used when finding possible moves
by finding all possible boards. It stores the amount of possible boards on which a mine is placed on relevant fields.

## Useful commands

### Effekt commands

Run the main file:
```sh
effekt src/main.effekt
```
This (like many other Effekt commands) uses the JavaScript backend by default.
To use a different backend, add the `--backend <backend>` flag.

Run the tests:
```sh
effekt src/test.effekt
```

Open the REPL:
```sh
effekt
```

Build the project:
```sh
effekt --build src/main.effekt
```
This builds the project into the `out/` directory, creating a runnable file `out/main`.

To see all available options and backends, run:
```sh
effekt --help
```

### Nix-related commands

While Nix installation is optional, it provides several benefits:

Update dependencies (also runs automatically in CI):
```sh
nix flake update
```

Open a shell with all necessary dependencies:
```sh
nix develop
```

Run the main entry point:
```sh
nix run
```

Build the project (output in `result/bin/`):
```sh
nix build
```

## Example projects using this template

- [`effekt-stm`](https://github.com/jiribenes/effekt-stm)
- This very project!

## Repository structure

- `.github/workflows/*.yml`: Contains the [CI](#ci) definitions
- `src/`: Contains the source code
  - `main.effekt`: Main entry point
  - `test.effekt`: Entry point for tests
  - `lib.effekt`: Library code imported by `main` and `test`
- `flake.nix`: Package configuration in a Nix flake
- `flake.lock`: Auto-generated lockfile for dependencies
- `LICENSE`: Project license
- `README`: This README file

## CI

Two GitHub Actions are set up:

1. `flake-check`:
   - Checks the `flake.nix` file, builds and tests the project
   - Runs on demand, on `main`, and on PRs
   - To run custom commands, add a step using:
     - `nix run -- <ARGS>` to run the main entry point with the given arguments
     - `nix develop -c '<bash command to run>'` to run commands in the correct environment

2. `update-flake-lock`:
   - Updates package versions in `flake.nix`
   - Runs on demand and weekly (Tuesdays at 00:00 UTC)

## Used Template
[Effekt Template](https://github.com/jiribenes/effekt-template)

## Related
- [JS Fairsweeper](https://github.com/pwmarcz/kaboom/tree/master)
- [SAT SMT](https://smt.st/SAT_SMT_by_example.pdf)
- [Very fast Probability Solver](https://www.reddit.com/r/Minesweeper/comments/6oli70/new_probability_algorithm_info_in_comments/)
