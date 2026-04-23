# AI-Trainer-OBLIVION — Reading List
*Curated bibliography for course development · April 2026*

This is the research Shane needs to read before writing each module. Not required reading for students — this is the foundation for writing lessons that are correct.

---

## Core References (Read First)

These apply across all 10 planned topics:

- **Andrej Karpathy — "Let's build GPT: from scratch, in code, spelled out"** (YouTube, 2023)
  The best ground-truth explanation of what a language model is. Watch before writing anything.
  https://www.youtube.com/watch?v=kCc8FmEb1nY

- **Sebastian Raschka — "LLMs from Scratch"** (GitHub/Book, 2024)
  Companion book to Karpathy's work. Covers tokenization, attention, training loops.
  https://github.com/rasbt/LLMs-from-scratch

- **Hugging Face Course — NLP Course** (HuggingFace, free)
  Practical fine-tuning walkthrough. Good for verifying understanding of transformers.
  https://huggingface.co/learn/nlp-course

---

## By Module Topic

### OB-1.1 — Prompt-to-Weights Reasoning

- **"A Recipe for Training Neural Networks"** — Andrej Karpathy (blog, 2019)
  https://karpathy.github.io/2019/04/25/recipe/
  Core intuitions about loss, learning rate, and why things fail.

- **"Yes You Should Understand Backprop"** — Andrej Karpathy (blog, 2016)
  https://karpathy.medium.com/yes-you-should-understand-backprop-e2f06eab496b

- **"The Loss Landscape of Neural Network Training"** — Li et al. (2018)
  https://arxiv.org/abs/1712.09913
  Visual intuition for what the loss surface looks like and why SGD finds what it finds.

---

### OB-1.2 — Quantization Trade-offs

- **"GGUF format documentation"** — llama.cpp project
  https://github.com/ggerganov/llama.cpp/blob/master/docs/gguf.md

- **"Quantization"** — Hugging Face documentation
  https://huggingface.co/docs/transformers/quantization

- **TheBloke's model cards** — Practical Q4/Q5/Q8 comparison notes
  https://huggingface.co/TheBloke
  Search any model + "GGUF" and read the quant description section.

- **"GPTQ: Accurate Post-Training Quantization"** — Frantar et al. (2022)
  https://arxiv.org/abs/2210.17323

---

### OB-1.3 — Embedding-Space Geometry

- **"Word2Vec Explained"** — Sebastian Ruder (blog, 2016)
  http://sebastianruder.com/word-embeddings-1/
  Foundation for understanding why semantic similarity works at all.

- **"The Illustrated Word2vec"** — Jay Alammar (blog, 2019)
  https://jalammar.github.io/illustrated-word2vec/

- **"Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks"** — Reimers & Gurevych (2019)
  https://arxiv.org/abs/1908.10084
  Why sentence-level embeddings are different from token-level embeddings.

- **Nomic AI — nomic-embed-text model card**
  https://huggingface.co/nomic-ai/nomic-embed-text-v1.5
  This is the model running in Shane's Weaviate stack. Understand it deeply.

- **Weaviate documentation — Vector Search Concepts**
  https://weaviate.io/developers/weaviate/concepts/vector-index

---

### OB-2.1 — Training-Data Curation

- **"LIMA: Less Is More for Alignment"** — Zhou et al. (2023)
  https://arxiv.org/abs/2305.11206
  1,000 carefully selected examples matching a 65B model trained on 52K. The source of the 1,000-sample insight.

- **"Deduplication and the Quality of Training Data"** — Lee et al. (2022)
  https://arxiv.org/abs/2107.06499

- **"Alpaca format documentation"** — Stanford Alpaca project
  https://github.com/tatsu-lab/stanford_alpaca#data-release

---

### OB-2.2 — Synthetic Data Generation

- **"Phi-1: Textbooks Are All You Need"** — Gunasekar et al. / Microsoft (2023)
  https://arxiv.org/abs/2306.11644
  Foundational paper for synthetic data quality over quantity.

