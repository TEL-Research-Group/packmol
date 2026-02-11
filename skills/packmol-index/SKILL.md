---
name: packmol-index
description: This skill should be used when users ask how to use packmol and the correct generated documentation skill must be selected before going deeper into source code.
---

# packmol Skills Index

## Route the request
- Select one topic skill first; avoid broad answers from this index.
- Prioritize docs-first guidance and only inspect source for unresolved details.

## Generated topic skills
- `packmol-inputs-and-modeling`: core input syntax, constraints, region design, and molecule setup.
- `packmol-advanced-topics`: consolidated quickstart, build/install/CLI, performance tuning, and advanced geometry semantics.

## Fast routing hints
- Building or debugging input files -> `packmol-inputs-and-modeling`
- Runtime/convergence tuning -> `packmol-advanced-topics`
- Build/package/CLI questions -> `packmol-advanced-topics`
- Advanced constraint semantics -> `packmol-advanced-topics`
- New-user quickstart -> `packmol-advanced-topics`

## Documentation-first inputs
- `packmol-docs`

## Tutorials and examples roots
- `testing`

## Test roots for behavior checks
- `testing`

## Escalate only when needed
- Start from the target skill's primary references.
- If details are missing, inspect the target skill doc maps:
  - `skills/packmol-inputs-and-modeling/references/doc_map.md`
  - `skills/packmol-advanced-topics/references/doc_map.md`
- If docs are still insufficient, inspect the corresponding source maps:
  - `skills/packmol-inputs-and-modeling/references/source_map.md`
  - `skills/packmol-advanced-topics/references/source_map.md`
- Suggested source search baseline: `rg -n "<symbol_or_keyword>" app python src`

## Source directories for deeper inspection
- `app`
- `python`
- `src`
