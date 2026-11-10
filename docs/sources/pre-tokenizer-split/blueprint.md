# Inherited model-data blueprint

Last updated: 2026-11-10

Historical design extracted from [Lab at ba67e51](https://github.com/alvarovillalbaa/lab/blob/ba67e510bab2703b1042993744ce099490221c1f/docs/specs/steps.md). The component specification owns current scope. This text does not prove implementation, current provider facts, or executed research.

# 7. Phase 3 — data pipeline

Data will decide most of the model quality. Treat data as the main research object.

## 7.1 Start from open corpora

Use a mix like:

| Source                                             | Use                                          |
| -------------------------------------------------- | -------------------------------------------- |
| FineWeb sample/full                                | web backbone                                 |
| Dolma                                              | open reproducible corpus                     |
| code datasets with permissive licenses             | coding                                       |
| Wikipedia / books / papers where licensing permits | knowledge and long-form                      |
| synthetic instruction data                         | post-training, not base pretraining at first |
| your own generated tasks                           | distillation/self-improvement                |

FineWeb is useful because it releases both a large cleaned/deduplicated corpus and reproduction code; Dolma gives a transparent open-data baseline and toolkit. ([Hugging Face][4])

## 7.2 Data processing steps

For each document:

1. normalize Unicode
2. strip boilerplate
3. detect language
4. remove extremely short/long garbage
5. remove duplicated paragraphs
6. exact dedup
7. fuzzy dedup
8. quality score
9. toxicity/safety/PII tagging
10. domain classification
11. license/source tracking
12. tokenize
13. pack into fixed-length sequences
14. shard into deterministic files
15. build manifest with hashes

Manifest example:

```json
{
  "shard_id": "fineweb_en_000123",
  "source": "fineweb",
  "tokens": 104857600,
  "documents": 392144,
  "language": "en",
  "dedup_version": "minhash_v03",
  "quality_filter": "qclf_v02_threshold_0.72",
  "license": "ODC-BY-1.0",
  "sha256": "..."
}
```

## 7.3 Build three data mixes

Do not use one mix. Use three:

| Mix                  | Purpose                             |
| -------------------- | ----------------------------------- |
| `baseline_mix`       | mostly FineWeb/Dolma-style          |
| `quality_mix`        | stricter quality filters, less data |
| `reasoning_code_mix` | more code/math/science              |

Run all three at **124M/350M scale** before choosing the 1B/3B mix.

## 7.4 Data research opportunity

Your first publishable research contribution could be:

> “A cheap multi-stage data filter that improves downstream score per training dollar.”

Use DCLM-style controlled evaluation: same model, same tokens, same compute, only data filter changes. DCLM exists exactly because data curation can be studied systematically across model scales. ([DataComp][5])

---

# 8. Phase 4 — tokenizer

Train your own tokenizer, even if you later compare against an existing one.

## Recommended tokenizer plan

| Parameter       | Recommendation                                             |
| --------------- | ---------------------------------------------------------- |
| Type            | BPE or Unigram                                             |
| Vocab size      | 32k for small models, 50k–64k for 1B+                      |
| Training sample | 10B–50B characters from final data mix                     |
| Special tokens  | BOS, EOS, PAD, UNK, system/user/assistant if chat          |
| Code support    | ensure indentation and common code tokens are handled well |
| Evaluation      | compression ratio by domain                                |

Tokenizer eval table:

| Dataset slice | chars/token | tokens/doc | unknown rate | notes |
| ------------- | ----------: | ---------: | -----------: | ----- |
| web           |             |            |              |       |
| code          |             |            |              |       |
| math          |             |            |              |       |
| Spanish       |             |            |              |       |
| tables        |             |            |              |       |

Even if the final model is English-heavy, include multilingual slices in tokenizer testing so you understand the tradeoff.

---
