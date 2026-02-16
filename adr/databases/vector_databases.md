# ADR: Adoption of Qdrant as Vector Database

## Status
Accepted

## Context

Our system implements a Retrieval-Augmented Generation (RAG) architecture that requires:

- Efficient vector similarity search
- Storage of embeddings with metadata
- High-performance nearest neighbor search
- Filtering capabilities on structured metadata
- Scalability for growing document corpus
- Kubernetes-native deployment
- Production-ready reliability

Key requirements:

- Low-latency similarity search
- Support for hybrid filtering (vector + metadata)
- REST and gRPC APIs
- Horizontal scalability
- Easy deployment on EKS
- Integration with LangChain
- Cost-effective compared to fully managed SaaS vector DBs

Constraints:

- Must run inside our AWS infrastructure
- Should support containerized deployment
- Avoid vendor lock-in to proprietary hosted services
- Minimal operational overhead

Alternatives considered:

- Pinecone
- Weaviate
- Milvus
- OpenSearch (vector search)
- PostgreSQL with pgvector

After evaluation, we decided to adopt Qdrant as the primary vector database.

## Decision
We will use Qdrant as our vector database for storing embeddings and performing similarity search.

### 1. Responsibilities
- Store embedding vectors
- Store associated metadata
- Perform nearest neighbor similarity search
- Support metadata filtering
- Enable collection-based organization

### 2. Deployment Architecture
- Deployed as a containerized service on EKS
- Persistent storage via attached volumes
- Internal cluster networking (not publicly exposed)
- Horizontal scaling enabled if required
- Backups configured for persistence and disaster recovery

### 3. Integration
- Integrated with LangChain retrievers
- Accessed by Knowledge Service (FastAPI)
- Used for:
  - Document retrieval
  - Context generation for RAG
  - Semantic search features

### 4. Performance Considerations
- HNSW indexing for efficient ANN search
- Tunable performance parameters
- Optimized for read-heavy workloads

## Consequences

### Positive
- High-performance similarity search
- Open-source and self-hostable
- Strong filtering support
- Kubernetes-friendly deployment
- Good LangChain integration
- Lower cost compared to managed SaaS vector databases

### Negative
- Operational responsibility for scaling and backups
- Requires monitoring and performance tuning
- Additional infrastructure component to manage

### Trade-offs
- Accept operational overhead in exchange for cost control and infrastructure ownership
- Self-managed flexibility over fully managed convenience

## Alternatives Considered

### 1. Pinecone
Rejected due to:
- SaaS-only model
- Higher recurring cost
- Vendor lock-in concerns

### 2. Weaviate
Rejected because:
- Heavier architecture
- More operational complexity for our use case

### 3. Milvus
Rejected due to:
- Higher infrastructure requirements
- More complex distributed setup

### 4. PostgreSQL with pgvector
Rejected because:
- Not optimized for large-scale ANN workloads
- Limited performance at high embedding volumes

### 5. OpenSearch Vector Search
Rejected because:
- Primarily search engine-focused
- Less optimized for high-dimensional embedding workloads

## Date
2026-01-25

## Authors / Reviewers

**Authors:**
- AI Engineering Team
- DevOps Team

**Reviewers:**
- Engineering Manager
- Architecture Review Board
