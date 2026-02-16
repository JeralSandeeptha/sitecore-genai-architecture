# ADR: Adoption of FastAPI for Knowledge Service (Vector Database Interaction Layer)

## Status
Accepted

## Context
Our system requires a backend service responsible for:

- Handling user queries
- Interacting with the vector database
- Coordinating Retrieval-Augmented Generation (RAG) workflows
- Exposing REST APIs for knowledge-based interactions
- Managing document ingestion and retrieval processes

Key requirements:
- High-performance API framework
- Asynchronous request handling
- Easy integration with LangChain
- Strong typing and validation
- Lightweight and scalable
- Compatibility with deployment on EKS
- Support for OpenAPI documentation

Constraints:
- Must integrate cleanly with our existing AWS + EKS infrastructure
- Must support async operations for vector database and LLM calls
- Minimal operational overhead
- Easy maintainability for backend engineers

Alternatives considered:
- Flask
- Django / Django REST Framework
- Node.js (Express/NestJS)
- Golang-based services

After evaluation, we decided to use FastAPI as the primary framework for the Knowledge Service.

## Decision
We will implement the Knowledge Service using FastAPI.

### 1. Responsibilities of the Knowledge Service
- Accept user queries via REST endpoints
- Process requests using LangChain RAG pipeline
- Interact with vector database for similarity search
- Manage document ingestion and indexing
- Handle embeddings generation workflow
- Return structured responses (JSON)

### 2. Architecture Integration
- Deployed as a containerized service on EKS
- Communicates with:
  - Vector database
  - LLM provider
  - Object storage (for documents)
- Integrated with logging and monitoring stack
- Exposed internally via Kubernetes service (or via API gateway if needed)

### 3. Technical Implementation
- Async endpoints using Python async/await
- Pydantic models for request/response validation
- Dependency injection for service layers
- Middleware for logging and authentication
- Health check and readiness endpoints for Kubernetes

### 4. Scalability
- Horizontally scalable via Kubernetes HPA
- Stateless service design
- Configurable through environment variables

## Consequences

### Positive
- High-performance asynchronous framework
- Automatic API documentation (OpenAPI/Swagger)
- Strong typing and validation using Pydantic
- Lightweight and easy to maintain
- Strong compatibility with LangChain ecosystem
- Faster development compared to heavier frameworks

### Negative
- Requires async programming discipline
- Smaller ecosystem compared to Django
- Dependency on Python runtime performance

### Trade-offs

- Choosing lightweight performance-focused framework over full-stack framework
- Favoring flexibility and speed over built-in admin and ORM features

## Alternatives Considered

### 1. Flask
Rejected due to:
- Lack of native async support (without extensions)
- Less structured validation out-of-the-box

### 2. Django / DRF
Rejected because:
- Heavier framework than required
- Unnecessary features for microservice architecture

### 3. Node.js (Express/NestJS)
Rejected due to:
- Additional ecosystem complexity
- Team stronger expertise in Python

### 4. Golang Service
Rejected because:
- Increased development time
- Less direct integration with LangChain (Python-native)

## Date
2026-01-25

## Authors / Reviewers

**Authors:**
- Backend Engineering Team
- AI Engineering Team

**Reviewers:**
- Engineering Manager
- Architecture Review Board
