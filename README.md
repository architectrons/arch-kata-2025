# Architectrons

## Business Problem
Certifiable, Inc. is facing a **5-10X increase** in certification requests due to **global expansion** and a **21% industry growth projection over the next four years**. The current **manual grading processes** cannot scale to meet demand while maintaining **accuracy and turnaround times**. The company is exploring **Generative AI** to enhance the **efficiency, accuracy, and scalability** of its certification system.

# AI-Integrated Certification System Architecture

## Overview

Certifiable, Inc. has integrated AI-driven automation into its certification process to address scalability challenges, reduce operational costs, and improve grading efficiency. By leveraging **Retrieval-Augmented Generation (RAG)** and cloud-based AI inference models, the system enhances the grading of aptitude tests, evaluates architecture submissions, and provides automated feedback without requiring costly model training or fine-tuning. The AI implementation ensures a balance between automation and expert oversight, preserving grading quality while significantly reducing manual effort.

### Key AI-driven enhancements:
- **Fraud Prevention & Identity Verification** - AI-powered facial recognition validates candidate identity.
- **Fully Automated AI-Assisted Aptitude Test Grading** – AI grades short-answer responses autonomously, requiring human intervention only for low-confidence cases.
- **AI-Powered Architecture Submission Evaluation** – Uses multi modal LLM to analyze architectural diagrams and flag uncertain cases for human review.

## Content
- [Business Goals](business_goals.md)
- [Constraints](constraints.md)
- [Main Use Cases](use_cases.md)
- [Detailed AI Use Cases](ai_use_cases_details.md)
- [Quality Attribute Scenarios](quality_attribute_scenarios.md)
- [ADRs](adrs/)
- [Infrastructure costs](aws_costs.md)
