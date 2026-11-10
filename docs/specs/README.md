# model-data specification

Last updated: 2026-11-10

Status: planned. All execution capabilities below remain unimplemented.

## Responsibility

Own dataset/document/shard preparation: ingestion, rights/source records,
normalization, filtering, exact/fuzzy deduplication, frozen train/validation/test
splits, mixing, manifests, deterministic sharding, packing, and data cards.

Tokenizer training and research are owned by
[model-tokenizers](https://github.com/alvarovillalbaa/model-tokenizers). Teacher/task/verifier/preference record
semantics are owned by [model-distillation](https://github.com/alvarovillalbaa/model-distillation). The
[data schema scope](../../data/schemas/README.md) records these boundaries.

## Target standalone interface

| Operation | Explicit inputs | Intended outputs |
| --- | --- | --- |
| Prepare dataset | Source revisions/content hashes, data rights, preprocessing/filter configuration, split policy, seeds | Curated records and dataset/document manifests with lineage and split identity |
| Encode and pack, when needed | Prepared dataset manifest and a selected tokenizer artifact reference with revision/hash | Encoded/packed shards and manifests binding the exact dataset, tokenizer, and packing configuration |

These are target capabilities, not installed commands or a stable wire schema.
A dataset pipeline can run without tokenizer processing. When tokenization is
requested, consume the selected artifact through its declared backend/interface;
do not fit a tokenizer, change its special-token IDs, or infer a mutable latest
revision inside dataset preparation.

## Next work

- [ ] Implement one tiny local ingestion/filter/dedup path.
- [ ] Define frozen splits and deterministic dataset/document/shard manifests.
- [ ] Preserve source rights, input/output hashes, configuration, and split lineage.
- [ ] Add optional encoding/packing using a pinned tokenizer artifact.
- [ ] Demonstrate independent use before adding corpus-scale dependencies.

[Inherited data blueprint](blueprint.md) retains original data requirements.
Tokenize/pack steps there mean consuming a chosen tokenizer; tokenizer training
and comparison requirements now have their own owner. Historical provider/data
statements there are not newly verified facts.

[Dataset backlog](backlog.md) ·
[Preserved pre-split source](../sources/pre-tokenizer-split/README.md)

## Acceptance

The first implementation must declare its dependencies, run outside Lab and
sibling checkouts, include a useful local example and focused checks, and show
that dataset preparation can omit tokenizers entirely. An encoding/packing
example must retain the supplied tokenizer revision and content hash.
