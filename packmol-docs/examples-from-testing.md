# Curated Examples From `testing/input_files`

Representative inputs already validated by repository tests.

## Basic boxes and mixtures

- `testing/input_files/water_box.inp`: canonical water box.
- `testing/input_files/mixture.inp`: water + urea in same region.

## Periodic systems

- `testing/input_files/water_box_pbc.inp`: cubic PBC box with implicit full occupancy.
- `testing/input_files/water_box_pbc_negative_coordinates.inp`: PBC with explicit min/max bounds.
- `testing/input_files/mixture_pbc.inp`: plane-partitioned mixture under PBC.

## Oriented assemblies

- `testing/input_files/bilayer.inp`: bilayer with atom-level plane constraints.
- `testing/input_files/spherical.inp`: multilayer spherical arrangement.

## Fixed-solute workflows

- `testing/input_files/solvprotein.inp`: fixed protein plus solvent and ions.
- `testing/input_files/solvprotein_pbc.inp`: fixed solute in periodic environment.

## Failure-mode references

- `testing/input_files/water_box_failed.inp`: intentionally under-iterated example.
- `testing/input_files/protein_outside_pbc_error.inp`: fixed molecule outside PBC error case.
