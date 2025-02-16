# AWS Cost Estimation for AI-Based Certification System (10x Growth)

With overseas expansion, Certifiable, Inc. should prepare for approximately 4,000 to 8,000 candidates per month
Beyond this surge, anticipate a steady increase of about 0.4375% per month, leading to approximately 4,214 candidates per month after one year (based on a 5× initial growth).

## AWS Monthly Costs

| **Feature**                           | **Estimated Cost (USD)** |
|---------------------------------------|-------------------------|
| Grade short answers                   | $1,178.80                   |
| Guardrails          | $161.60                 |
| **Total**                             | **$1,340.40**           |


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

---

# 2. Guardrails costs estimation
## 1. Ensuring Fair & Unbiased AI Scoring

### Bias Detection in Grading (Amazon SageMaker Clarify)
**Use Case:** Detect grading inconsistencies across demographics and flag biased responses.

#### Usage Requirements:
- **SageMaker Clarify Pricing:** $0.42 per hour.
- Key Estimations:
	•	Assume 1 batch job per week to analyze bias trends in AI grading.
	•	Each batch run processes 40,000 responses (160,000 responses / 4 weeks).
	•	Estimated Compute Time per Batch: 12.5 hours (for feature extraction, fairness metric calculations, and report generation).
	•	Total per Month: 12.5 hours × 4 weeks = 50 hours/month.
- **Estimated Usage:** 50 hours per month.

#### Cost Calculation:
- **Monthly Cost:** 50 hours × $0.42/hour = **$21.00**.

### Content Analysis on Candidate Responses (Amazon Comprehend)
**Use Case:** Ensure AI does not misinterpret tone or phrasing when grading.

#### Usage Requirements:
- **Amazon Comprehend Pricing:** $0.0001 per 1,000 characters.
- **Estimated Characters per Response:** 1,000 characters.
- **Total Characters Processed Monthly:** 8,000 candidates × 20 responses/candidate × 1,000 characters = 160,000,000 characters.

#### Cost Calculation:
- **Monthly Cost:** (160,000,000 ÷ 1,000) × $0.0001 = **$16.00**.

---

## 2. AI Drift & Consistency in Grading Over Time

### Response Drift Detection (Amazon Bedrock Model Evaluation)
**Use Case:** Monitor grading changes over time to prevent inconsistencies.

#### Usage Requirements:
- **Bedrock Model Evaluation Pricing:** Estimated $10 per evaluation.
- **Evaluations per Month:** 10 runs.

#### Cost Calculation:
- **Monthly Cost:** 10 evaluations × $10/evaluation = **$100.00**.

### Scoring Stability Check (Amazon SageMaker Model Monitor)
**Use Case:** Track grading distribution to prevent unfair fluctuations.

#### Usage Requirements:
- **SageMaker Model Monitor Pricing:** $0.30 per hour.
- Key Estimations:
	•	Assume 1 batch job per week to analyze grading consistency.
	•	Each batch run processes 40,000 responses (160,000 responses / 4 weeks).
	•	Estimated Compute Time per Batch: 12.5 hours
- **Estimated Usage:** 50 hours per month.

#### Cost Calculation:
- **Monthly Cost:** 50 hours × $0.30/hour = **$15.00**.

---

## 3. AI Explainability & Compliance Guardrails

### AI Grading Audit Logs (AWS CloudTrail)
**Use Case:** Log all AI grading decisions for auditability.

#### Usage Requirements:
- **CloudTrail Pricing:** $2.00 per 100,000 events.
- **Logged Events per Response:** 3 (grading decision, evaluation, audit entry).
- **Total Events Monthly:** 8,000 candidates × 20 responses/candidate × 3 events/response = 480,000 events.

#### Cost Calculation:
- **Monthly Cost:** (480,000 ÷ 100,000) × $2.00 = **$9.60**.

---

# Total Estimated Monthly Guardrails Cost

| **Service**                                      | **Estimated Monthly Cost (USD)** |
|--------------------------------------------------|----------------------------------|
| Amazon SageMaker Clarify (Bias Detection)        | $21.00                           |
| Amazon Comprehend (Content Analysis)             | $16.00                           |
| Amazon Bedrock Model Evaluation (Drift Detection)| $100.00                          |
| Amazon SageMaker Model Monitor (Stability Check) | $15.00                           |
| AWS CloudTrail (Audit Logs)                      | $9.60                            |
| **Total**                                        | **$161.60**                      |
