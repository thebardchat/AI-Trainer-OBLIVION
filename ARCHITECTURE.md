# OBLIVION Architecture
*Captured: April 23, 2026 · Shane Brazelton / thebardchat*

---

## Why OBLIVION Exists

[AI-Trainer-MAX](https://github.com/thebardchat/AI-Trainer-MAX) teaches you to *use* a local AI.
It covers installation, vectors, RAG, personal knowledge vaults, automation, legacy, and teaching others.
By Module 5.10 (The Multiplier), you have a working brain, you can defend it, and you can spread it.

MAX deliberately left out one layer: **the inside of the model.**

MAX treats the model as a black box you configure and prompt. OBLIVION opens the box.

---

## The Core Distinction

| MAX | OBLIVION |
|-----|---------|
| Run a model | Shape a model |
| System prompts as config | System prompts as architecture |
| RAG fills gaps | Training rewrites weights |
| Eval is "does it feel right" | Eval is a harness with pass/fail |
| GPU optional | GPU required for most modules |
| Works on 7.4GB RAM | Requires 16GB+ RAM; GPU tiers matter |

---

## Planned Phase Structure

OBLIVION's 10 topic areas map to a provisional 3-phase arc. This is a working outline — not final until modules are written and tested.

### Phase OB-1 — THE FOUNDATION LAYER
*What the model is and how it changes*

| Planned Module | Topic |
|----------------|-------|
| OB-1.1 | Prompt-to-weights reasoning — what a gradient actually does |
| OB-1.2 | Quantization trade-offs — GGUF, Q4/Q5/Q8, when each wins |
| OB-1.3 | Embedding-space geometry — how retrieval really works |

**Prerequisite:** Completed AI-Trainer-MAX Phase 5 (The Multiplier)
**Hardware:** Pi 5 / CPU-only sufficient for Phase OB-1

---

### Phase OB-2 — THE TRAINING ARC
*Building, curating, and running a fine-tune*

| Planned Module | Topic |
|----------------|-------|
| OB-2.1 | Training-data curation — building the dataset that matters |
| OB-2.2 | Synthetic data generation pipelines — making your own, ethically |
| OB-2.3 | Custom Modelfiles at depth — system prompts as architecture |
| OB-2.4 | Fine-tuning on your own hardware — the actual mechanics |
| OB-2.5 | LoRA / QLoRA on consumer GPUs — 8GB, 12GB, 24GB reality |

**Prerequisite:** Phase OB-1 complete
**Hardware:** GPU with at least 8GB VRAM required starting Module OB-2.4

---

### Phase OB-3 — THE PRODUCTION RUN
*Measuring, deploying, and maintaining what you built*

| Planned Module | Topic |
|----------------|-------|
| OB-3.1 | Eval harnesses — measuring "better" instead of feeling it |
| OB-3.2 | Running your fine-tune in production — the part nobody documents |

**Prerequisite:** Phase OB-2 complete; a working fine-tuned model checkpoint
**Hardware:** Same as Phase OB-2

---

## Hardware Tiers

OBLIVION content will explicitly address three GPU tiers:

| Tier | VRAM | Capable Of |
|------|------|-----------|
| Entry | 8GB | QLoRA on 7B models, Q4/Q5 inference |
| Mid | 12GB | QLoRA on 13B models, Q8 inference, LoRA on 7B |
| High | 24GB | Full LoRA on 13B-70B, larger batch sizes, faster evals |

Pi 5 (no GPU, 16GB RAM) is the orchestration and RAG node, not the training node. It handles Phase OB-1 and the non-GPU portions of OB-2.1 through OB-2.3.

---

## File Structure (Target State)

```
AI-Trainer-OBLIVION/
├── README.md                    ← teaser + overview
├── ARCHITECTURE.md              ← this file
├── SYLLABUS.md                  ← topic outlines, module map
├── READING.md                   ← bibliography by topic
├── CHANGELOG.md                 ← release history
├── CLAUDE.md                    ← instructions for future Claude sessions
├── CONSTITUTION.md              ← governing principles
├── STATUS.md                    ← current project state (updated each session)
├── LICENSE
├── docs/
│   └── index.html               ← landing page (GitHub Pages)
├── .github/
│   ├── assets/
│   │   └── banner.svg
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.yml
│   │   ├── feature_request.yml
│   │   └── config.yml
│   └── PULL_REQUEST_TEMPLATE.md
└── phases/
    ├── phase-ob1-foundation/
    │   ├── README.md
    │   ├── module-ob1.1-prompt-to-weights/   PLANNED.md
    │   ├── module-ob1.2-quantization/        PLANNED.md
    │   └── module-ob1.3-embedding-geometry/  PLANNED.md
    ├── phase-ob2-training/
    │   ├── README.md
    │   ├── module-ob2.1-data-curation/       PLANNED.md
    │   ├── module-ob2.2-synthetic-data/      PLANNED.md
    │   ├── module-ob2.3-modelfiles-depth/    PLANNED.md
    │   ├── module-ob2.4-finetune-hardware/   PLANNED.md
    │   └── module-ob2.5-lora-qlora/          PLANNED.md
    └── phase-ob3-production/
        ├── README.md
        ├── module-ob3.1-eval-harnesses/      PLANNED.md
        └── module-ob3.2-production-deploy/   PLANNED.md
```

When a module is ready to write, it will gain: `lesson.md`, `exercise.sh`, `verify.sh`, `hints.md`.

---

## Relationship to the Broader Ecosystem

OBLIVION is the depth layer between MAX (foundation) and Angel Cloud (public platform).

```
ShaneBrain         (local · private)
  └── AI-Trainer-MAX         ← START HERE · foundation · 36 modules · COMPLETE
        └── AI-Trainer-OBLIVION   ← depth · 10 topics · IN DEVELOPMENT
              └── Angel Cloud      (public · families)
                    └── Pulsar AI     (enterprise · secure)
                          └── TheirNameBrain  (legacy · generational)
```

The fine-tuning and eval skills from OBLIVION directly feed TheirNameBrain: when you can shape a model for yourself, you can shape one for a family member who can't. That's the long game.

---

*"Your legacy runs local. OBLIVION is where you learn to build the thing that runs it."*

Built in Alabama. Built for everyone who's ready for the next step.

Co-built by Shane Brazelton and [Claude (Anthropic)](https://claude.ai/referral/4fAMYN9Ing).
