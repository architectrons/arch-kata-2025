# Constraints

## Overview
This document outlines the constraints that impact the architecture and design of the AI-powered certification system. These constraints ensure that the solution aligns with business goals, technical limitations, and regulatory requirements.

## Constraints Table

| ID  | Description | Priority | Related Business Goals |
|-----|------------|----------|-----------------------|
| C-1 | The certification exam cost of $800 is fixed and cannot be adjusted. | Hard | None |
| C-2 | Certification grading turnaround times must be maintained at one week for both tests to uphold service commitments. | Hard | BG-1, BG-5 |
| C-3 | Accuracy in test grading and certification results must be maintained to protect company credibility and candidate career outcomes. | Hard | BG-4 |
| C-4 | AI implementation costs must be managed to avoid significant cost overruns. | Soft | BG-5, BG-6 |
| C-5 | Expert software architects must remain involved in the certification process for grading and quality assurance. | Hard | BG-3, BG-4 |
| C-6 | The system must handle the projected 5-10X increase in certification requests without service degradation. | Hard | BG-1 |
| C-7 | The system must comply with potential regional data privacy and security regulations (e.g., GDPR in Europe, local regulations in Asia). | Soft | BG-2 |
| C-8 | Ensure high availability and low latency of the certification platform for candidates across multiple regions. | Soft | BG-2 |
| C-9 | AI must ensure **fairness and prevent grading bias** to maintain certification credibility. | Hard | BG-4 |
| C-10 | AI-generated grades must be **explainable and interpretable** to provide clear justification for scores. | Hard | BG-4 |

[Back to Index](index.md)
