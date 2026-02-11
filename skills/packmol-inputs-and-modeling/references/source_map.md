# packmol source map: Inputs and Modeling

Generated from source roots:
- `app`
- `python`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `inside`
- `outside`
- `fixed`
- `atoms`
- `pbc`
- `nloop`
- `tolerance`

## Fast source navigation
- `rg -n "inside|outside|fixed|atoms|constrain_rotation|pbc" src/getinp.f90`
- `rg -n "ityperest|restpars|frest" src/comprest.f90 src/gwalls.f90`

## Suggested source entry points
- `src/setsizes.f90` (structure counting, filetype setup, `nloop` parsing)
- `src/getinp.f90` (keyword parsing and defaults)
- `src/input.f90` (global input state)
- `src/comprest.f90` (constraint penalty definitions)
- `src/gwalls.f90` (constraint gradients)
- `src/pbc.f90` (periodic wrapping and distance logic)
- `testing/input_files` (validated input patterns)
