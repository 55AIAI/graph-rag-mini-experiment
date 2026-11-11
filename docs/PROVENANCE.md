# Provenance and uncertainty

## Sources used for this publication

1. **Primary numerical source:** author's `Graph_RAG_Technical_Report.pdf`, prepared 11 November 2026, four pages. Pages 1–2 describe data and settings; page 3 contains the main, ablation and association tables; pages 3–4 report intervals, interpretation and release limits.
2. **Secondary cross-check:** `CASJ2026_Article_final.docx`, eleven-page manuscript. Used to compare rounded main results and identify methodological discrepancies. Its private author questionnaire and contact information are excluded.
3. **Primary external sources:** official HotpotQA website/evaluator and model cards, linked in [references](REFERENCES.md). These verify asset identities and attribution; they do not independently verify this experiment's results.

Both source documents were read for this publication. Neither source document is redistributed. The original archive, code and journal were not inspected, and this publication does not independently confirm their stated validation history.

## Source discrepancies and interpretation

| Topic | Technical report | Manuscript | Treatment here |
| --- | --- | --- | --- |
| Dense-seed weights | Softmax temperature 0.1 | Equal seed mass | Both recorded; exact executed behavior unresolved |
| Original release contents | Describes code, tests, journal and reproduction commands | Describes study | Those artifacts are unavailable in this repository |
| Explanation of oracle gap | Causal mechanism not isolated | Uses “context dilution” language | Report associations only; no causal attribution |
| F1 precision | Three decimal places | Rounded to one decimal | Use technical-report precision and label it rounded |
| BM25 | Explicit tokenizer/IDF description | “Lucene settings” | Do not claim Lucene was the implementation |

The model identity strings below are copied from the technical report. They have not been checked against actual downloaded weights or binaries in this publication.

## Reported identities

| Item | Recorded identity |
| --- | --- |
| Embedder | sentence-transformers/all-MiniLM-L6-v2 |
| Embedder revision | c9745ed1d9f207416be6d2e6f8de32d1f16199bf |
| Reranker | cross-encoder/ms-marco-MiniLM-L6-v2 |
| Reranker revision | c5ee24cb16019beea0893ab7796b1df96625c6b8 |
| Generator | Qwen2.5-7B-Instruct Q4_K_M |
| GGUF SHA-256 | 2bada8a7450677000f678be90653b85d364de7db25eb5ea54136ada5f3933730 |
| Reference ZIP SHA-256 | 4952687ca03585da9c39f5672d6645c346e550e753524210b1155c7bf6051153 |
| Runtime | llama.cpp b9672; short commit 74ade5274 |
| Split/bootstrap seed | 20261029 |
| Bootstrap resamples | 2,000 |

The dataset source SHA-256 and quantized GGUF download source are not printed in the source report. A model name or digest does not establish a redistribution right or provide the missing file.

## Audit boundary

Verified during preparation: access to the source-document text; transcription consistency of main tables; aggregate arithmetic and local document links.

Not independently verified: inference execution, graph extraction, data leakage prevention, exact selected rows, raw predictions, full-precision scores, bootstrap implementation, original code licensing and claimed prior local tests.

The source report calls its protocol internally frozen on 29 October 2026. This is not external preregistration; the protocol file itself was not recovered for this release.
