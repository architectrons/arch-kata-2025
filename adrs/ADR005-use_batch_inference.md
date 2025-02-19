# ADR: Use Bedrock Batch Inference For Grading Short Answers

## Status: Proposed  
## Date: 2025-02-18  
## Deciders: Architectrons

## Context and Problem Statement

The organization needs a cost-effective method for grading short answers using AI. Given the volume of responses, real-time inference is expensive and unnecessary, as the grading SLA allows one week for processing. The goal is to automate grading with minimal costs while ensuring scalability.

### Decision Drivers

- Cost reduction – Optimize cloud compute usage to minimize inference costs.  
- Batch processing sufficiency – The one-week SLA enables a batch processing approach instead of real-time inference.  
- Automation – Jobs should execute automatically when a new dataset is available.  
- Scalability – The solution should handle variable workloads efficiently.  

## Considered Options

1. Bedrock Batch Inference
2. Bedrock Real-time Inference

## Decision Outcome

### Chosen Option: "Bedrock Batch Inference"  
This option is selected because it provides the most cost-effective solution while meeting the one-week SLA and enabling automatic execution when new files are uploaded to S3.

### Consequences

- ✅ Good, because:
  - Cost-efficient – Charges only for batch jobs without maintaining real-time endpoints.  
  - Fully managed – No need to manage infrastructure for hosting models.  
  - Scales automatically – Can handle large numbers of responses without manual intervention.  
  - Native AWS Integration – Works seamlessly with S3 for storage and Step Functions/Lambda for job execution.  

- ❌ Bad, because:
  - Higher latency – Cannot provide immediate grading feedback.  
  - Batch job execution delays – Dependent on queue availability in AWS.  
