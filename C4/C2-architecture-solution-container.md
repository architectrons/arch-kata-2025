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
1.  **Automated pre-grading:**
    *   Upon submission, the  `Architecture Solution Grader Service` (LLM-based) automatically reviews and grades the solution.
    *   The grade and feedback are stored in the `Architecture Grade and Feedback DB`.
    *   Submissions received from the `topic: for_solution_pregrading` Kafka topic trigger this process asynchronously.

2.  **Manual grading by experts:**
    *   `Expert Software Architects` use the `Expert Grading UI` to access solutions from the `Submission Grading DB` via the `Architecture Manual Grader Service`.
    *   Experts manually review the pre-graded solution while supplementing or overriding the automated review results. The grades and feedback will be stored in the `Architecture Grade and Feedback DB`.


## Key design considerations
*   **Asynchronous Processing:** The use of Apache Kafka queues is important for decoupling the `Architecture Submission Service` from the grading services. This allows the system to handle a large volume of architecture submissions without overwhelming the grading service.
*   **AI Integration:** The system leverages AI for pre-grading architecture case study solutions. This can significantly reduce the workload for expert architects, allowing them to focus on the most challenging solutions.
*   **Clear Separation of Concerns:** The system is designed with a clear separation of concerns. Each service has a specific responsibility, making the system more maintainable and scalable.
*   **API Gateway:** The `Public API Gateway` is a central point of entry for all external requests, providing security, load balancing, and other API management features.
