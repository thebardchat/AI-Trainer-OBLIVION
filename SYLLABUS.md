# AI-Trainer-OBLIVION — Provisional Syllabus
*Working outline · April 2026 · Subject to change as modules are written and tested*

---

## Prerequisites (Hard Gates)

Before starting OBLIVION you must have:

- Completed all 5 phases of [AI-Trainer-MAX](https://github.com/thebardchat/AI-Trainer-MAX) (36 modules)
- A machine with at least 16GB RAM
- A GPU with at least 8GB VRAM (12GB+ recommended; 24GB for later modules)
- Comfort at the command line — not fluency, comfort
- Python 3.10+ installed
- Ollama installed and running at least one model (from MAX)
- Patience — training runs fail; that is part of the course

If you haven't finished MAX: **finish MAX first.** OBLIVION will still be here.

---

## Phase OB-1 — THE FOUNDATION LAYER
*Understand what the model is before you try to change it*

**Goal:** Build enough conceptual grounding in how language models work — gradients, quantization, embeddings — that the training arc in Phase OB-2 makes sense. Not a math degree. Operational understanding.

**Hardware requirement:** The Pi 5 (CPU-only, 16GB RAM) can run most of Phase OB-1. No GPU required until Phase OB-2.

---

### Module OB-1.1 — Prompt-to-Weights Reasoning
**"What a gradient actually does."**

- What a forward pass is and what it computes
- What a loss function measures
- What backpropagation changes and why
- Why your loss curve is not the same as your model getting "better"
- Mental model: the parameter space and what fine-tuning navigates inside it
- Exercise: visualize training loss vs. eval loss on a published checkpoint

**You will prove:** You can explain, in plain language, why a model that overfits on training data gets worse at the thing you care about.

---

### Module OB-1.2 — Quantization Trade-offs
**"GGUF, Q4 vs Q5 vs Q8 — when each wins, when they break."**

- What quantization actually is (not "it makes the file smaller")
- Bit-width and information loss: Q2 through Q8
- GGUF format: what it encodes, how Ollama uses it
- The perplexity vs. speed vs. RAM triangle
- When to use Q4_K_M, Q5_K_M, Q8_0 — practical decision criteria
- Exercise: run the same prompt through Q4, Q5, and Q8 of the same model; compare output quality and speed

**You will prove:** You can choose a quantization level for a given hardware budget and use case without guessing.

---

### Module OB-1.3 — Embedding-Space Geometry
**"How retrieval really works. Why your RAG gets confused."**

- What an embedding is (not "a vector"; what it represents)
- Cosine similarity and why it's not Euclidean distance
- Semantic drift: why "patient" (medical) and "patient" (waiting) land in different places
- Dimensionality and what collapses when you compress
- Why adding bad documents to Weaviate hurts retrieval even if the good ones are there
- Exercise: embed 20 sentences; visualize clustering; find the two that are closest but shouldn't be

**You will prove:** You can explain why a RAG system returns wrong results and identify which part of the pipeline caused it.

---

## Phase OB-2 — THE TRAINING ARC
*Build a fine-tuned model from scratch on hardware you own*

**Goal:** Run a complete fine-tuning pipeline: collect data, clean it, format it, train a LoRA adapter, merge it, and verify the result is actually better than the base model.

**Hardware requirement:** GPU with at least 8GB VRAM required starting Module OB-2.4. Modules OB-2.1 through OB-2.3 can run on CPU.

---

### Module OB-2.1 — Training-Data Curation
**"Quality over quantity. Signal over noise."**

- The 1,000-sample myth: why more data is not always better
- What makes a good fine-tuning example (task, response, no ambiguity)
- Data formats: Alpaca, ShareGPT, raw instruction-response pairs
- Deduplication: why near-duplicates are worse than fewer examples
- Exercise: collect 100 real examples from your own use case; audit for quality; remove 20%

**You will prove:** You have a dataset of at least 50 high-quality examples in a recognized training format, with a documented quality-filtering pass.

---

### Module OB-2.2 — Synthetic Data Generation Pipelines
**"Making your own training data, ethically, at scale."**

- When synthetic data helps and when it compounds model drift
- Using your existing local model to generate variations on seed examples
- Decontamination: ensuring your synthetic data doesn't recapitulate training data you don't own
- Ethical use: what you can and can't fine-tune on
- Exercise: use Ollama + a local model to generate 50 synthetic training examples from 10 seed examples; run a dedup pass; audit 10 manually

**You will prove:** You have a clean synthetic dataset pipeline running locally that you understand end-to-end.

---

### Module OB-2.3 — Custom Modelfiles at Depth
**"System prompts as architecture, not cosmetics."**

- What a Modelfile actually encodes beyond the system prompt
- PARAMETER directives: temperature, top_p, top_k, repeat_penalty
- TEMPLATE: how the conversation format shapes model behavior (ChatML, Llama, Mistral)
- FROM + ADAPTER: using Modelfiles to load a fine-tuned adapter at inference time
- Exercise: write 3 Modelfiles for the same base model with different parameter profiles; test on the same 10 prompts; document which works best for each task

**You will prove:** You can write a Modelfile that changes model behavior in a measurable way, not just a description of what you want the model to say.

---

### Module OB-2.4 — Fine-Tuning on Your Own Hardware
**"The actual mechanics. Not hand-waving. Not someone else's Colab."**

- The training stack: Unsloth / Axolotl / llama.cpp finetune — when to use each
- Full fine-tune vs. LoRA vs. QLoRA: what changes in each case
- Dataset loading, tokenization, packing
- Setting: learning rate, batch size, epochs — the three levers that matter most
- Reading a training run: what loss curves tell you and what they don't
- Exercise: run a full QLoRA fine-tune of a 7B model on your curated dataset from OB-2.1; save the adapter checkpoint

**You will prove:** You have a trained LoRA adapter checkpoint on disk that you created from scratch on your own hardware.

---

### Module OB-2.5 — LoRA / QLoRA on Consumer GPUs
**"8GB, 12GB, 24GB — what's possible at each tier."**

- LoRA mechanics: what rank means, why it matters
- QLoRA: 4-bit quantized base + 16-bit LoRA adapters — the math that makes it fit
- Memory accounting: how to predict whether a given model + rank will fit in your VRAM
- Gradient checkpointing and why it slows training to save memory
- Merging adapters into the base model for Ollama serving
- Exercise: merge the adapter from OB-2.4 into the base model; import it into Ollama; run the eval prompts

**You will prove:** You can serve your fine-tuned model through Ollama and demonstrate that it answers your target domain better than the untuned base.

---

## Phase OB-3 — THE PRODUCTION RUN
*Measure what you built, deploy it, maintain it*

**Goal:** Move from "I trained a model" to "I have a model in production that I can measure, update, and roll back."

**Hardware requirement:** Same as Phase OB-2.

---

### Module OB-3.1 — Eval Harnesses
**"Measuring 'better' instead of feeling it."**

- Why vibes-based eval is not enough
- Writing test prompts that have objectively correct answers
- Scoring: exact match, ROUGE, LLM-as-judge
- Running the same eval against base model vs. fine-tune
- Regression testing: making sure the next version didn't break what the last one fixed
- Exercise: write an eval harness of 25 prompts for your target domain; run it against your fine-tune from OB-2.5 and the original base model; produce a comparison report

**You will prove:** You have a quantified score showing your fine-tune outperforms the base model on your target domain.

---

### Module OB-3.2 — Running Your Fine-Tune in Production
**"The part nobody documents."**

- Serving via Ollama: naming, versioning, switching models without downtime
- Integrating your fine-tune into a ShaneBrain MCP tool (the MAX ecosystem)
- Rolling updates: how to switch between model versions without breaking active sessions
- When to retrain vs. when to extend with RAG
- Monitoring: what to log, what degradation looks like over time
- Exercise: replace the model serving one of your MAX automation workflows with your fine-tune; run it for 24 hours; report on any quality regressions

**You will prove:** Your fine-tuned model is running inside your actual ShaneBrain infrastructure and you have a documented rollback procedure.

---

## Module Count Summary

| Phase | Modules | Status |
|-------|---------|--------|
| OB-1 Foundation Layer | 3 | PLANNED — not written |
| OB-2 Training Arc | 5 | PLANNED — not written |
| OB-3 Production Run | 2 | PLANNED — not written |
| **Total** | **10** | **0% complete** |

---

*This syllabus is a working outline. Module titles, order, and content are subject to change as Shane researches and tests the material. Nothing here is stable until a module is shipped.*

*Last updated: April 23, 2026*
