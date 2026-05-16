# SLG-PAA: Spatiotemporal Language Guidance with Part-Aware Alignment for Skeleton-based Micro-Action Recognition

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Paper](https://img.shields.io/badge/Paper-Under%20Review-red.svg)](#)

Official repository for the paper:

**Spatiotemporal Language Guidance with Part-Aware Alignment for Skeleton-based Micro-Action Recognition**

Tao Lu, Degui Xiao\*, Xingxing Xie, Chanthasith Phoutthihong, Yi Liu

*College of Computer Science and Electronic Engineering, Hunan University*

---

## 📖 Overview

Skeleton-based micro-action recognition is challenging because discriminative cues are highly localized to a few body parts and depend on subtle dynamics within specific motion stages. Existing skeleton-based approaches mainly rely on category-level supervision, which provides limited guidance about *which body parts* and *which motion stages* are discriminative.

To address this, we propose **SLG-PAA**, a language-guided training framework that supplies structured spatiotemporal priors through three components:

1. **Spatiotemporal Prompt Design** — Prompt templates tailored to micro-action differences, generating complementary spatial-part and temporal-stage text descriptions for each action category.
2. **Part-wise Temporal Stage Attention (PTSA)** — Selectively fuses the most relevant temporal-stage semantics into each part prototype on the text side.
3. **Coarse-to-Part Semantic Gating (CPSG)** — Assigns differentiated alignment weights to body parts based on their discriminative contributions on the alignment side.

The text branch serves **purely as a training-time supervisor** and adds **no inference cost**.

### Highlights

- 🎯 First language-guided training framework for skeleton-based micro-action recognition.
- 🧩 Tailored spatiotemporal prompts inject fine-grained micro-action priors.
- ⚖️ Part-wise temporal-stage attention and coarse-to-part gating align text and skeleton.
- ⚡ Achieves +2.54% F1 over the strongest skeleton-only baseline on the MA-52 dataset.

---

## 📂 Repository Structure

```
SLG-PAA/
├── text_descriptions/
│   ├── spatial-part_descriptions.csv     # 52 actions × {Global + 6 body regions}
│   └── temporal-stage_descriptions.csv   # 52 actions × 3 temporal stages
├── LICENSE
└── README.md
```

Training code will be released soon.

---

## 📑 Text Descriptions

### `text_descriptions/spatial-part_descriptions.csv`

Per-action, per-body-region textual descriptions emphasizing **which body parts are involved and how they move spatially**.

| Column         | Description                                                       |
| -------------- | ----------------------------------------------------------------- |
| `Action Label` | Action category name (52 in total, matches MA-52 official labels) |
| `Global`       | Whole-body description of the action                              |
| `Head`         | Description focused on the head                                   |
| `Arms`         | Description focused on the arms                                   |
| `Hands`        | Description focused on the hands                                  |
| `Torso`        | Description focused on the torso                                  |
| `Legs`         | Description focused on the legs                                   |
| `Feet`         | Description focused on the feet                                   |

**Example row** (`shaking body`):
- *Global*: "The torso and head move together in a rhythmic, small-amplitude motion, first tilting slightly to the left or right and then returning to an upright position, while seated, with no noticeable movement of the arms, legs, or feet."
- *Head*: "Head follows the torso with small left-right motion and minimal tilt."
- *Arms*: "The arms remain relaxed and still, with no noticeable movement."

### `text_descriptions/temporal-stage_descriptions.csv`

Per-action, per-stage textual descriptions emphasizing **how the motion unfolds across time**.

| Column         | Description                                       |
| -------------- | ------------------------------------------------- |
| `Action Label` | Action category name (matches the file above)     |
| `Stage 1`      | Onset / preparation phase                         |
| `Stage 2`      | Peak / execution phase                            |
| `Stage 3`      | Decay / return phase                              |

**Example row** (`shaking body`):
- *Stage 1*: "Head and torso subtly tense, ready to initiate oscillatory motion from a stable sitting position."
- *Stage 2*: "Torso and head rapidly oscillate with small amplitude, achieving peak speed in a localized, rhythmic shaking."
- *Stage 3*: "The oscillatory motion decelerates, and the head and torso return to a stable, stationary posture."

---

## 🙏 Acknowledgments

We thank the creators of the MA-52 dataset for providing a high-quality benchmark for micro-action research, and the authors of MMN for releasing their code, which our implementation builds upon.

---

## ⚖️ License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details. The MA-52 dataset has its own license; usage of the dataset must comply with the original terms set by its authors.
