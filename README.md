# Arabic Clinical Named Entity Recognition (NER)

This project implements a high-performance **Arabic Clinical Named Entity Recognition (NER)** system. It demonstrates a complete pipeline from handling restricted medical data to deploying state-of-the-art transformer architectures.

## 🚀 Pipeline Overview

1.  **Baseline Data**: Started with an Arabic clinical dataset restricted to a single entity (**Disease**).
2.  **LLM-Driven Augmentation**: Leveraged the **Gemini Pro API** to generate synthetic clinical scenarios, balancing the representation of rare medical categories.
3.  **AI Annotation**: Integrated **GPT-4o** via **Dify** to automatically annotate medical Q&A datasets, expanding the system to 5 clinical categories.
4.  **Transformation**: Converted complex **IOBES** labels into a unified **IOB** scheme for transformer compatibility.

---

## 🛠️ Data Preprocessing

To ensure robust performance across formal and dialectal Arabic, the following normalization was applied:

* **Arabic Normalization**: Removal of diacritics and Tatweel; unification of Alef, Yaa, Hamza-on-waaw, and Taa Marbouta variants.
* **Sentence Grouping**: Tokens were grouped into contextually coherent sentences using punctuation boundaries.
* **Sub-word Alignment**: Labels were aligned with BERT WordPiece sub-tokens using a `-100` ignore index to prevent loss bias during training.

---

## 📊 Model Evaluation

We benchmarked five specialized transformer architectures under identical experimental protocols:

| Model | Architecture Focus | F1-Score |
| :--- | :--- | :--- |
| **CAMeL-BERT-Mix** | **Winner: Balanced MSA and Dialectal Arabic** | **0.8439** |
| **AraBERT** | Modern Standard Arabic (MSA) specialization | 0.8230 |
| **QARiB** | Pre-trained on diverse Arabic corpora | 0.8145 |
| **MARBERT** | Optimized for Arabic Dialects | 0.8100 |
| **XLM-RoBERTa** | Multilingual baseline (underperforms on domain-specific Arabic) | 0.7950 |

> **Note:** CAMeL-BERT achieved the highest performance due to its Arabic-focused pre-training and superior handling of long medical sequences.

---

## 🏆 Final Model: CAMeL-BERT-Mix

The best-performing model utilizes a targeted optimization strategy:

* **Learning Rate**: 3e-5 (Optimized from 1e-5 to 3e-5).
* **Training**: Full fine-tuning (outperformed partial layer freezing).
* **Metric Strategy**: Best model selected based on **F1-score** to ensure a balance between precision and recall for rare entities.

## 📂 File Structure
* `data/`: Preprocessed datasets (Original + Gemini-Augmented + AI-Annotated).
* `scripts/`: Preprocessing logic and training loops.
* `notebooks/`: Exploratory Data Analysis and Model Benchmarking.

---
