# Dataset manifests

Last updated: 2026-11-10

Planned manifests bind dataset/document/shard identity, source revision and
rights, frozen split membership, preprocessing/filter versions, row/document
counts, and content hashes. Output order and shard construction must be
deterministic under the recorded configuration and seeds.

Token counts apply only when encoding is requested. An encoded/packed shard
also references the exact tokenizer artifact revision and hash supplied by
[model-tokenizers](https://github.com/alvarovillalbaa/model-tokenizers) or another compatible tokenizer producer.
Preparing a non-tokenized dataset does not require a tokenizer or invented
token counts. Actual large datasets and artifacts remain outside Git.
