# ADR: Adoption of MongoDB for User and Task Services

## Status
Accepted

## Context

Our system includes User and Task services that require:

- Storage of user profiles and authentication-related data
- Storage of task definitions and task execution metadata
- Flexible schema to support evolving requirements
- High availability and scalability
- Fast read/write performance
- Easy integration with backend services (FastAPI)

Key requirements:

- JSON-like document storage
- Horizontal scalability
- Indexing support
- Replication and high availability
- Managed or self-hosted deployment options
- Compatibility with AWS infrastructure

Constraints:

- Must integrate with services deployed on EKS
- Support for containerized or managed deployment
- Minimal schema migration overhead
- Operational simplicity

Alternatives considered:

- PostgreSQL
- MySQL
- DynamoDB
- Cassandra

After evaluation, we decided to adopt MongoDB as the primary database for User and Task services.

## Decision

We will use MongoDB to store and manage data for:

- User Service
- Task Service

### 1. Data Responsibilities

#### User Service
- User profiles
- Role and permission mappings
- Account metadata
- Audit information

#### Task Service
- Task definitions
- Task status and lifecycle state
- Execution logs (metadata level)
- Associated user references

### 2. Deployment Strategy

- Deployed as:
  - Managed service (recommended: MongoDB Atlas) OR
  - Self-hosted cluster within AWS
- Configured with:
  - Replica set for high availability
  - Automated backups
  - Indexing strategy for performance

### 3. Integration

- Accessed by FastAPI-based services
- Uses asynchronous MongoDB drivers
- Environment-based configuration
- Internal network access only (not publicly exposed)

### 4. Data Modeling Approach

- Document-oriented schema
- Denormalized where appropriate
- Indexed frequently queried fields
- Soft deletes for audit retention (if required)

## Consequences

### Positive

- Flexible schema for evolving business requirements
- Easy mapping to JSON-based APIs
- Horizontal scalability
- Strong ecosystem and tooling
- Faster development compared to strict relational schemas

### Negative

- No enforced relational constraints (must be handled in application)
- Potential for inconsistent schema if not governed properly
- Requires careful indexing for performance optimization

### Trade-offs

- Flexibility over strict relational consistency
- Faster iteration over rigid schema enforcement
- Document modeling complexity over normalized relational modeling

## Alternatives Considered

### 1. PostgreSQL

Rejected due to:
- Rigid schema migrations
- Less flexible for rapidly evolving task structures

### 2. MySQL

Rejected because:
- Similar relational constraints
- Less suited for flexible document storage needs

### 3. DynamoDB

Rejected due to:
- AWS vendor lock-in concerns
- More complex access patterns for certain queries

### 4. Cassandra

Rejected because:
- Operational complexity
- Overkill for current workload requirements

## Date
2026-01-25

## Authors / Reviewers

**Authors:**
- Backend Engineering Team
- DevOps Team

**Reviewers:**
- Engineering Manager
- Architecture Review Board
