# model-data specification

Last updated: 2026-11-10

Status: planned. All runtime capabilities below remain planned.

## Responsibility

Ingestion, normalization, filters, deduplication, tokenization, packing, sharding, provenance, and data cards.

## First next work

- [ ] Implement deterministic manifests with exact source/split references and content hashes.
- [ ] Build a tiny local preprocessing path before adding large corpus tooling.
- [ ] Preserve licenses, validation splits, and lineage at every transformation.

## Interfaces and composition

Specify the smallest public API against the first real consumer before implementing it. Use explicit inputs, artifacts, versions, and dependency declarations. A planned interface is not an implementation.

[Inherited blueprint](blueprint.md) preserves the relevant original design sections. Provider claims, dates, estimates, and unimplemented features there are historical requirements, not new measurements.

[Inherited backlog](backlog.md) records the original planning status; use the implementation status above for the current boundary.

## Acceptance

The first implementation must install/run independently, declare dependencies, include a useful example and focused behavior checks, and record remaining limitations. Do not mark this project implemented solely because the documentation exists.
