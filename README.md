# Automated Invoice Compliance Validation using Multi-LLM Orchestration and RAG Based Pipeline

> A multimodal, schema-enforced Proof of Concept system designed to intelligently validate invoice compliance using orchestrated large language models. This POC demonstrates how invoice fraud, policy violations, and document inconsistencies can be identified and explained clearly, both for machine integration and human consumption, across documents of diverse formats and quality.


## Problem Statement

In large-scale enterprises and financial operations, invoices received from third-party vendors often vary in format, clarity, layout and completeness. Manual verification of such documents is time-consuming, error-prone. Traditional Python scripts based on regex or rule-based parsers struggle to generalize across heterogeneous formats. Furthermore, conventional scripting lacks the ability to contextualize business rules or compliance policies in real-time.


This project addresses the industrial need for:
- Automating invoice validation across heterogeneous formats
- Detecting anomalies such as missing tax IDs, bank details, or suspicious amounts
- Assessing policy violations based on internal compliance guidelines
- Delivering results in a format that is both machine-readable and human-readable, allowing non-technical finance staff to act confidently on validation outcomes.


## Project Overview

This POC system demonstrates how multiple LLMs can be orchestrated to perform end-to-end invoice compliance checks using GPT-4o’s multimodal capabilities and policy-based reasoning from GPT-4o-mini. The pipeline is built with a clear separation of responsibilities between model stages, enforced via OpenAI's function-calling mechanism.

Key Features:
- Analyzes invoice images to extract critical fields using GPT-4o
- Detects common compliance issues (missing tax data, bank info, abnormal amounts)
- Retrieves relevant internal policy clauses using vector similarity search (ChromaDB)
- Uses GPT-4o-mini to interpret violations in the context of those policies
- Outputs results in a structured JSON format for seamless integration into enterprise workflows, while also presenting them in a clear, human-readable format suitable for audit and review.

---

## Architecture Overview

```
[Invoice Image]
        ↓
[Stage 1: GPT-4o (Multimodal Analysis)]
        ↓
• Extracts invoice data
• Identifies potential errors
        ↓
[ChromaDB Vector Store]
• Retrieves top-2 relevant policy clauses
        ↓
[Stage 2: GPT-4o-mini (Policy-Aware Reasoning)]
        ↓
• Determines policy violations
• Suggests actionable next steps
        ↓
[Structured JSON Output]
• validation_summary
• risk_assessment with policy references
• suggestive_action
        ↓
Deliver in human readable format
```


## Technology Stack

| Component              | Technology Used                         |
|------------------------|------------------------------------------|
| Multimodal LLM         | OpenAI GPT-4o                            |
| Lightweight LLM        | OpenAI GPT-4o-mini                       |
| Embedding Model        | Sentence Transformers (MiniLM)           |
| Vector Store           | ChromaDB via LangChain VectorStores      |
| Schema Enforcement     | OpenAI Function Calling Schema           |
| Orchestration & Logic  | Python, Pandas                           |


## Scope for Further Enhancement (OCR Enhancement)

While GPT-4o provides basic multimodal capabilities for extracting text from images, integrating a dedicated OCR engine such as Google Document AI or AWS Textract would improve reliability on low-quality or complex invoice formats. This would complement the existing pipeline and enhance consistency in production environments.


## Library Versions

- openai==1.80.0  
- chromadb==1.0.13  
- sentence-transformers==3.4.1  
- pandas==2.2.2  
- langchain==0.3.25  
- langchain-core==0.3.63  
- langchain-community==0.3.25  
- langchain-chroma==0.2.4  
- python==3.10+


## Contact
Anusha Chaudhuri [anusha761]
