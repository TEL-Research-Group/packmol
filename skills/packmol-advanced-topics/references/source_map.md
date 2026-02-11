# packmol source map: Advanced Topics

Generated from source roots:
- `app`
- `python`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `build`
- `cli`
- `nloop`
- `nloop0`
- `maxit`
- `precision`
- `inside`
- `outside`
- `fixed`
- `constrain_rotation`

## Fast source navigation
- `rg -n "tolerance|output|seed|pbc|inside|outside|fixed|constrain_rotation|nloop|nloop0|maxit|precision" src/getinp.f90 app/packmol.f90`
- `rg -n "parse_command_line_args|command_argument_count|-i|-o" src/cli_parser.f90`
- `rg -n "movebad|restart_from|restart_to|checkpoint" src/initial.f90 src/heuristics.f90 src/checkpoint.f90`

## Suggested source entry points
- `app/packmol.f90` (main execution flow and optimization loop)
- `src/getinp.f90` (keyword parsing, defaults, and restrictions)
- `src/setsizes.f90` (input file parsing and type handling)
- `src/initial.f90` (initialization and constraint-only stage)
- `src/heuristics.f90` (move-bad heuristic)
- `src/comprest.f90` (constraint objective penalties)
- `src/cli_parser.f90` (CLI argument parsing)
- `src/checkpoint.f90` (failed-convergence handling)
- `src/output.f90` (output and restart writing)
- `python/packmol/cli.py` (Python entrypoint wrapper)
- `Makefile` (native build)
- `CMakeLists.txt` (CMake build)
- `fpm.toml` (fpm build)
