# ADR: Adoption of Microservices Architecture for Backend RAG System

## Status
Accepted

## Context

Our backend system supports a Retrieval-Augmented Generation (RAG) platform consisting of:

- Knowledge Service (RAG orchestration)
- User Service
- Task Service
- Vector Database
- LLM integrations
- Document ingestion workflows

As the system grows in complexity, we require:

- Independent service scalability
- Clear separation of responsibilities
- Independent deployment cycles
- Fault isolation
- Technology flexibility across services
- Improved maintainability

Key requirements:

- Containerized deployment on Kubernetes (EKS)
- API-based inter-service communication
- Independent scaling per service
- Clear domain boundaries
- CI/CD per service
- Observability across services

Constraints:

- Must integrate with AWS + EKS infrastructure
- Minimize tight coupling between services
- Avoid monolithic bottlenecks
- Maintain operational simplicity

Alternatives considered:

- Monolithic architecture
- Modular monolith
- Serverless-first architecture

After evaluation, we decided to adopt a microservices architecture for the backend RAG system.

## Decision

We will implement the backend using a microservices architecture.

### 1. Service Boundaries

Each service will have clear ownership and responsibility:

- Knowledge Service  
  - Handles RAG orchestration  
  - Interacts with vector database  
  - Calls LLM providers  

- User Service  
  - Manages user profiles and authentication data  

- Task Service  
  - Manages task definitions and lifecycle  

- Vector Database Service  
  - Stores embeddings  
  - Provides similarity search  

Each service will:

- Be independently deployable
- Have its own API
- Own its data storage
- Be containerized and deployed on EKS

### 2. Communication Model

- REST-based communication between services
- Internal Kubernetes networking
- Service discovery via Kubernetes services
- Optional API Gateway for external access

### 3. Deployment Strategy

- Each service packaged as Docker container
- Independent CI/CD pipelines
- Horizontal Pod Autoscaling (HPA)
- Environment-based configuration
- Health checks and readiness probes

### 4. Data Ownership

- Each service owns its database
- No shared databases between services
- Communication only via APIs
- Event-driven integration can be introduced if needed

## Consequences

### Positive

- Independent scalability per service
- Better fault isolation
- Faster development across teams
- Independent deployments
- Clear domain ownership
- Technology flexibility per service

### Negative

- Increased operational complexity
- Network latency between services
- Distributed debugging challenges
- Requires strong observability and logging
- More CI/CD pipelines to manage

### Trade-offs

- Accept operational complexity for scalability and maintainability
- Distributed system overhead in exchange for modularity and resilience

## Alternatives Considered

### 1. Monolithic Architecture

Rejected due to:
- Tight coupling of components
- Difficult scaling of specific modules
- Slower deployments
- Reduced fault isolation

### 2. Modular Monolith

Rejected because:
- Still limited independent scaling
- Harder long-term evolution into distributed services

### 3. Serverless-First Architecture

Rejected due to:
- Not ideal for long-running RAG workflows
- Limited flexibility for vector database integration
- Cold-start considerations

## Date
2026-01-25

## Authors / Reviewers

**Authors:**
- Backend Engineering Team
- AI Engineering Team
- DevOps Team

**Reviewers:**
- Engineering Manager
- Architecture Review Board
