# Empathetic Response AI

Emotion-aware chatbot — detects the emotion in a message first, then generates a reply that matches it.

## Problem Statement

A chatbot that ignores how someone is feeling comes across as cold, especially in support chats. Companies like Zendesk lean toward AI that reads emotional tone before replying. This project pairs a pretrained emotion classifier with a LoRA-fine-tuned GPT-2 that generates emotion-conditioned replies.

## Dataset

[EmpatheticDialogues](https://huggingface.co/datasets/facebook/empathetic_dialogues) — 30,000 training examples sampled from ~76,700 available conversation turns, each tagged with one of 32 emotion labels.

## What It Builds

- An emotion detector (pretrained DistilRoBERTa classifier, no training needed for this part)
- A GPT-2 model fine-tuned with LoRA to reply in a way that matches the detected emotion
- A combined `empathetic_response()` function: detect emotion → generate a matching reply
- A saved, lightweight LoRA adapter (not a multi-GB checkpoint)

## Results (from an actual training run)

| Metric | Value |
|---|---|
| Training examples | 30,000 |
| LoRA trainable params | 294,912 out of 124,734,720 (**0.24%**) |
| Training epochs | 4 |
| Final training loss | 2.54 |
| Training time | ~7.5 min on a free Colab T4 |

**Example run:**
> Input: *"I just lost my job after five years at the company."*
> Detected emotion: **sadness** (0.76 confidence)
> Generated reply: *"I'm sure I will have to work hard for my life to get back to the top. I hope I can come back with an amazing job in life..."*

The reply is a bit repetitive in places — an honest known limitation of GPT-2-small at this training scale, worth noting rather than hiding.

## Tech Stack

Python · HuggingFace Transformers · PEFT (LoRA) · Google Colab (free T4 GPU)

## How to Run

1. Open the notebook in Google Colab
2. Runtime → Change runtime type → T4 GPU
3. Run all cells top to bottom
4. Enter a free [Groq API key](https://console.groq.com/keys) when prompted (used for an optional AI helper, not required for the core training pipeline)

## Repo Structure

```
empathetic-response-ai/
├── Empathetic_Response_AI.ipynb
└── README.md
```

## Disclaimer

Built as a learning/portfolio project. Not a substitute for real emotional support or crisis resources — generated replies are for demonstration purposes only.

---
By Akshat Kesharwani
