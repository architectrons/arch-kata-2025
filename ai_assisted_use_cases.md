# AI assisted Use Cases generation

Use AI scheduled job generates 10 new Use Cases for Expert review once a week.

```mermaid
sequenceDiagram
    participant Scheduler as Cron Scheduler - EventBridge
    participant Batch as AWS Batch - Generate Use Cases
    participant DB as Vector DB
    participant S3 as S3
    participant Bedrock as Bedrock
    participant LLM as LLM
    participant DMSJob as DMS Job
    participant Expert as Expert Architect
    participant AdminUI as Admin UI

    Scheduler ->> Batch: Triggers Batch Job
    Batch ->> DB: Retrieve Similar Use Cases (10)
    DB ->> Batch: Pass Retrieved Data
    Batch ->> S3: Store prompts to LLM with context in a file
    Bedrock ->> S3: Read prompts file
    Bedrock ->> LLM: Generate New Use Cases (10)
    LLM ->> S3: Store generated use cases
    DMSJob ->> DB: Write use cases to DB in pending state
    Expert ->> AdminUI: Fetch Pending Use Cases
    AdminUI ->> DB: Submit Approval or Edits
```

## AI Evals. Accuracy and Similiarity

```mermaid
sequenceDiagram
    participant Clarify as SageMaker Clarify
    participant DB as Vector DB
    participant Analytics as Amazon Quicksights

    Clarify->>DB: Retrieve Most Similar Expert-Approved Use Cases
    DB->>Clarify: Return Best-Matching Cases
    Clarify->>Clarify: Compute BLEU, ROUGE, and Cosine Similarity
    Clarify->>Analytics: Log Accuracy Metrics
```

| **Metric** | **Description** |
|------------|----------------|
| **BLEU Score** | Measures text similarity between AI-generated and expert-approved use cases. |
| **ROUGE Score** | Evaluates how much AI-generated use cases overlap with best practices. |
| **Cosine Similarity** | Checks if AI-generated use cases are semantically close to expert cases. |
