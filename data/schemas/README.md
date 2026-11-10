# Dataset schemas

Last updated: 2026-11-10

This component owns dataset, document, data-split, and shard manifest schemas.
They will identify source revisions and rights, transformations/filter versions,
record or shard counts, split membership, content hashes, and lineage.

When encoding/packing uses a tokenizer, the shard manifest references the exact
external tokenizer artifact revision and content hash. Tokenizer artifact
contents and training/inspection policy are owned by
[model-tokenizers](https://github.com/alvarovillalbaa/model-tokenizers).

Teacher-registry, task, teacher-response, verifier-result, and preference-pair
contracts are owned by [model-distillation](https://github.com/alvarovillalbaa/model-distillation). Do not duplicate
those types or reinterpret their eligibility/verification meaning here.
Imported records may be referenced or transported as data while retaining their
producer's version and provenance. No dataset wire schema is implemented yet.
