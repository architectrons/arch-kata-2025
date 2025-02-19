# Aptitude Test Container Diagram (C2)

This diagram represents the high-level architecture of an aptitude test system. It outlines the key containers and their interactions.

![Aptitude Test Container](/C4/images/aptitude-test-container.drawio.svg)

The main goal of this component and the revised architecture is to pre-grade the short answer questions in addition to autograding the multiple choice questions. The key component in this architecture is the `AI Short Answer Grade Service` which acts as an orchestrator for the pre-grading process. 

## Key components and data flows
### AI Short Answer Grader Service
The `AI Short Answer Grader Service` automates the initial grading of short answer questions, leveraging AI to provide a preliminary assessment. This reduces the burden on expert architects, allowing them to focus on more complex or ambiguous answers identified by a confidence rating.

The `AI Short Answer Grader Service` receives short answer questions that candidates have provided during the aptitude test. The questions arrive indirectly via the `Aptitude PreGrading Service`. Specifically, the `Aptitude Test Taker Service` queues these short answer questions to the `topic: for_aptitude_pregrading queue`. The `Aptitude PreGrading Service` then consumes them from this queue and sends them to the 'AI Short Answer Grader Service`. The pregraded short answer, score, and confidence level are stored in the 'Aptitude Test Pregraded DB'. This information is then available for expert architects to review and adjust where necessary using the `Aptitude Manual Grader Service`.

### Aptitude PreGrading Service
The `Aptitude PreGrading Service` is a message consumer and forwarder, ensuring that short answer questions are delivered to the `AI Short Answer Grader Service for AI-powered pre-grading. The `Aptitude PreGrading Service` receives short answer questions from the `topic: for_aptitude_pregrading` queue using Apache Kafka as the technology. The `Aptitude Test Taker Service` then places these questions on the queue asynchronously during the test-taking process.

### Aptitude Manual Grader Service
The `Aptitude Manual Grader Service` provides the interface and logic for expert architects to review and validate the AI's pre-graded short answer questions, ensuring the accuracy and fairness of the grading process. They are now only required to grade those marked as 'low confidence' by the LLM. The expert architect's final score for the short answer question is stored in the Aptitude Test Grade DB.

### Key flows
1.  **Aptitude PreGrading Service --> AI Short Answer Grader:**
    *  Receives short answer questions from `topic: for_aptitude_pregrading` queue
    *  Sends short answer questions to `AI Short Answer Grader Service` for pre-grading
2.  **AI Short Answer Grader Service --> Aptitude Test Pregraded DB:**
    *   Recieve short answer questions via its API from `Aptitude PreGrading Service`
    *   Using an LLM and well-formatted prompts, the short answer questions are pregraded.
    *   The results of the AI pre-grading are stored in the `Aptitude Test Pregraded D`B.
3.  **Aptitude Manual Grader Service --> Aptitude Test Grade DB:**
    *   Retrieves pre-graded answers and allows the experts to review low-confidence answers.
    *   Final grades are stored in the `Aptitude Test Grade DB`.
      
## Key design considerations
*   **Asynchronous Processing:** The use of Apache Kafka queues is important for decoupling the `Aptitude Test Taker Service` from the grading services. This allows the system to handle a large volume of test submissions without overwhelming the grading components.
*   **AI Integration:** The system leverages AI for pre-grading short answer questions. This can significantly reduce the workload for expert architects, allowing them to focus on the most challenging or ambiguous answers.
*   **Clear Separation of Concerns:** The system is designed with a clear separation of concerns. Each service has a specific responsibility, making the system more maintainable and scalable.
*   **API Gateway:** The `Public API Gateway` is a central point of entry for all external requests, providing security, load balancing, and other API management features.

