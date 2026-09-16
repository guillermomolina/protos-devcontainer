# Protos Dev Container Agent Guidelines

## Repository purpose

`guillermomolina/protos-devcontainer` owns the ready-to-use development
environment for running and experimenting with released Protos versions.

This repository is a companion product. It does not own the Protos language,
runtime, specification, formal project lifecycle, or durable project-record
architecture.

## Cross-repository Protos authority

```text
OPERATIONAL_PROTOS_PROJECT_AUTHORITY = guillermomolina/protos
NORMATIVE_PROTOS_AUTHORITY           = guillermomolina/protos/spec
DURABLE_PROTOS_PROJECT_RECORDS       = guillermomolina/protos-project-docs:docs/project/**
DEVCONTAINER_PRODUCT_AUTHORITY       = guillermomolina/protos-devcontainer
```

Formal Protos work items remain coordinated in `guillermomolina/protos`.
Required durable, non-normative Protos project records belong in
`guillermomolina/protos-project-docs`.

This repository remains authoritative for devcontainer configuration,
`versions.json`, container bootstrap behavior, curated environment snapshots,
devcontainer-specific documentation, and product-local build/release evidence.

Do not duplicate formal Protos Issues or durable project records here.

## Product boundary

The container consumes released Protos/runtime/editor products; it must not
silently redefine their semantics or compatibility contracts for convenience.

- Do not patch Protos language/runtime semantics inside the container.
- Do not invent a different supported runtime contract from the selected Protos
  release.
- Do not maintain an independent Protos grammar or extension implementation.
- Keep consumed Protos and VS Code extension versions explicit and reproducible.
- Route Protos language/runtime/specification defects to
  `guillermomolina/protos`.
- Route extension-product defects to
  `guillermomolina/protos-vscode-extension`.

If a formal Protos work item requires a devcontainer change, publish the product
change here first, then let the durable Protos project record reference the exact
devcontainer revision or immutable artifact identity.

## Repository workflow

Keep repository changes scoped to the devcontainer product. Do not repair
unrelated caller state, do not force-push, and stage only intended files.

Documentation and policy-only changes require at minimum:

```text
git diff --check
```

Run container/build validation when executable devcontainer behavior changes.

## Language

Repository documentation, configuration comments, commit messages, and
maintained product metadata are written in English except where test/sample data
requires another language.
