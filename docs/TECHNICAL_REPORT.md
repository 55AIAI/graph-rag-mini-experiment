# Evidence completeness and answer quality in graph-assisted RAG

Prepared for repository publication on 12 November 2026.

## Abstract

This report summarizes an author's recorded local experiment comparing sparse, dense and graph-assisted retrieval for multi-hop question answering. All three retrieved conditions use the same cross-encoder, packing constraints and local Qwen generator. A deterministic split of HotpotQA development distractor data provides 50 tuning and 200 reserved questions, whose passages form a shared pool of 2,485 documents. Reported complete-evidence coverage is 68% for BM25, 67% for dense and 71% for the graph route. Answer F1 is 47.233%, 44.833% and 46.933%, respectively. The graph-minus-dense difference is +2.100 percentage points, with both reported 95% bootstrap intervals including zero. The study motivates separating retained evidence from answer correctness; it does not establish a reliable directional answer-quality improvement.

**Evidence status:** the numbers and runtime settings below are transcribed from the technical report dated 11 November 2026. Original source files, predictions and gold-row manifests were unavailable for independent recomputation during this publication.

## Research question

Does a cheap title-mention passage graph improve the retention of complete annotated supporting evidence and answer quality compared with dense retrieval, under shared downstream processing?

Two observations must be distinguished: retrieving all annotated supporting sentences and generating the correct answer from the packed context. Annotation overlap is an operational benchmark measure, not proof of general factual grounding.

## Design

The source is HotpotQA development distractor v1. IDs are ordered by the SHA-256 digest of `20261029:<id>`; the first 50 form a tuning set and the next 200 the reserved set. All selected context and distractor passages form one shared corpus. The reserved questions comprise 159 bridge and 41 comparison items. This pooled search task differs from both the official ten-paragraph distractor task and full-Wikipedia search.

The graph uses normalized exact title mentions in sentences, with sentence provenance. Shared-entity and title-mention links yield an undirected passage graph. High-incidence entities are filtered at more than 30 documents. The recorded graph contains 1,362 mention triples and 3,230 edges. It is a lexical mention graph, without verified semantic relations or LLM extraction.

## Compared conditions

| Condition | Candidate selection / context | Role |
| --- | --- | --- |
| BM25 + reranking | Sparse lexical ranking, top 20 to common reranker | Sparse baseline |
| Dense + reranking | Normalized all-MiniLM-L6-v2 similarity, top 20 | Dense baseline |
| Mention graph + reranking | Dense-seeded propagation fused with dense ranks, top 20 | Graph-assisted route |
| Closed book | No retrieved context, prior-knowledge instruction | Control |
| Oracle supporting sentences | All annotated supporting sentences | Privileged control |

The common cross-encoder is ms-marco-MiniLM-L6-v2. Whole-sentence packing permits up to five passages, 256 Qwen tokens per passage, and 1,024 context tokens including headers. The generator is Qwen2.5-7B-Instruct Q4_K_M through llama.cpp on a Windows laptop with a recorded RTX 3050 Ti 4 GB GPU. Greedy grammar-constrained generation permits at most 128 output tokens and returns one JSON answer field.

The report records 1,000 logical evaluations (five conditions times 200 questions), 716 unique model inputs, reuse of exact duplicate responses and zero failed outputs. Logical evaluations are not independent model calls.

## Results

| Condition | Complete evidence | EM | F1 | Failed outputs |
| --- | ---: | ---: | ---: | ---: |
| BM25 + reranking | 68.0% | 37.000% | 47.233% | 0 |
| Dense + reranking | 67.0% | 34.000% | 44.833% | 0 |
| Mention graph + reranking | 71.0% | 37.000% | 46.933% | 0 |
| Closed book | N/A | 4.500% | 6.515% | 0 |
| Oracle supporting sentences | N/A | 49.500% | 64.119% | 0 |

The primary graph-minus-dense macro F1 difference is **+2.100 percentage points**. Its reported paired question-bootstrap 95% interval is **[-0.0667, +4.6667] pp**; its source-cluster interval is **[-0.1684, +4.6435] pp**. Both include zero. Bootstrap uses 2,000 resamples and seed 20261029; source clustering reportedly produces 198 connected components of maximum size two.

Before reranking, graph evidence completeness is 67.0% versus dense 51.5%; after reranking these become 71.0% and 67.0%. These ablations measure evidence retention only: non-reranked routes do not have separate reported answer-generation runs.

## Interpretation

The graph has a higher observed evidence-completeness rate but a small, unresolved answer-F1 difference from dense retrieval. BM25's higher observed F1 shows why a lexical baseline matters in this experiment. Neither graph superiority nor general inferiority can be concluded from one small sample.

For graph retrieval, 63 of 142 complete-evidence cases and 11 of 58 incomplete-evidence cases have an exact-match answer. Thus, complete annotation coverage is neither sufficient nor necessary for EM success under these definitions. Annotation omissions, answer aliases, prior knowledge and model behavior may all contribute.

The manuscript uses an evidence-to-answer decomposition and labels part of the oracle gap “context dilution.” In this public report those comparisons are treated only as descriptive associations. The oracle has shorter, curated contexts; no intervention isolates context dilution or reasoning failure. Similar average context lengths also do not imply equivalent context content.

## Limits

- One generator, one small development-derived sample and modest retrievers.
- Corpus pooling is partly transductive and is not an official evaluation setting.
- A title-mention graph lacks alias resolution and semantic relation verification.
- Supporting labels can omit valid evidence; EM/F1 can penalize valid aliases.
- Encoder truncation differs from Qwen-token packing.
- Graph weight was reportedly selected using an earlier MiniLM-token packing pilot, then transferred to Qwen packing.
- Human review is incomplete; secondary subgroup analyses are exploratory.
- The original implementation and journal have not been inspected or rerun for this release.
- The manuscript and technical report disagree on seed weighting; see [provenance](PROVENANCE.md).

## Reproducibility boundary

This repository makes the study design and reported numerical claims inspectable. It does not yet provide computational reproduction. Recovering the original code, split manifest, prompts, predictions, environment lock and model identities is required before independent re-scoring or fresh inference can be claimed.

See [architecture](ARCHITECTURE.md), [dataset](DATASET.md), [results](RESULTS.md), [reproduction requirements](REPRODUCIBILITY.md) and [primary references](REFERENCES.md).
