# Primary references

1. Yang, Z., Qi, P., Zhang, S., Bengio, Y., Cohen, W. W., Salakhutdinov, R. and Manning, C. D. (2018). *HotpotQA: A Dataset for Diverse, Explainable Multi-hop Question Answering*. EMNLP. [Paper](https://doi.org/10.18653/v1/D18-1259).
2. HotpotQA authors. [Official dataset, download links, citation and data license](https://hotpotqa.github.io/). [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). Dataset text is not bundled.
3. HotpotQA authors. [Official evaluator](https://github.com/hotpotqa/hotpot/blob/master/hotpot_evaluate_v1.py) and [repository](https://github.com/hotpotqa/hotpot). Referenced for metric behavior; implementation equivalence has not been independently checked.
4. Sentence Transformers. [all-MiniLM-L6-v2 model card](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2). Reported encoder revision: `c9745ed1d9f207416be6d2e6f8de32d1f16199bf`.
5. Sentence Transformers Cross-Encoders. [ms-marco-MiniLM-L6-v2 model card](https://huggingface.co/cross-encoder/ms-marco-MiniLM-L6-v2). Reported reranker revision: `c5ee24cb16019beea0893ab7796b1df96625c6b8`.
6. Qwen Team. [Qwen2.5-7B-Instruct model card](https://huggingface.co/Qwen/Qwen2.5-7B-Instruct). The experiment reports a separately obtained Q4_K_M GGUF; that exact file's origin is not established by the base model card.
7. llama.cpp maintainers. [Runtime repository](https://github.com/ggml-org/llama.cpp). The study records build b9672 and short commit `74ade5274`; the binary was not inspected for this release.

The original numerical source is the author's four-page technical report dated 11 November 2026. It is not an external independent confirmation of the reported run. Source hierarchy and discrepancies are documented in [PROVENANCE.md](PROVENANCE.md).
