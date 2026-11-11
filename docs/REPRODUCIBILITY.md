# Reproducibility status

## What this release supports

A reader can inspect the reported design, architecture, aggregate tables and uncertainty statements, and check aggregate arithmetic. This release contains no implementation, dataset rows, prompts, raw model responses or per-question prediction journal. It cannot reproduce answer metrics, bootstrap intervals, graph statistics or fresh generation.

No new experiment or model inference was performed when preparing this repository. No remote CI success is claimed.

## Evidence inventory

| Artifact | Status in this repository | Consequence |
| --- | --- | --- |
| Technical summary and model identities | Included as transcribed documentation | Settings can be reviewed; implementation is unverified |
| Aggregate results | Included as Markdown and CSV | Reported values can be compared |
| Official dataset and model links | Included | Assets must be obtained from upstream |
| Original code and lockfiles | Unavailable / excluded | Pipeline execution cannot be verified |
| Source hash, split manifest and passage mapping | Unavailable | Exact data identity and selection cannot be checked |
| Prompt templates and grammar | Unavailable | Generator inputs cannot be reconstructed exactly |
| Per-question gold/prediction journal | Unavailable | EM/F1 and paired intervals cannot be recomputed |
| Native runtime and model binaries | Not redistributed | Fresh inference needs separately obtained files |

The source technical report refers to a larger export containing commands such as `python scripts/reproduce.py`, `scripts/verify_dataset.py` and `requirements-offline.lock.txt`. Those files are not present here. Its statements about that export are not claims about the contents or validation of this repository.

## Recovery sequence

1. Recover the original experiment export and verify its identity against the recorded ZIP SHA-256 in [provenance](PROVENANCE.md). Locate the frozen protocol and environment manifest.
2. Review code ownership, distribution permissions and third-party notices. Remove secrets, private paths, personal forms and unrelated files before any release.
3. Resolve the seed-weighting discrepancy by inspecting the frozen implementation and runtime configuration.
4. Recover the dataset source hash and exact split/corpus manifests. Obtain the official HotpotQA source, verify its hash and compare reconstructed rows.
5. Recover all 200 records for every condition, including question IDs, gold answers, predicted answers, raw responses, failure flags and packed sentence IDs. Check uniqueness, denominator completeness and duplicate-input reuse.
6. Run the recovered evaluator against the official normalization behavior. Recompute EM/F1, failure totals, coverage and the primary paired bootstrap intervals.
7. Publish the actual tested command, pinned dependency versions, artifact hashes and observed validation output.
8. Only then attempt fresh inference with the recorded GGUF and native runtime, documenting hardware and any numerical differences.

## Minimum journal fields

| Field | Purpose |
| --- | --- |
| question_id, condition | Pair methods and enforce one evaluation per question/condition |
| gold_answer, predicted_answer | Recompute answer metrics |
| raw_response, parse_status, failure_reason | Audit output handling |
| gold_supporting_sentence_ids, packed_sentence_ids | Recompute coverage |
| packed_context_token_count | Verify context budget |
| model_input_hash, response_cache_key | Audit exact duplicate reuse |
| prompt/config/runtime/model identifiers | Establish generation provenance |

A recovered journal may contain dataset-derived text. Its publication must preserve upstream attribution and license obligations; no journal is released here.

## Future evaluation

Once the original run is auditable, use a new untouched sample to test alias handling, stronger retrievers, graph variants and context selection. Keep these plans separate from completed measurements. Do not tune on the 200 already analyzed questions and continue calling them unseen.
