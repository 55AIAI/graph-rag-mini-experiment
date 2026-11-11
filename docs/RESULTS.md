# Results and metric definitions

All recorded experimental values on this page were transcribed from the author's *Graph_RAG_Technical_Report.pdf*, dated 11 November 2026, pages 2–4. They have not been recomputed from predictions for this publication. CSVs preserve the displayed decimal precision, not unavailable full-precision underlying scores.

## Metrics

Let G be the set of annotated supporting sentence IDs and P the IDs surviving final context packing.

| Metric | Definition |
| --- | --- |
| Answer EM | Exact equality after case, punctuation, article and whitespace normalization |
| Answer F1 | Macro average of per-question answer token-overlap F1; categorical yes/no/noanswer handling |
| Complete evidence | Indicator that every sentence in G appears in P |
| Supporting-sentence recall | Per-question fraction of G retained in P, then averaged |
| Mean context tokens | Mean packed Qwen context token count including headers |
| Failure rate | Predefined malformed, incomplete, overflow or token-limited outputs; scored zero |

For overlap F1, precision is overlapping answer tokens / predicted tokens, recall is overlapping tokens / gold tokens, and F1 is their harmonic mean. Repeated tokens require multiset overlap. The [official evaluator](https://github.com/hotpotqa/hotpot/blob/master/hotpot_evaluate_v1.py) is the reference for benchmark normalization, but equivalence of the unavailable project evaluator has not been checked.

All five answer conditions retain all 200 questions in the denominator. The report records zero failed outputs. Evidence coverage measures label overlap, not truth, faithfulness or the validity of alternative evidence paths.

## Main answer conditions

| Condition | n | Complete evidence | EM | F1 | Failed | Mean context tokens |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| BM25 + reranking | 200 | 68.0% | 37.000% | 47.233% | 0 | 702.0 |
| Dense + reranking | 200 | 67.0% | 34.000% | 44.833% | 0 | 700.6 |
| Mention graph + reranking | 200 | 71.0% | 37.000% | 46.933% | 0 | 703.1 |
| Closed book | 200 | N/A | 4.500% | 6.515% | 0 | 0.0 |
| Oracle supporting sentences | 200 | N/A | 49.500% | 64.119% | 0 | 149.0 |

The oracle is a privileged control with shorter curated context, not a budget-matched method or a strict mathematical upper bound.

## Primary paired comparison

Graph minus dense answer F1, percentage points:

| Resampling unit | Difference | Reported 95% interval |
| --- | ---: | --- |
| Questions | +2.100 | [-0.0667, +4.6667] |
| Connected source clusters | +2.100 | [-0.1684, +4.6435] |

Both use 2,000 bootstrap resamples with seed 20261029. Source clustering reportedly yields 198 clusters, maximum size two. Resamples must pair the same questions across methods. These intervals include zero and are conditional on this sample; a reliable directional advantage has not been established.

## Evidence-only ablation

| Route | Complete evidence | Supporting-sentence recall | Mean context tokens |
| --- | ---: | ---: | ---: |
| BM25 | 48.5% | 73.25% | 690.0 |
| BM25 + reranking | 68.0% | 84.33% | 702.0 |
| Dense | 51.5% | 74.07% | 692.7 |
| Dense + reranking | 67.0% | 83.08% | 700.6 |
| Graph | 67.0% | 81.54% | 700.4 |
| Graph + reranking | 71.0% | 85.17% | 703.1 |

Non-reranked rows are retrieval-only ablations; no separate answer EM/F1 is available for those conditions.

## Evidence and answer association

| Retrieved condition | Complete: n | Complete: EM-correct | Incomplete: n | Incomplete: EM-correct |
| --- | ---: | ---: | ---: | ---: |
| BM25 + reranking | 136 | 61 | 64 | 13 |
| Dense + reranking | 134 | 57 | 66 | 11 |
| Graph + reranking | 142 | 63 | 58 | 11 |

The count totals give EM values of 37%, 34% and 37%. These arithmetic consistency checks are possible without the original predictions. Relative to dense, the report says the graph gains complete evidence on 12 questions and loses it on four, a net eight (4 percentage points). It also reports 36 abstentions among the graph's 142 complete-evidence cases.

These observed groups do not identify causal effects of evidence completeness, reasoning failure or context dilution. Secondary comparisons and selected cases are exploratory and not multiplicity-corrected.

## Table format

CSV percentage columns use a 0–100 scale; `*_pp` columns use percentage points. Empty complete-evidence cells for controls mean not applicable, not zero. F1 is rounded to three decimal places as printed in the report. Machine-readable files are under [results/](../results).
