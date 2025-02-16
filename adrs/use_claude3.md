# AI Model Selection for Certification System
## Status
Proposed

## Date
2025-02-15

## Deciders
- Architectrons

---

## Context and Problem Statement

Certifiable, Inc. is integrating **AI-driven automation** for **grading certification exams** and **candidate authentication**. The AI models used must:  

- **Ensure Data Privacy & Security** – Test content and responses **must not be leaked or used for public AI training**.  
- **Provide Cost Efficiency** – AI services should be **scalable without excessive costs**.  
- **Ensure Scalability & Performance** – The solution must handle **increasing certification demand** efficiently.  
- **Support Explainability & Governance** – AI decisions must be **auditable and explainable** for certification credibility.  

A **trade-off analysis** is performed to evaluate AI models for **grading written responses, evaluating architecture diagrams**.  

---

## AI Model Trade-Off Analysis

| **Model**                | **Accuracy** | **Explainability** | **Data Privacy** | **Cost Efficiency** | **Scalability** | **Cloud Integration** |
|--------------------------|-------------|--------------------|------------------|----------------------|----------------|----------------------|
| **Claude 3 (Opus, Sonnet, Haiku)** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | **AWS Bedrock** |
| **GPT-4o** (OpenAI) | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | **OpenAI API, Azure OpenAI** |
| **Llama 3.3** (Meta) | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | **AWS Bedrock, Meta API** |
| **Gemini 2.0** (Google) | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | **Google Vertex AI** |

> **⭐ Ratings (1-5)** indicate relative performance in each category.

---

## AI Model Selection Justification

### **🏆 Choice: Claude 3 (Opus, Sonnet, Haiku)**
- **Strengths**: High **accuracy, privacy, and scalability**.  
- **Why?**: Available on **AWS Bedrock**, ensuring **test content is not leaked**.  
- **Multimodal Support**: **Can process text, images**, making it ideal for **grading written responses and analyzing diagrams**.  
- **Limitation**: Slightly lower cost efficiency than Llama 3.3.  

---

## Decision Outcome

| **Model** | **Primary Use** | **Justification** |
|-----------|---------------|------------------|
| **Claude 3 (Opus, Sonnet, Haiku)** | **Grading text-based exams + architecture diagrams** | Ensures **high accuracy, detailed feedback, and easy integration** via AWS Bedrock. |

