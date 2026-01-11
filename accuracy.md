# Accuracy Analysis

## Overview
The automated detector was evaluated against a manually labeled dataset of 50 e-commerce chatbot conversations. Each conversation was classified into predefined error categories such as Hallucination, Retrieval Failure, False Action, or Correct.

## Results
- Total conversations: 50
- Correct predictions: 25
- Mismatches: 14
- Detector errors: 11
- Overall accuracy: 50.00%

## Interpretation
The overall accuracy is impacted by DetectorError cases. These errors were caused by inconsistent responses from the free-tier LLM inference API, such as missing expected response fields. When considering only successfully processed responses, the effective accuracy is higher.

## Observations
- The detector performed better on clear and explicit failure cases such as False Action and Safety Refusal.
- Subtle cases involving partial hallucinations or ambiguous responses were harder for the model to classify correctly.
- Several mismatches occurred in cases where error categories overlapped conceptually.

## Limitations
- Reliance on a free-tier LLM API resulted in unstable responses and incomplete outputs.
- No retry or fallback mechanism was implemented to handle temporary API failures.
- The model was not fine-tuned for this specific classification task.

## Conclusion
Despite the limitations, the automated detector successfully demonstrates how LLMs can be used to audit chatbot behavior and identify major failure patterns. In a production setting, accuracy could be improved by adding retries, response validation, and fallback models.
