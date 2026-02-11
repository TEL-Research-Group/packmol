# Constraints and Regions

Packmol supports whole-molecule and atom-level constraints.

## Region primitives

- `inside box xmin ymin zmin xmax ymax zmax`
- `outside box xmin ymin zmin xmax ymax zmax`
- `inside/outside cube xmin ymin zmin side`
- `inside/outside sphere cx cy cz radius`
- `inside/outside ellipsoid cx cy cz a b c scale`
- `inside/outside cylinder x0 y0 z0 dx dy dz radius length`
- `above|over plane a b c d`
- `below plane a b c d`

## Atom-level constraints

Use within a structure:

```text
atoms 1 2
  above plane 0. 0. 1. 12.
end atoms
```

This is essential for orientation control in bilayers and curved assemblies.

## Fixed molecules

`fixed x y z alpha beta gamma` places a molecule at a rigid pose.

Important restrictions:

- Fixed structures must have `number 1`.
- Fixed structures cannot use `restart_from` or `restart_to`.
- With PBC enabled, fixed atoms must lie inside PBC bounds after transformation.

## Periodic systems

When `pbc` is set, Packmol automatically adds an inside-box constraint for non-fixed atoms.

For slab-like or partitioned systems under PBC, combine `pbc` with plane/sphere constraints rather than only large inside-box regions.
