---
name: packmol-advanced-topics
description: This skill should be used when users ask about advanced or secondary Packmol topics outside core input authoring, including getting started, performance tuning, constraints deep dives, and build/CLI details.
---

# packmol: Advanced Topics

## High-Signal Playbook

### Route the request
- Use `packmol-inputs-and-modeling` first for most input-file construction/debugging.
- Use this skill when the request is primarily about:
  - onboarding and quickstart workflow,
  - performance/convergence tuning,
  - advanced constraint semantics, or
  - build/install/CLI behavior.

### Triage questions
- Is the user blocked by parser/setup issues, convergence/runtime, or geometry semantics?
- Is the request about execution environment (build/CLI) rather than input chemistry?
- Does the user need deterministic reproducibility while tuning (`seed` policy)?
- Is PBC active, and are fixed molecules or atom-level constraints involved?

### Canonical workflow
1. Confirm baseline run mode (`packmol < input.inp`, `packmol -i`, or `packmol -i/-o`).
2. If convergence issue: classify whether `frest` (constraints) or `fdist` (overlap) dominates.
3. Tune loops in order: `nloop0` (constraint fitting), then `nloop`, then `maxit`.
4. Tune aggressiveness conservatively (`discale`, `movefrac`) with fixed `seed`.
5. Use `restart_to`/`restart_from` for iterative continuation.
6. For geometric assemblies, validate region semantics and atom-level constraints before adding complexity.

### Minimal working examples

Quickstart execution:

```bash
packmol < input.inp
```

Convergence tuning snippet:

```text
precision 0.01
nloop0 200
nloop 800
maxit 40
discale 1.15
movefrac 0.08
seed 1024
restart_to run.restart
```

### Pitfalls
- Random seed mode (`seed -1`) while tuning causes non-reproducible comparisons.
- Large `nloop` without fixing infeasible constraints wastes runtime.
- Over-constrained atom-level regions can make packing impossible.
- Fixed molecules outside PBC bounds fail early.
- Confusing CLI invocation modes can mask input/output filename mistakes.

### Convergence/validation checklist
- `frest < precision` and `fdist < precision` at successful completion.
- Output coordinates satisfy intended occupancy/geometry.
- Loop and seed settings are recorded for reproducibility.
- For failed runs, checkpoint or forced output strategy is explicit.

## Scope
- Consolidated advanced topics to reduce routing surface.
- Covers quickstart, build/install/CLI, performance tuning, and advanced geometry semantics.

## Primary documentation references
- `packmol-docs/overview.md`
- `packmol-docs/workflows-and-cli.md`
- `packmol-docs/performance-playbook.md`
- `packmol-docs/constraints-and-regions.md`

## Workflow
- Start from the most relevant primary reference above.
- If details are missing, inspect `references/doc_map.md`.
- Reuse `testing/input_files/*.inp` and `testing/test_cli.sh` patterns before source inspection.
- Escalate to source only for unresolved behavior using `references/source_map.md`.

## Tutorials and examples
- `testing`

## Test references
- `testing`

## Optional deeper inspection
- `app`
- `python`
- `src`

## Source entry points for unresolved issues
- `app/packmol.f90`
- `src/getinp.f90`
- `src/initial.f90`
- `src/heuristics.f90`
- `src/comprest.f90`
- `src/cli_parser.f90`
- `src/checkpoint.f90`
- `src/output.f90`
- `Makefile`
- `CMakeLists.txt`
- `fpm.toml`
- Prefer targeted source search (for example: `rg -n "nloop|nloop0|maxit|precision|inside|outside|fixed|constrain_rotation|-i|-o" app python src`).
