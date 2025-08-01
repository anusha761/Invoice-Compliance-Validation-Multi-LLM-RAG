# Automated Invoice Compliance Validation using Multi-LLM Orchestration and RAG Based Pipeline

> A multimodal, schema-enforced Proof of Concept system designed to intelligently validate invoice compliance using orchestrated large language models. Inspired by principles from the Model Context Protocol (MCP), this POC explores how structured handoffs between LLMs can enable clear, traceable reasoning across stages. This POC demonstrates how invoice fraud, policy violations, and document inconsistencies can be identified and explained clearly, both for machine integration and human understanding, across documents of diverse formats and quality.


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

## Solution Overview

1. Multimodal Invoice Analysis (Stage 1 – GPT-4o) : The pipeline begins with an invoice image. GPT-4o, leveraging its multimodal capabilities, extracts key fields such as vendor name, bank details, tax info, invoice amount, and line items. It also flags potential issues—like missing fields, unclear images, or abnormal quantities. The model's output is strictly formatted using OpenAI’s function-calling schema, ensuring the results conform to a predefined structure. This schema-enforced output allows for consistent downstream processing and reliable integration with subsequent reasoning steps and system components.

2. Policy Retrieval (ChromaDB + Sentence Transformers): Identified error messages are used to query a vector store built with ChromaDB. The system retrieves the top two most relevant policy clauses from the stored compliance documents.

3. Policy-Aware Reasoning (Stage 2 – GPT-4o-mini): The original LLM output, along with the retrieved policy clauses, is passed to a second LLM (GPT-4o-mini). It evaluates the issues in context and determines whether they represent actual policy violations. It also recommends appropriate next steps based on the policy.

4. Structured and Human-Readable Output: The result is returned as a structured schema enforced JSON object containing - validation_summary, risk_assessment (with references to relevant policies), suggestive_action. This output is machine-readable for integration into enterprise systems, but also formatted into clear, plain English summaries—easily understandable by users such as compliance officers, finance staff, or auditors.

## Design Philosophy

This project was inspired by the Model Context Protocol (MCP) — a framework that encourages structured, modular interactions between language models. While this implementation is exploratory and intentionally lightweight, it adopts the core spirit of MCP to enable multi-LLM orchestration using OpenAI’s function calling schema.

In this prototype, GPT-4o first produces a structured JSON output based on multimodal invoice analysis. This output is then programmatically enriched and passed as input to a second model (GPT-4o-mini) for context-aware policy reasoning. Enforcing a consistent schema between these stages brings clarity, traceability, and alignment to the LLM pipeline.

This approach represents an early-stage, hands-on attempt to explore how ideas from MCP can be applied in practical, real-world use cases. It is presented as a rapid prototype and proof of concept, with full acknowledgment that MCP is a broader and more sophisticated paradigm still evolving in the research and enterprise AI community.


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


## Output Screenshots

#### Invoice 1

<img width="690" height="763" alt="inv1" src="https://github.com/user-attachments/assets/ad03ccc1-949f-43a7-8323-d6d7bbdc7b15" />

#### Report

<img width="1149" height="166" alt="inv1-resp" src="https://github.com/user-attachments/assets/1d56d6cc-5e8f-455b-9a88-c29fcf7e3afe" />

#### Invoice 2

<img width="657" height="851" alt="inv2" src="https://github.com/user-attachments/assets/33cdfa78-9bef-48e3-b4b8-289ec538a1d8" />

#### Report

<img width="1159" height="283" alt="inv2-resp" src="https://github.com/user-attachments/assets/819d8dae-fd5c-4657-80bf-e641ec1b43b2" />

#### Invoice 3

<img width="676" height="866" alt="inv3" src="https://github.com/user-attachments/assets/f9f897eb-c52e-4d50-995d-fc2359040b47" />

#### Report

<img width="259" height="84" alt="inv3-resp" src="https://github.com/user-attachments/assets/30f9bcf8-0345-423f-8f08-23bd6728fa4e" />


## Library Versions

- openai==1.97.1  
- chromadb==1.0.15  
- transformers==4.53.3  
- pandas==2.2.2  
- langchain==0.3.27


## Contact
Anusha Chaudhuri [anusha761]
