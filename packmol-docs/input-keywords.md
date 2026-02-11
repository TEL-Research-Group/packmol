# Packmol Input Keywords

This file summarizes high-impact keywords for geometry generation.

## Required global keys

- `tolerance <real>`: mandatory minimum-distance target.
- `output <file>`: mandatory output filename.
- `filetype pdb|xyz|tinker`: defaults to `pdb` when omitted.

## Global optimization/control keys

Defaults are set in `src/getinp.f90`.

- `seed <int>`: default `1234567`; `-1` uses current time.
- `precision <real>`: default `1e-2`, success threshold for both `fdist` and `frest`.
- `maxit <int>`: default `20` GENCAN iterations per optimization call.
- `nloop <int>`: default `200 * ntype` for full packing loops.
- `nloop0 <int>`: default `20 * ntype` for constraint-only stage.
- `writeout <seconds>`: default `10`.
- `discale <real>`: default `1.1`, temporary radius scale in early loops.
- `movefrac <real>`: default `0.05`, fraction of worst molecules moved by heuristic.
- `movebadrandom`: move worst molecules to random positions.
- `disable_movebad`: disable move-bad heuristic.
- `packall`: skip per-type-first ordering and pack all together from start.
- `check`: only write initial approximation and stop.
- `writebad`: allow writing intermediate non-improving structures.

## Spatial and periodic keys

- `pbc Lx Ly Lz` means box `[0,0,0] -> [Lx,Ly,Lz]`.
- `pbc xmin ymin zmin xmax ymax zmax` uses explicit min/max bounds.
- `sidemax <real>`: default `1000`, coarse global pre-bound for initialization.
- `fbins <real>`: linked-cell bin tuning parameter (default `sqrt(3)`).

## Structure block keys

Inside each:

```text
structure file.pdb
  number N
  ... constraints ...
end structure
```

Common keys:

- `number <int>`
- region constraints: `inside`/`outside` for `box`, `cube`, `sphere`, `ellipsoid`, `cylinder`
- plane constraints: `above`/`over plane ...`, `below plane ...`
- `fixed x y z alpha beta gamma`
- `atoms i [j ...]` ... `end atoms` for atom-specific constraints
- `constrain_rotation x|y|z center spread`
- per-structure `nloop`, `nloop0`, `maxmove`
- restart keys: `restart_from <file>`, `restart_to <file>`

## Atom overlap tuning keys

- `radius <real>`
- `fscale <real>`
- `short_radius <real>`
- `short_radius_scale <real>`
- global short-distance controls: `use_short_tol`, `short_tol_dist`, `short_tol_scale`

## PDB output convenience keys

- `resnumbers`
- `connect`
- `changechains`
- `chain`
- `segid`
- `add_amber_ter`, `amber_ter_preserve`
- `hexadecimal_indices`
- `ignore_conect`, `non_standard_conect`
