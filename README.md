# model-data

Last updated: 2026-11-10

Prepare reproducible datasets and shards for independent model consumers.

**Status: planned.** This repository contains specifications and an
implementation backlog. It has no executable engine or installable package.

## Independent use

Read [the component specification](docs/specs/README.md) and
[dataset preparation backlog](docs/specs/backlog.md). The first implementation
should prepare a tiny local dataset without Lab, a GPU, or a tokenizer when
the task does not need tokenization.

## Ownership

Dataset ingestion, normalization, filtering, deduplication, split construction,
mixing, document/shard manifests, packing, dataset lineage, and data cards.

Tokenizer training, vocabulary/special-token policy, artifact inspection,
compression experiments, and tokenizer comparisons belong to
[model-tokenizers](https://github.com/alvarovillalbaa/model-tokenizers). Model-data may encode and pack data using an
explicitly selected, hash-pinned tokenizer artifact; it does not train or
silently replace that tokenizer.

[model-distillation](https://github.com/alvarovillalbaa/model-distillation) owns teacher-registry, task,
teacher-response, verifier-result, and preference-pair contracts. Model-data owns
dataset/document/shard schemas and preserves an external producer's records
without becoming their semantic owner.

## Compose

Use independently, or register a pinned version in
[Lab](https://github.com/alvarovillalbaa/lab). The boundary is explicit dataset
and optional tokenizer artifact references; no sibling checkout is required.

[Specification](docs/specs/README.md) ·
[Extraction provenance](docs/sources/lab-provenance.json) ·
[Tokenizer boundary migration](docs/sources/tokenizer-boundary-map.json)

MIT applies to the authored code and documentation. External datasets, tokenizer
artifacts, models, and dependencies retain their own terms.
