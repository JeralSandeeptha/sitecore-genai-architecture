# ADR: Adoption of AWS Infrastructure using EKS and VPC

## Status
Proposed

## Context
Our project requires a scalable, secure, and production-ready cloud infrastructure to support containerized applications and future growth.

### Key Requirements
- Container orchestration for microservices
- High availability across multiple availability zones
- Secure networking with isolation between services
- Infrastructure as Code (IaC)
- CI/CD integration capability
- Observability and monitoring
- Support for horizontal scaling
- Managed services to reduce operational overhead

### Constraints
- Small DevOps team
- Need for production-grade reliability
- Cost optimization considerations
- Compliance with security best practices

### Alternatives Considered
- Self-managed Kubernetes on EC2
- ECS with Fargate
- Fully serverless architecture
- Other cloud providers

After evaluation, we decided to use AWS managed services, specifically:
- Amazon EKS (managed Kubernetes service)
- Amazon VPC (virtual network service)

## Decision
We will build our infrastructure on AWS using the following components:

### 1. Networking
- Dedicated Amazon VPC
- Public and private subnets across at least two Availability Zones
- Internet Gateway for public access
- NAT Gateway for outbound internet access from private subnets
- Security Groups and NACLs for network security
- VPC endpoints where appropriate

### 2. Kubernetes Platform
- Amazon EKS for managed Kubernetes control plane
- Managed node groups (EC2-based initially)
- Cluster Autoscaler enabled
- IAM Roles for Service Accounts (IRSA)

### 3. Infrastructure as Code
- Terraform for provisioning infrastructure
- Modular structure for VPC, EKS, IAM, and supporting services

### 4. Storage & Data
- Amazon EBS for persistent volumes
- Amazon S3 for object storage
- RDS (if relational database required)

### 5. Observability
- CloudWatch for logs and metrics
- Prometheus + Grafana (deployed in-cluster)
- Centralized logging

### 6. Security
- Private EKS cluster endpoint
- Least privilege IAM roles
- Secrets stored in AWS Secrets Manager
- Encryption at rest and in transit

### 7. CI/CD
- GitHub Actions (or similar)
- Image storage in Amazon ECR
- Automated deployments to EKS

## Consequences

### Positive
- Fully managed Kubernetes control plane reduces operational burden
- High availability across multiple AZs
- Scalable infrastructure with autoscaling
- Strong integration with AWS ecosystem
- Infrastructure reproducibility via Terraform
- Improved security posture using VPC isolation

### Negative
- Higher baseline cost (EKS control plane fee, NAT gateways)
- Increased complexity compared to simple EC2 deployment
- AWS vendor lock-in
- Requires Kubernetes expertise

### Trade-offs
- More initial setup complexity for long-term scalability and resilience
- Managed services cost more but reduce operational risk

## Alternatives Considered

### 1. Self-managed Kubernetes on EC2
Rejected due to:
- High operational overhead
- Control plane management burden
- Upgrade and security patch complexity

### 2. ECS with Fargate
Rejected because:
- Less Kubernetes ecosystem flexibility
- Migration risk if future multi-cloud strategy is adopted

### 3. Fully Serverless (Lambda-based)
Rejected because:
- Not suitable for long-running services
- Architectural limitations for our microservices

### 4. Other Cloud Providers
Rejected due to:
- Existing AWS familiarity
- Team experience
- Organizational alignment with AWS

## Date
2026-01-25

## Authors / Reviewers

**Authors:**
- DevOps Team
- Backend Lead

**Reviewers:**
- Engineering Manager
- Security Team
