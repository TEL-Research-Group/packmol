# Workflows and CLI

## Execution modes

Packmol supports:

- stdin redirection:

```bash
packmol < input.inp
```

- explicit input file:

```bash
packmol -i input.inp
```

- explicit input and output override:

```bash
packmol -i input.inp -o output.pdb
```

## Build/install options

- `make` (default optimized flags include `-O3 -march=native -funroll-loops`)
- `cmake`
- `fpm install --profile release`
- `pip install packmol` or `uvx packmol`

## Iterative workflow for robust packing

1. Create minimal input with one structure type and broad region.
2. Run with fixed `seed`.
3. Add additional structure blocks gradually.
4. Introduce orientation constraints (`atoms`) only after feasibility is confirmed.
5. For difficult systems, save checkpoints with `restart_to` and continue via `restart_from`.
6. Final run with desired counts and full constraints.

## Minimal templates

Single box:

```text
tolerance 2.0
filetype pdb
output output.pdb

structure water.pdb
  number 1000
  inside box -20. -20. -20. 20. 20. 20.
end structure
```

Periodic slab partition:

```text
tolerance 2.0
filetype pdb
output output.pdb
pbc 45. 45. 45.

structure water.pdb
  number 500
  below plane 0.0 0.0 1.0 20.0
end structure

structure water.pdb
  number 500
  over plane 0.0 0.0 1.0 25.0
end structure
```
