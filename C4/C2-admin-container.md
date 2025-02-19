# Administrator Container Diagram (C2)

This container diagram description provides a structured overview of the SoftArchCert administrative system's architecture. It highlights the key containers, their responsibilities, and how they interact with each other.

![Administrator Container](/C4/images/admin-container.drawio.svg)

In summary, AI components of this system revolve around using LLMs to create vector embeddings of aptitude tests and case studies, enabling semantic search and AI-powered analysis. The *AI Certification Maintenance Service* is the orchestrator for generating these embeddings, which are then stored in PostgreSQL databases using the pgvector extension (See [ADR002](/adrs/ADR002-use-pgvector-pinecone.md)). What this approach aims to achieve is to improve the management, analysis, efficiency and potentially the quality of the certification process. There is no direct interaction between the candidates and this sub-system.

