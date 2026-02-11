---
name: packmol-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in packmol; it prioritizes documentation references and then source inspection only for unresolved details.
---

# packmol: Inputs and Modeling

## High-Signal Playbook

### Route the request
- Route non-core topics to `packmol-advanced-topics` (performance tuning, build/CLI, quickstart, deep geometry semantics).

### Triage questions
- Which structure files are used, and are they valid for selected `filetype`?
- Is packing periodic (`pbc`) or non-periodic?
- Which region primitives are needed (`box`, `sphere`, `cylinder`, planes)?
- Are atom-level orientation constraints required (`atoms ... end atoms`)?
- Are there fixed molecules, and if so, are their poses/PBC bounds valid?
- Is reproducibility needed (`seed`) while tuning inputs?

### Canonical workflow
1. Define global controls: `tolerance`, `filetype`, `output`, and fixed `seed`.
2. Add structure blocks one by one with `number` and broad constraints.
3. For oriented assemblies, add atom-specific plane/sphere constraints.
4. Add explicit `pbc` for periodic systems.
5. Validate with small counts first; then scale counts upward.
6. If parser or feasibility issues appear, inspect `testing/input_files` patterns and troubleshooting docs.

### Minimal working example

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

### Pitfalls
- `fixed` structures must use `number 1`.
- Fixed structures cannot use `restart_from`/`restart_to`.
- In PBC mode, fixed atoms must be inside PBC bounds.
- Inconsistent constraints can fail before distance optimization (`nloop0` stage).
- Missing or invalid residue/chain options can affect downstream PDB expectations.
- Forgetting reproducible `seed` during tuning makes comparisons noisy.

### Convergence/validation checklist
- Constraints are physically feasible with requested counts.
- `fdist` and `frest` are both below `precision` at completion.
- Region semantics (`inside` vs `outside`) match intended geometry.
- Output coordinates satisfy expected box/shape occupancy.

## Scope
- Handle input syntax, molecule setup, and spatial constraint construction.
- Keep guidance concrete and example-driven.

## Primary documentation references
- `packmol-docs/input-keywords.md`
- `packmol-docs/examples-from-testing.md`
- `packmol-docs/troubleshooting.md`

## Workflow
- Start from primary references.
- If details are missing, inspect `references/doc_map.md`.
- Reuse closest `testing/input_files/*.inp` example instead of inventing from scratch.
- Escalate to source only for parser/runtime edge cases using `references/source_map.md`.

## Tutorials and examples
- `testing`

## Test references
- `testing`

## Optional deeper inspection
- `app`
- `python`
- `src`

## Source entry points for unresolved issues
- `src/setsizes.f90`
- `src/getinp.f90`
- `src/input.f90`
- `src/comprest.f90`
- `src/pbc.f90`
- `app/packmol.f90`
- Prefer targeted source search (for example: `rg -n "inside|outside|fixed|atoms|tolerance|pbc|nloop" app python src`).
