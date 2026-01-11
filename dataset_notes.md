# Dataset Notes – Hallucination Auditor

## Overview
This dataset was created to simulate real-world customer support chatbot conversations in an e-commerce domain.  
The goal was not to create perfect or artificial examples, but to reflect practical failure modes that occur when chatbots are deployed in production.

Each conversation includes:
- A user query  
- The chatbot’s response  
- A reference context document (or None)  
- A human-assigned ground truth label indicating whether the response is correct or problematic  

### Why this domain was chosen
I chose the e-commerce customer support domain because:
- It is easy to understand without deep domain knowledge  
- It involves real business risks (refunds, cancellations, data privacy)  
- It commonly appears in real chatbot deployments  

This allowed me to focus on reasoning and error analysis rather than domain complexity.

---

## Error Categories and Motivation

The dataset includes the following categories, each chosen to reflect a different type of real-world risk:

### 1. Correct
These cases ensure the system can recognize when the chatbot behaves correctly.  
Including correct examples avoids a bias toward flagging everything as an error.

### 2. Hallucination
In these cases, the chatbot invents information that is not supported by the context document.  
I intentionally included subtle hallucinations, such as:
- Slightly changing numbers (e.g., 30 days → 45 days)  
- Adding guarantees or timelines not mentioned in the policy  

These are dangerous because they sound confident and plausible.

### 3. Retrieval Failure
Here, the chatbot responds with uncertainty or lack of knowledge even though the required information exists in the context.  
These cases simulate poor document grounding rather than incorrect generation.

### 4. Safety Refusal
These represent correct refusals where the chatbot blocks harmful or sensitive requests (e.g., hacking, accessing private data).  
Including these cases helps distinguish good refusals from actual failures.

### 5. Prompt Injection
These cases simulate attempts to override system rules using instructions like “ignore all previous rules.”  
They are important because such attacks are common in real deployments and can lead to serious data leaks if mishandled.

### 6. False Action
These are the most critical business-risk cases.  
The chatbot claims it has performed actions such as:
- Processing refunds  
- Cancelling orders  
- Updating user information  

In reality, the chatbot does not have the authority to perform these actions.  
Such responses can lead to legal, financial, and trust-related issues.

---

## Design Considerations
- The dataset intentionally mixes clear errors and ambiguous edge cases  
- Some examples are partially correct but still labeled as errors to reflect realistic judgment calls  
- Context documents vary in completeness to simulate real knowledge base limitations  
- Not all failures are obvious; some require careful comparison between response and context  

The dataset is not intended to be perfect, but to reflect the kinds of challenges faced when auditing real AI systems.

---

## Limitations
- The dataset is synthetic and manually created  
- Ground truth labels are based on human judgment and may vary across reviewers  
- Some ambiguous cases could reasonably be interpreted differently  

These limitations are intentional, as they mirror the uncertainty present in real-world AI evaluation.

---

## Conclusion
This dataset was designed to support analysis of hallucinations, grounding failures, safety risks, and false claims in chatbot systems.  
The focus was on practical reasoning and failure understanding, rather than maximizing accuracy or complexity.
