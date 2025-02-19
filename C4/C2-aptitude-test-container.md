# Aptitude Test Container Diagram (C2)

This diagram represents the high-level architecture of an aptitude test system. It outlines the key containers and their interactions.

![Aptitude Test Container](/C4/images/aptitude-test-container.drawio.svg)

The main goal of this component and the revised architecture is to pregrade the short answer questions in addition to autograding the multiple choice questions. The key component in this architecture is the `AI Short Answer Grade Service` which acts as an orchestrator for the pregrading process. 

## Key components and data flows

### AI Short Answer Grader Service

### Aptitude PreGrading Service

### Aptitude Manual Grader Service
This component allows expert architects to review pregraded short answer questions. They are now only required to grade those marked as 'low confidence' by the LLM.

### Key flows
1.  **Aptitude PreGrading Service --> AI Short Answer Grader:**
    *  Receives short answer questions from `topic: for_aptitude_pregrading` queue
    *  Sends short answer questions to `AI Short Answer Grader Service` for pre-grading
2.  **AI Short Answer Grader Service --> Aptitude Test Pregraded DB:**
    *   Recieve short answer questions via its API from `Aptitude PreGrading Service`
    *   Using an LLM and well-formatted prompts, the short answer questions are pregraded.
    *   The results of the AI pre-grading are stored in the `Aptitude Test Pregraded D`B.
  
## Key design considerations
*   **Asynchronous Processing:** The use of Apache Kafka queues is important for decoupling the `Aptitude Test Taker Service` from the grading services. This allows the system to handle a large volume of test submissions without overwhelming the grading components.
*   **AI Integration:** The system leverages AI for pre-grading short answer questions. This can significantly reduce the workload for expert architects, allowing them to focus on the most challenging or ambiguous answers.
*   **Clear Separation of Concerns:** The system is designed with a clear separation of concerns. Each service has a specific responsibility, making the system more maintainable and scalable.
*   **API Gateway:** The `Public API Gateway` is a central point of entry for all external requests, providing security, load balancing, and other API management features.

