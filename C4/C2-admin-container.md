# Administrator Container Diagram (C2)

This container diagram description provides a structured overview of the SoftArchCert administrative system's architecture. It highlights the key containers, their responsibilities, and how they interact with each other.

![Administrator Container](/C4/images/admin-container.drawio.svg)

Ihe AI components of this system revolve around using LLMs to create vector embeddings of aptitude tests and case studies, enabling semantic search and AI-powered analysis. The *AI Certification Maintenance Service* is the orchestrator for generating these embeddings, which are then stored in PostgreSQL databases using the pgvector extension (See [ADR002](/adrs/ADR002-use-pgvector-pinecone.md)). This approach aims to improve the management, analysis, efficiency and quality of the certification process. There is no direct interaction between the candidates and this sub-system.

## Key components and data flows

### AI Certification Maintenance Service
This is the central AI component. Its primary responsibility is to orchestrate all interactions, which include embedding aptitude tests and architecture case studies into a vector database to represent the semantic meanings of the aptitude tests and the criteria chunks of the case studies. This helps enable similarity searches and other functionalities. The core of this component is Txtai (See [ADR003](/adrs/ADR003-use-txtai-langchain.md)).

### Key flows
1.  **Aptitude Test Maintenance Service --> AI Certification Maintenance Service:**
    *  When an administrator adds, removes, or modifies aptitude test questions via the `Aptitude Test Maintenance Service`, the system triggers the creation of embeddings for these tests.
    *  The `AI Certification Maintenance Service` takes these test questions and uses *Txtai* to generate vector embeddings.
    *  These embeddings and the original test data are then stored in the *Aptitude Test DB*
2.  **Case Study Maintenance Service --> AI Certification Maintenance Service:**
    *   Similar to the aptitude tests, embeddings are created when administrators manage case studies through the `Case Study Maintenance Service`.
    *   The `AI Certification Maintenance Service` processes these case studies, generating vector embeddings using *Txtai*.
    *   These embeddings and the case study data are stored in the *Case Study DB* (also PostgreSQL with pgvector).
3.  **Aptitude Test Analysis Service --> Aptitude Test Grade DB:**
    *   The `Aptitude Test Analysis Service` uses the historical test reports stored in the `Aptitude Test Grade DB` to analyze questions.
    *   The historical test reports are used for further analysis using an LLM, as described in the detailed description of the `AI Certification Maintenance Service`.