- **"Self-Instruct: Aligning Language Models with Self-Generated Instructions"** — Wang et al. (2023)
  https://arxiv.org/abs/2212.10560
  The technique underlying most synthetic data pipelines.

- **"WizardLM: Empowering Large Language Models to Follow Complex Instructions"**
  https://arxiv.org/abs/2304.12244
  Evol-Instruct: systematically increasing instruction complexity in synthetic data.

---

### OB-2.3 — Custom Modelfiles at Depth

- **Ollama Modelfile documentation** (official)
  https://github.com/ollama/ollama/blob/main/docs/modelfile.md

- **"Prompt Engineering Guide"** — DAIR.AI
  https://www.promptingguide.ai/

- **ChatML format specification** — OpenAI (2023)
  https://github.com/openai/openai-python/blob/main/chatml.md
  The chat template most modern models use.

---

### OB-2.4 — Fine-Tuning on Your Own Hardware

- **Unsloth documentation and fast-start guides**
  https://github.com/unslothai/unsloth
  Currently the most efficient fine-tuning library for consumer hardware.

- **Axolotl configuration guide**
  https://github.com/OpenAccess-AI-Collective/axolotl
  More configurable than Unsloth; better for production pipelines.

- **"Practical Tips for Finetuning LLMs Using LoRA"** — Sebastian Raschka (2023)
  https://magazine.sebastianraschka.com/p/practical-tips-for-finetuning-llms

- **llama.cpp fine-tuning (lora) documentation**
  https://github.com/ggerganov/llama.cpp/tree/master/examples/finetune
  Relevant for CPU-only or low-VRAM environments.

---

### OB-2.5 — LoRA / QLoRA

- **"LoRA: Low-Rank Adaptation of Large Language Models"** — Hu et al. (2021)
  https://arxiv.org/abs/2106.09685
  The original LoRA paper. Read it.

- **"QLoRA: Efficient Finetuning of Quantized LLMs"** — Dettmers et al. (2023)
  https://arxiv.org/abs/2305.14314
  The original QLoRA paper. Read it.

- **"Making LLMs even more accessible with bitsandbytes, 4-bit quantization and QLoRA"** — HuggingFace blog
  https://huggingface.co/blog/4bit-transformers-bitsandbytes

---

### OB-3.1 — Eval Harnesses

- **"HELM: Holistic Evaluation of Language Models"** — Liang et al. (2022)
  https://arxiv.org/abs/2211.09110
  The most thorough public eval framework. Read the methodology section.

- **lm-evaluation-harness — EleutherAI**
  https://github.com/EleutherAI/lm-evaluation-harness
  The standard tool. OBLIVION eval module will be based on this.

- **"Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena"** — Zheng et al. (2023)
  https://arxiv.org/abs/2306.05685
  When and why LLM-as-judge works (and when it doesn't).

- **ROUGE-L score documentation** — HuggingFace evaluate library
  https://huggingface.co/spaces/evaluate-metric/rouge

---

### OB-3.2 — Running Your Fine-Tune in Production

- **Ollama REST API documentation**
  https://github.com/ollama/ollama/blob/main/docs/api.md

- **"MLOps: From Model-centric to Data-centric AI"** — Andrew Ng (landing.ai)
  https://info.landing.ai/mlops-from-model-centric-ai-to-data-centric-ai

- **ShaneBrain MCP Server documentation**
  https://github.com/thebardchat/shanebrain_mcp
  The integration target for OB-3.2 exercises.

---

## Reading Priority Order

If starting from zero research, read in this order:

1. Watch Karpathy's GPT video (3 hours — non-negotiable)
2. Read LIMA paper (20 min — resets expectations about data quantity)
3. Read original LoRA paper (30 min)
4. Read QLoRA paper (30 min)
5. Read Raschka's practical fine-tuning tips (20 min)
6. Then go module-by-module for depth

---

*This list is a starting point. It will grow as modules are written and research turns up better sources. If you find a better reference for any topic, open an issue.*

*Last updated: April 23, 2026*
