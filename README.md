# Hallucination Auditor

## Overview
This project audits the behavior of a customer support chatbot to identify **hallucinations, incorrect refusals, false action claims, and other failure patterns**.

The goal is to demonstrate how Large Language Models (LLMs) can be used **not to answer customers**, but to **evaluate and monitor chatbot quality** in a real-world e-commerce setting.

This project was completed as part of a technical assignment for a **Junior AI/ML Engineer** role.

---

## Problem Statement
A customer support chatbot was deployed in beta and customers started reporting incorrect and misleading responses.

The product team suspected the model was “broken”.

This project investigates:
- What kinds of failures occur
- Why they happen
- How they can be detected automatically
- What should be fixed at the system level

---

## Dataset
The dataset consists of **50 synthetic but realistic chatbot conversations**.

Each record includes:
- `id`: Unique conversation ID  
- `user_query`: Customer question  
- `bot_response`: Chatbot reply  
- `context_document`: Policy or knowledge source (or `None`)  
- `ground_truth_error`: Human-labeled outcome  

### Error Categories
- Correct  
- Hallucination  
- Retrieval Failure  
- Safety Refusal  
- Prompt Injection  
- False Action  

More details are available in `dataset_notes.md`.

---

## Automated Detector
The detector (`detector.py`) uses a **free-tier LLM API (Hugging Face)** to analyze each conversation and classify the chatbot response.

For each conversation, the detector checks:
- Whether the response contradicts the policy
- Whether information was invented
- Whether the chatbot claimed to perform unauthorized actions
- Whether a refusal was appropriate

### Output
The detector produces `results.json` with the following structure:
```json
{
  "id": 1,
  "predicted_error": "Hallucination",
  "confidence": 0.9,
  "reasoning": "Explanation of the decision"
}
```
How to Run
1. Install dependencies
pip install requests python-dotenv

2. Set environment variable

Create a .env file:

HF_TOKEN=your_huggingface_token

3. Run detector
python detector.py

4. Review outputs

results.json

accuracy.md

Project Structure
.
├── chat_logs.json
├── dataset_notes.md
├── detector.py
├── results.json
├── accuracy.md
├── executive_memo.pdf
└── README.md

Notes

Only free-tier APIs were used

No fine-tuning was performed

Detector errors were handled and documented

The focus is on reasoning and auditing, not maximizing accuracy

Author

Jawaharsrinath M N
