# Architecture Solution Container (C2)

This diagram represents the high-level architecture of the architecture solution system. It outlines the key containers and their interactions.

![Architecture Solution Container](/C4/images/architecture-solution-container.drawio.svg)

The main goal of this component and the revised architecture is to pre-grade the architecture solution submissions. The key component in this architecture is the `AI Architecture Grader Service`, which acts as an orchestrator for the pre-grading process.

## Key components and data flows

### AI Architecture Solution Grader Service
The `AI Architecture Solution Grader Service` is a backend component that reviews and grades architecture solutions automatically using an LLM. It analyzes architecture solutions submitted by candidates and assigns a grade based on predefined criteria and the knowledge embedded in the Case Study vector database and provides it to the LLM as additional context.

### Architecture Manual Grader Service
This service allows expert architects to review architecture solutions submitted by candidates and assign grades. It bridges the gap between automated grading and human expertise, ensuring that candidates receive a thorough and accurate assessment of their architecture solutions. It helps us achieve 'Human-in-the-loop'. 

### Key flows
