# AWS Cost Estimation for AI-Based Certification System (10x Growth)

With overseas expansion, Certifiable, Inc. should prepare for approximately 4,000 to 8,000 candidates per month
Beyond this surge, anticipate a steady increase of about 0.4375% per month, leading to approximately 4,214 candidates per month after one year (based on a 5× initial growth).

---
# 1. Short answers grading

## Total Estimated Monthly Cost

| **Service**                           | **Estimated Cost (USD)** |
|---------------------------------------|-------------------------|
| Amazon S3                             | $0.18                   |
| Amazon OpenSearch Serverless          | $692.70                 |
| Amazon Bedrock (Claude 3.5 Sonnet)    | $480.00                 |
| AWS Lambda                            | $0.06                   |
| Amazon CloudWatch Logs                | $5.30                   |
| Amazon API Gateway (Optional)         | $0.56                   |
| **Total**                             | **$1,178.80**           |


## 1. Data Storage (Amazon S3)
**Use Case:** Store candidate responses and processed results.

### Storage Requirements:
- **Data Volume:** 8,000 candidates/month × 20 responses/candidate × 50 KB/response = **8,000,000 KB/month** (approximately 7.63 GB).

## 2. Vector Database (Amazon OpenSearch Serverless with Vector Engine and Graph Module)
**Use Case:** Store and retrieve question embeddings for Retrieval Augmented Generation (RAG).

### Compute Requirements:
- **Minimum OCUs:** OpenSearch Serverless requires a minimum of **4 OCUs** (2 for indexing, 2 for search).

### Cost Calculation:
- **Compute Cost:** 4 OCUs × $0.24/OCU-hour × 24 hours/day × 30 days = **$691.20/month**.
- **Storage Cost:** Assuming 5 GB of vector embeddings at $0.30/GB-month = **$1.50/month**.

## 3. Model Inference (Amazon Bedrock using Claude 3.5 Sonnet Model)
**Use Case:** Evaluate candidate responses and generate feedback.

### Inference Requirements:
- **Total Inferences:** 8,000 candidates × 20 responses each = **160,000 inferences/month**.
- **Token Usage per Inference:** 500 input tokens + 300 output tokens = **800 tokens**.
- **Total Tokens per Month:** 160,000 inferences × 800 tokens = **128,000,000 tokens**.

### Cost Calculation:
- **Input Token Cost:** (500 tokens/input ÷ 1,000) × $0.0015 × 160,000 inferences = **$120.00**.
- **Output Token Cost:** (300 tokens/output ÷ 1,000) × $0.0075 × 160,000 inferences = **$360.00**.

### **Estimated Monthly Cost:** **$480.00**.

## 4. Compute & Processing (AWS Lambda)
**Use Case:** Post-process model outputs, calculate grades, and provide feedback.

### Execution Requirements:
- **Invocations:** 160,000/month.
- **Duration per Invocation:** 1 second.
- **Memory Allocation:** 512 MB.

## 5. Monitoring & Logging (Amazon CloudWatch Logs)
**Use Case:** Track API requests, inference logs, and debugging information.

### Logging Requirements:
- **Log Data:** Assuming **10 GB/month**.

## 6. API Gateway (Optional)
**Use Case:** Provide a managed API for RAG queries.

### Request Requirements:
- **Requests:** 160,000/month.

---

## Notes:
- **Amazon OpenSearch Serverless:** Minimum deployment requires **4 OCUs**, leading to a base cost of approximately **$691.20/month** ([AWS OpenSearch Pricing](https://aws.amazon.com/opensearch-service/pricing/)).
- **Amazon Bedrock Pricing:** The Claude 3.5 Sonnet model is priced at **$0.0015 per 1,000 input tokens** and **$0.0075 per 1,000 output tokens** for batch prcessing (50% discount) ([AWS Bedrock Pricing](https://aws.amazon.com/bedrock/pricing/)).
- **AWS Lambda and API Gateway:** Costs are minimal due to the low execution time and request volume.
- **CloudWatch Logs:** Costs are based on ingestion and storage rates.
