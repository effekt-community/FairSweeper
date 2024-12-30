# FairSweeper

## Table of contents

- [FairSweeper](#fairsweeper)
  - [Table of contents](#table-of-contents)
  - [Setup](#setup)
  - [Progress](#progress)
    - [Week 4/5 -31.12.2024](#week-45--31122024)
    - [Week 3](#week-3)
    - [Week 2](#week-2)
    - [Week 1](#week-1)
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

On Windows some characters won't show correctly in the CLI to fix this you can follow this [post](https://stackoverflow.com/questions/57131654/using-utf-8-encoding-chcp-65001-in-command-prompt-windows-powershell-window/57134096#57134096) (does not work for my Win10 Laptop idk)

## Progress

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