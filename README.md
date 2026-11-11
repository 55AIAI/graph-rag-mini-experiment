# Graph-assisted RAG: evidence completeness and answer quality

A small research study of whether a lightweight title-mention graph helps multi-hop question answering when the reranker, context budget and generator are shared.

**Release status:** documentation and reported aggregate results. The original experiment implementation, selected dataset and per-question journal are **not included**. Metrics were transcribed from the author's technical report dated 11 November 2026; they were not independently recomputed for this publication.

## Main finding

On 200 reserved questions in a local pooled HotpotQA setting, graph-assisted retrieval retained complete annotated evidence for **71%** of questions versus **67%** for dense retrieval. Answer F1 was **46.933%** versus **44.833%**. The reported paired 95% interval for the **+2.100 percentage-point** F1 difference includes zero. BM25 with the same reranker had the highest observed F1 of the retrieved conditions.

| Condition | Questions | Complete evidence | Answer EM | Answer F1 | Mean context tokens |
| --- | ---: | ---: | ---: | ---: | ---: |
| BM25 + reranking | 200 | 68.0% | 37.000% | 47.233% | 702.0 |
| Dense + reranking | 200 | 67.0% | 34.000% | 44.833% | 700.6 |
| Mention graph + reranking | 200 | 71.0% | 37.000% | 46.933% | 703.1 |
| Closed book | 200 | N/A | 4.500% | 6.515% | 0.0 |
| Oracle supporting sentences | 200 | N/A | 49.500% | 64.119% | 149.0 |

These are local development-derived results, not official HotpotQA leaderboard scores. Controls have different context construction and are not budget-matched retrieval methods.

## Read the study

| Document | Contents |
| --- | --- |
| [Technical report](docs/TECHNICAL_REPORT.md) | Research question, design, results and interpretation |
| [Architecture](docs/ARCHITECTURE.md) | Graph construction, ranking, shared reranker and generation |
| [Dataset](docs/DATASET.md) | Source, deterministic split, pooled corpus and attribution |
| [Results and metrics](docs/RESULTS.md) | Definitions, paired intervals, ablations and evidence counts |
| [Reproducibility](docs/REPRODUCIBILITY.md) | Available evidence, missing artifacts and recovery plan |
| [Provenance](docs/PROVENANCE.md) | Source hierarchy, discrepancies and model identities |
| [Publication scope](docs/RELEASE_SCOPE.md) | Included materials and disclosure boundaries |
| [References](docs/REFERENCES.md) | Primary dataset, evaluator and model sources |

Machine-readable tables: [main results](results/main_results.csv), [retrieval ablation](results/retrieval_ablation.csv), [paired intervals](results/paired_intervals.csv), [evidence association](results/evidence_association.csv).

## How to use this repository

Start with the technical report and architecture, then inspect the CSV tables. There is no installation or experiment execution command in this release: it contains no runnable experiment.

The immediate next step for computational reproducibility is to recover and review the original code and prediction journal, verify their identities, and only then release permitted artifacts and recompute the results. See the [reproduction boundary](docs/REPRODUCIBILITY.md).

## Disclosure and reuse

Only newly prepared documentation and aggregate numerical tables are published here. No dataset rows, question text, answers, model weights, original code, private forms or personal contact details are included. This publication does not grant a license to unavailable original project code or redistribute upstream model/data assets.
