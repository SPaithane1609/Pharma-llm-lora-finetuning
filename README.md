# Pharma Drug Information Assistant — LoRA Fine-Tuning of an Open-Source LLM

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/SPaithane1609/Pharma-llm-lora-finetuning/blob/main/Pharma-Drug-Information-Assistant.ipynb)

A parameter-efficient fine-tuning (LoRA/QLoRA) project that adapts an open-source LLM (TinyLlama-1.1B-Chat) to answer pharmaceutical questions — drug indications, dosage, warnings, and side effects — using real FDA drug label data.

## Problem

Generic LLMs are inconsistent and often too verbose or vague when asked domain-specific pharma questions. This project fine-tunes a small open-source model on structured FDA label data so it responds in a consistent, factual, domain-appropriate format — a pattern directly relevant to pharma-industry use cases like internal drug-info assistants, medical affairs support, and patient education tooling.

## Approach

1. **Data collection** — pulled structured drug label sections (indications, dosage, warnings, adverse reactions, contraindications) live from the [openFDA Drug Label API](https://open.fda.gov/apis/drug/label/) for 20 common drugs.
2. **Dataset construction** — converted label sections into instruction/response pairs using an Alpaca-style prompt template.
3. **Fine-tuning** — loaded the base model in 4-bit precision (QLoRA) and attached LoRA adapters to the attention layers, training only ~1-2% of total parameters.
4. **Evaluation** — compared base model vs. fine-tuned model responses on held-out drug questions.
5. **Deployment** — served the fine-tuned model through an interactive Gradio chat demo, launchable directly from Colab.

## Tech stack

- **Model:** TinyLlama-1.1B-Chat (open-source, ungated)
- **Fine-tuning:** LoRA / QLoRA via Hugging Face `peft`, `transformers`, `bitsandbytes`
- **Data:** openFDA Drug Label API
- **Deployment:** Gradio (Colab-hosted demo)

## Results

| | Example query | Response style |
|---|---|---|
| Base model | "What is Metformin used for?" | Generic, occasionally off-topic |
| Fine-tuned model | "What is Metformin used for?" | Concise, FDA-label-aligned phrasing |

![Screenshot](assests/Base%20Model%20Example%201.png)
![Screenshot](assests/Fine%20Tuned%20Model%20Example%201.png)

## How to run

1. Open `Pharma Drug Information Assistant.ipynb` in Google Colab (badge above) or locally with a CUDA GPU.
2. Set runtime to a T4 GPU (Colab free tier works).
3. Run all cells top to bottom — it installs dependencies, pulls data, fine-tunes, evaluates, and launches a live demo link.

## Project structure

```
pharma-lora-finetuning/
├── Pharma_LoRA_FineTuning.ipynb   # full pipeline: data → training → eval → deployment
├── data/                          # sample collected/processed data (optional)
├── assets/                        # screenshots for this README
├── requirements.txt
└── README.md
```

## Disclaimer

Educational/portfolio project only. Not intended for clinical or medical decision-making — always defer to official FDA labeling and licensed professionals.

## Author

Built by Siddhant Paithane
