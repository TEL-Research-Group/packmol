# Packmol Performance Playbook

This guidance focuses on faster convergence for initial geometry generation.

## How convergence is judged

Packmol stops successfully when both are below `precision`:

- `fdist`: maximum violation of minimum atom distance.
- `frest`: maximum violation of geometric constraints.

`precision` default is `1e-2`.

## High-impact tuning order

1. Validate feasibility first:
   - Ensure regions can physically contain requested molecules.
   - Use `check` to inspect initial point quickly.
2. Keep constraints simple for first solve:
   - Start with broad regions, then tighten.
3. Use explicit `pbc` for periodic systems:
   - Avoid ambiguity in effective box boundaries.
4. Increase loop budgets before extreme parameter changes:
   - Raise `nloop0` if constraint fitting fails.
   - Raise `nloop` if overlap removal stagnates.
5. Tune loop aggressiveness:
   - `discale` controls temporary expanded exclusion radii.
   - `movefrac` and `maxmove` control how many worst molecules are relocated.
6. Use deterministic seeds while iterating:
   - Set `seed` to a fixed integer for reproducible tuning.

## Defaults that matter

- `nloop = 200 * ntype` if unset.
- `nloop0 = 20 * ntype` if unset.
- `maxit = 20` GENCAN iterations per internal call.
- `movefrac = 0.05`.
- `discale = 1.1`.

## Fast failure diagnostics

- If constraint-only stage fails (`nloop0` exhausted): constraints likely inconsistent or too tight.
- If full stage stalls: try larger `nloop`, slightly larger `discale`, and larger `movefrac`.
- If system is large and packing is unexpectedly slow: review `sidemax`, PBC definition, and region fragmentation.

## Practical strategies for hard systems

- Start with fewer molecules and scale up.
- Solve solvent-only first, then add solute/fixed components.
- Use `restart_to` and `restart_from` to continue from best intermediate states.
- For layered or vesicle systems, prefer atom-specific orientation constraints (`atoms ...`) over highly coupled global constraints.
