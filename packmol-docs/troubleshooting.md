# Troubleshooting

## Frequent input errors

- `Output file not (correctly?) specified`: missing `output` line.
- `Overall tolerance not set`: missing `tolerance` line.
- `Keyword not recognized`: typo or unsupported key.
- `Structure specification not ending with "end structure"`: malformed block.

## Constraint and geometry failures

- Constraint-only stage fails (`nloop0` exhausted): constraints likely incompatible with molecule geometry.
- Fixed molecule outside PBC bounds: adjust `fixed` pose or PBC box.
- Very dense target region: reduce molecule count or expand region.

## Convergence failures

If Packmol ends without perfect packing:

- Increase `nloop` first.
- Increase `nloop0` if restraints are the bottleneck.
- Set a different deterministic `seed` and retry.
- Start from best checkpoint using `restart_from`.

Packmol can emit a forced output (`*_FORCED`) for post-minimization workflows when exact tolerance is not reached.

## Reproducibility tips

- Use explicit `seed <int>` during development.
- Avoid `seed -1` when comparing outputs across runs.
- Prefer the same invocation mode (`stdin` vs `-i/-o`) during regression tests.
