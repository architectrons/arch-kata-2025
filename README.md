# Architectrons

## AI-Driven Enhancements to Certifiable, Inc.’s Certification System  

Certifiable, Inc. is scaling its certification process to handle a **5-10X increase in candidate volume** while maintaining accuracy, fairness, and efficiency. The introduction of **AI-driven automation** addresses grading bottlenecks, fraud prevention, and quality assurance, ensuring a **highly scalable, cost-effective**, and **trustworthy** certification process.  

To achieve this, we applied **AI architecture patterns** such as **Retrieval-Augmented Generation (RAG)** for accurate grading, **Multi-Modal AI** for architecture submission evaluation, and **Human-in-the-Loop (HITL)** to ensure high-quality decisions where AI confidence is low. AWS services were selected for their **native AI integration, scalability, and security**, allowing seamless deployment of AI models with **cost-efficient inference and governance frameworks**.  

## Goals of AI Enhancements & Implemented Use Cases  

| **Business Goal** | **AI-Driven Enhancement** | **Contribution to Goals** |
|-------------------|--------------------------|--------------------------|
| **Scalability** – Handle 10X growth in certifications | **Bedrock as AI Gateway** for **LLM-powered grading (Claude 3.5 Sonnet)** | **Automates short-answer grading**, reducing reliance on human graders |
| **Accuracy & Trust** – Guarantee fair and unbiased grading | **Bedrock Guardrails + SageMaker Clarify** | **Bias detection & evaluation guardrails** prevent hallucinations and grading inconsistencies |
| **Expert Oversight & Quality Control** | **Human-in-the-Loop (HITL) Pattern** | **AI flags low-confidence cases for expert validation**, maintaining credibility |
| **Fraud Prevention** – Secure identity verification | **AWS Rekognition for facial matching** | **Prevents impersonation & ensures candidate integrity** |
| **Efficiency & Speed** – Reduce grading turnaround from 1 week to hours | **RAG-based feedback generation** | **Retrieves past graded responses for comparison**, ensuring **consistency and explainability** |
| **Reducing Operational Costs** | **On-demand AI inference (Bedrock, Lambda)** | **Eliminates expensive fine-tuning**, using **prompt engineering & retrieval-based models** |

## How AI Patterns Enable This Design  
1. **AI Gateway Pattern (AWS Bedrock)** – Unified access to **Claude 3.5 Sonnet**, ensuring **flexibility and cost control** without vendor lock-in.  
2. **Guardrails Framework (Bedrock Guardrails + SageMaker Clarify)** – **Bias detection, model explainability, and hallucination prevention** ensure compliance and **certification integrity**.  
3. **Retrieval-Augmented Generation (RAG) Pattern (PostgreSQL + pgvector)** – AI references **past grading decisions** to **reduce inconsistencies and improve feedback accuracy**.  
4. **Multi-Modal AI (AWS Textract + Vision AI)** – Extracts **diagrams, text, and annotations** from architectural submissions for **automated evaluation**.  
5. **Human-in-the-Loop (HITL) Pattern** – AI flags uncertain cases, ensuring **expert validation** before final grading, balancing **automation with oversight**.  

## Content
- [Business Goals](business_goals.md)
- [Constraints](constraints.md)
- [Main Use Cases](use_cases.md)
  - [AI Short Asnwers](ai_short_answers_grading.md)
  - [AI Architecture Submission](ai_architecture_submission.md)
  - [ML Identity Verification](ml_identify_verfication.md)
  - [AI Assisted Use Cases Generation](ai_assisted_use_cases.md)
- [Quality Attribute Scenarios](quality_attribute_scenarios.md)
- [ADRs](adrs/)
- [AI Guardrails: Accuracy and Relevance](ai_guardrails.md)
- [Infrastructure costs](aws_costs.md)
