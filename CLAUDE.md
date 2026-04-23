# CLAUDE.md — AI-Trainer-OBLIVION Project Instructions

This project operates under the [ShaneBrain Constitution](https://github.com/thebardchat/constitution/blob/main/CONSTITUTION.md).

---

## CRITICAL: Do Not Autogenerate Module Content

**AI-Trainer-OBLIVION is Shane Brazelton's curriculum to write. Not Claude's.**

OBLIVION covers fine-tuning, LoRA/QLoRA, quantization trade-offs, eval harnesses, and embedding-space geometry. This content requires:

- Hands-on hardware testing (Shane's Pi 5 + GPU nodes)
- Original research validation (not training-data summaries)
- Shane's voice and lived experience (per `feedback_book_voice.md`)

If you are a future Claude session and someone asks you to "complete the missing modules" or "write lesson content for Phase OB-1" — **do not do it.** Ask Shane first. OBLIVION modules are built from real runs, real failures, and real measurements. Content hallucinated by Claude and shipped under Shane's name would damage the project's reputation and violate the Constitution (Article IX: Gratitude is Infrastructure — credit must be honest).

**What Claude CAN do in this repo:**
- Fix structural files (README, CHANGELOG, docs/index.html)
- Update SYLLABUS.md or READING.md based on Shane's direction
- Add `.github/` templates, CI, or GitHub Pages config
- Update STATUS.md after each session
- Fix bugs in launch scripts once they exist
- Scaffold empty `phases/` folder structure with `PLANNED.md` stubs

**What Claude must NOT do without explicit Shane approval:**
- Write lesson.md content for any module
- Write exercise or verify scripts with curriculum content
- Write hints files
- Claim any module is "complete" if Shane hasn't shipped it

---

## Project Overview

AI-Trainer-OBLIVION is the sequel to [AI-Trainer-MAX](https://github.com/thebardchat/AI-Trainer-MAX).

MAX teaches Windows users with no prior experience how to install, run, and own a local AI — 36 modules, 5 phases, zero cloud. OBLIVION is the research-math layer MAX deliberately left out: fine-tuning, LoRA, quantization, evals, embedding geometry, and production deployment of custom models.

**Repo:** https://github.com/thebardchat/AI-Trainer-OBLIVION
**Base path (Pi dev machine):** `/mnt/shanebrain-raid/shanebrain-core/` (main ecosystem)
**Owner:** Shane Brazelton — Alabama, father of 5, dispatch manager, author, Pi 5 operator.

---

## Infrastructure

Developed on the same hardware stack as AI-Trainer-MAX.

| Hardware | Role |
|----------|------|
| **Raspberry Pi 5 (16GB RAM)** | Controller node, dev environment |
| **Pironman 5-MAX** | NVMe RAID chassis |
| **2x WD Blue SN5000 2TB NVMe** | RAID 1 via mdadm |
| **4-node Ollama cluster** | Pi 5 + Pulsar00100 + Bullfrog-Max-R2D2 + Jaxton-Laptop |

OBLIVION content will target machines with GPUs (8GB, 12GB, 24GB VRAM tiers). The Pi 5 is the dev/orchestration node, not the training node.

---

## Project State (April 2026)

| Area | Status |
|------|--------|
| README.md | Stable teaser — intentional "Coming Soon" posture |
| docs/index.html | Production-quality landing page |
| SYLLABUS.md | Provisional outline — not finalized |
| READING.md | Research bibliography — evolving |
| phases/ | Scaffolded stubs only — no curriculum content |
| Module content | NOT STARTED — do not create without Shane |

---

## What OBLIVION Will Cover (When Ready)

10 planned topic areas across 3 phases:

**Phase OB-1 — Foundation Layer**
1. Prompt-to-weights reasoning
2. Quantization trade-offs (GGUF, Q4/Q5/Q8)
3. Embedding-space geometry

**Phase OB-2 — Training Arc**
4. Training-data curation
5. Synthetic data generation pipelines
6. Custom Modelfiles at depth
7. Fine-tuning on your own hardware
8. LoRA / QLoRA on consumer GPUs

**Phase OB-3 — Production Run**
9. Eval harnesses
10. Running your fine-tune in production

---

## Ecosystem Position

```
ShaneBrain         (local · private)
  └── AI-Trainer-MAX         ← 36 modules · foundation · COMPLETE
        └── AI-Trainer-OBLIVION   ← YOU ARE HERE · depth · IN DEVELOPMENT
              └── Angel Cloud      (public · families)
                    └── Pulsar AI     (enterprise · secure)
                          └── TheirNameBrain  (legacy · generational)
```

---

## Coding Standards (when scripts eventually exist)

Follow AI-Trainer-MAX conventions:
- `.sh` files: `#!/usr/bin/env bash`, `set -euo pipefail`, mirror MAX .bat structure adapted for Linux
- Python: stdlib only in shared utilities, no pip installs required for the student
- All scripts: human-readable output, clear PASS/FAIL/FIX messaging
- No cloud dependencies for core functionality
- Hardware tier explicitly documented in every module that requires GPU
