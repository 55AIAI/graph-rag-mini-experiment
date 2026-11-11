# Dataset and split

## Source and attribution

The experiment uses **HotpotQA development distractor v1**, distributed by the dataset authors. Obtain it from the [official HotpotQA website](https://hotpotqa.github.io/) using its development distractor download link.

The official site states the dataset is distributed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). Dataset licensing is distinct from licensing the official evaluator or this project's implementation. This repository redistributes no dataset rows or derived passage text.

Citation: Zhilin Yang, Peng Qi, Saizheng Zhang, Yoshua Bengio, William W. Cohen, Ruslan Salakhutdinov and Christopher D. Manning (2018). *HotpotQA: A Dataset for Diverse, Explainable Multi-hop Question Answering*. EMNLP. [DOI](https://doi.org/10.18653/v1/D18-1259).

## Recorded local selection

| Item | Reported value |
| --- | ---: |
| Original file | hotpot_dev_distractor_v1.json |
| Source records | 7,405 |
| Source bytes | 46,320,117 |
| Split seed | 20261029 |
| Tuning questions | 50 |
| Reserved questions | 200 |
| Reserved bridge / comparison | 159 / 41 |
| Shared selected passage corpus | 2,485 |

The technical report describes ordering all question IDs by SHA-256 of the UTF-8 string `20261029:<id>`, taking the first 50 for tuning and the next 200 for evaluation. Their supplied context and distractor passages form the shared search corpus. Exact tie handling, passage deduplication, sentence normalization and corpus IDs must be checked against the original code.

The original source hash is reportedly recorded in an unavailable `data/PROVENANCE.json`; its value was not printed in the technical report. File size alone cannot establish source identity. No hash or split manifest is invented here.

## Evaluation boundary

- Every method searches the same pooled corpus, including passages associated with the selected reserved questions.
- This is a partly transductive, development-derived local task.
- It is not the official ten-paragraphs-per-question distractor setting or full-Wikipedia retrieval.
- Its metrics are not directly comparable to official leaderboard scores.
- Gold answers and supporting-fact labels should be excluded from indexing, graph construction and ranking.
- Previously inspected reserved questions should not be treated as fresh unseen data for later tuning.

## What is needed for recovery

Recover the original source hash, exact ordered ID manifest, passage mapping and dataset-construction code. Then download the official dataset, verify its identity, reconstruct every selected row and compare the entire result to the recovered manifest. This publication does not claim that this validation has been performed.
