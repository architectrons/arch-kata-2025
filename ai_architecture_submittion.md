# AI Architecture Submissions processing

```mermaid
sequenceDiagram
    participant Candidate
    participant Submissions API
    participant Submissions DB
    participant Preprocessing Lambda
    participant AI Grading Engine
    participant Expert Architect
    participant Notifications as Notifications Service
    participant Certification DB

    Candidate->>Submissions API: Upload Architecture Submission
    Submissions API->>Submissions DB: Store Submission Data
    Submissions DB-->>Preprocessing Lambda: Trigger Processing Event

    Preprocessing Lambda->>AI Grading Engine: Extract & Process Submission
    AI Grading Engine->>Submissions DB: Retrieve Past Submissions (Vector Search)

    Submissions DB-->>AI Grading Engine: Return Similar Submissions
    AI Grading Engine->>S3: Store formated prompt
    BackgroundJob-->>S3: Read propmpts to LLM in batch
    BackgroundJob-->>LLM: Run batch inference (Generate Initial Grade & Feedback)
    LLM-->>S3: Store response
    
    AI Grading Engine->>LLM: Generate Initial Grade & Feedback
    LLM-->>AI Grading Engine: Return Grading Results
    AI Grading Engine-->>S3: Read response from LLM
    AI Grading Engine->>Expert Architect: Send for Review & Approval
    Expert Architect->>Expert Architect: Review & Modify if Needed
    Expert Architect->>Submissions DB: Store Finalized Grade & Feedback
```

### Process Architecture Submission Files and store to DB

Detailed flow for `Preprocessing Lambda` mentioned in general flow

[Data processing AWS Costs](aws_costs.md#2-guardrails-costs-estimation)

```mermaid
sequenceDiagram
    participant DataIngestion
    participant AWS Textract
    participant AWS Comprehend
    participant AWS Rekognition
    participant Data Aggregator
    participant Submissions DB

    DataIngestion->>AWS Textract: Extract Text from PDF (OCR)
    AWS Textract-->>DataIngestion: Return Extracted Text

    DataIngestion->>AWS Comprehend: Analyze Text (NLP)
    AWS Comprehend-->>DataIngestion: Return Key Entities & Semantic Analysis

    DataIngestion->>AWS Rekognition: Analyze Diagrams (Object Detection)
    AWS Rekognition-->>DataIngestion: Return Extracted Diagram Components

    DataIngestion->>Data Aggregator: Combine Text & Diagram Data
    Data Aggregator-->>DataIngestion: Return Aggregated Analysis

    DataIngestion->>Submissions DB: Store Processed & Structured Submissions Data
```

### RAG workflow

```mermaid
sequenceDiagram
    participant AI Grading Engine
    participant Submissions DB as Submissions DB (Vector Search)
    participant LLm as Claude 3 (AWS Bedrock)

    AI Grading Engine->>Submissions DB: Convert Submission to Vector & Search
    Submissions DB-->>AI Grading Engine: Return Top N Similar Submissions
    
    AI Grading Engine->>AI Grading Engine: Construct Contextual Prompt
    AI Grading Engine->>LLM: Send Submission + Retrieved Examples
    LLM-->>AI Grading Engine: Return AI-Generated Grade & Feedback
```

### Contextual propmt example (Use Bedrock Model Evaluation to adjust prompt)

```
Use case: {USE_CASE}
Candidate's proposed architecture design: {PROCESSED_SUBMISSION}

[Relevant Past Submissions]
1. {HIGH_SCORE_SUBMISSION_EXAMPLE}
2. {LOW_SCORE_SUBMISSION_EXAMPLE}
3. {MEDIUM_SCORE_SUBMISSION_EXAMPLE}

[Grading Metrics]
- Accuracy Criteria: {KNOWLEDGE_BASE_ON_ACCURACY}
- Completeness Criteria: {KNOWLEDGE_BASE_ON_COMPLETENESS}
- Best Practices Compliance: {KNOWLEDGE_BASE_ON_COMPLIANCE}
- Match architecture patterns: {KNOWLEDGE_BASE_ON_ARCHITECTURE_PATTERNS}
```

### Data Indexing and Embeddings
```mermaid
flowchart TD
    A[Raw Documents] -->|Document Ingestion| B[Text nad Images Preprocessing]
    B -->|Chunking| C[Document Chunks]
    C -->|Embedding Model| D[Vector Embeddings]
    D -->|Indexing| E[Vector Database]
    E -->|Retrieval Queries| F[Relevant Document Embeddings]
```

## Backfill old submissions with vector represenatation

To be used as examples.

```mermaid
sequenceDiagram
    participant Batch Process Lambda
    participant Submissions DB (Old Data)
    participant Embeddings Model as AWS Titan Embedding
    participant Submissions DB (Vector Storage)

    Batch Process Lambda->>Submissions DB (Old Data): Fetch Old Submissions without Vectors
    Submissions DB (Old Data)-->>Batch Process Lambda: Return Submission Texts

    Batch Process Lambda->>Embeddings Model: Generate Embeddings
    Embeddings Model-->>Batch Process Lambda: Return Vectors

    Batch Process Lambda->>Submissions DB: Store Vector Representations
```
