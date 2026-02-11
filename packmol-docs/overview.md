# Packmol Overview

Packmol builds initial molecular configurations for simulations by optimizing molecule positions and orientations
subject to geometric constraints and minimum-distance tolerances.

## Core capability

- Input: one structure file per molecule type (`pdb`, `xyz`, or `tinker`), molecule counts, and region constraints.
- Output: packed structure in `pdb` or `xyz` (and optionally `crd`).
- Objective: simultaneously satisfy:
  - inter-atomic distance tolerance (`tolerance`), and
  - user constraints (`inside`, `outside`, `fixed`, planes, cylinders, etc.).

## Typical use

- Solvation boxes and slabs.
- Multi-component mixtures.
- Systems with fixed solutes plus mobile solvent/ions.
- Layered or spherical assemblies with atom-level orientation constraints.

## Important behavior

- Packmol internally optimizes using GENCAN with iterative loops.
- It first performs a constraint-focused stage and then full packing stages.
- Success is judged with both distance and constraint residuals.

## Repository map

- Main executable entry: `app/packmol.f90`
- Input parsing and defaults: `src/getinp.f90`, `src/setsizes.f90`
- Initialization and cell setup: `src/initial.f90`
- Objective and gradients: `src/computef.f90`, `src/computeg.f90`, `src/fparc.f90`, `src/comprest.f90`
- Heuristics for hard cases: `src/heuristics.f90`
- Real input examples: `testing/input_files/*.inp`
