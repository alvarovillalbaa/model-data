# Dataset preparation backlog

Last updated: 2026-11-10

This retains the original data-pipeline checklist from
[Lab](https://github.com/alvarovillalbaa/lab/blob/ba67e510bab2703b1042993744ce099490221c1f/docs/IMPLEMENTATION_BACKLOG.md). The tokenization item refers
to encoding with a selected, pinned tokenizer artifact; training and tokenizer
research are maintained by [model-tokenizers](https://github.com/alvarovillalbaa/model-tokenizers).
The [previous combined backlog](../sources/pre-tokenizer-split/backlog.md)
is historical evidence. This project remains planned.

## Data Pipeline

Status: planned.

- [ ] Manifest schema.
- [ ] Source ingestion.
- [ ] Unicode normalization.
- [ ] Boilerplate stripping.
- [ ] Language detection.
- [ ] Length filters.
- [ ] Paragraph dedup.
- [ ] Exact dedup.
- [ ] Fuzzy dedup.
- [ ] Quality scoring.
- [ ] Toxicity/safety/PII tagging.
- [ ] Domain classification.
- [ ] License/source tracking.
- [ ] Tokenization.
- [ ] Packing.
- [ ] Deterministic sharding.
