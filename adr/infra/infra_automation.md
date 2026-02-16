# ADR: Adoption of AWS Infrastructure using EKS, VPC, and Terraform

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
- Automated and repeatable infrastructure provisioning

### Constraints
- Small DevOps team
- Need for production-grade reliability
- Cost optimization considerations
- Compliance with security best practices
- Minimize manual infrastructure changes

### Alternatives Considered
- Self-managed Kubernetes on EC2
- ECS with Fargate
- Fully serverless architecture
- Manual infrastructure provisioning
- Other cloud providers

After evaluation, we decided to use AWS managed services combined with Terraform for Infrastructure as Code.

## Decision
We will build and manage our infrastructure on AWS using the following components:

### 1. Infrastructure as Code (Primary Automation Tool)
- Terraform will be used for provisioning and managing all infrastructure.
- Modular Terraform structure (VPC, EKS, IAM, Networking, Storage).
- Remote backend for state management (e.g., S3 + DynamoDB locking).
- CI/CD integration for automated Terraform plan and apply.
- Version-controlled infrastructure in Git.

### 2. Networking
- Dedicated Amazon VPC
- Public and private subnets across at least two Availability Zones
- Internet Gateway for public access
- NAT Gateway for outbound internet access from private subnets
- Security Groups and NACLs for network security
- VPC endpoints where appropriate

### 3. Kubernetes Platform
- Amazon EKS for managed Kubernetes control plane
- Managed node groups (EC2-based initially)
- Cluster Autoscaler enabled
- IAM Roles for Service Accounts (IRSA)

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
- Automated Terraform validation and deployment pipeline

## Consequences

### Positive
- Fully automated, reproducible infrastructure
- Reduced manual configuration errors
- Version-controlled infrastructure changes
- Managed Kubernetes reduces operational burden
- High availability across multiple AZs
- Scalable architecture with autoscaling
- Strong AWS ecosystem integration

### Negative
- Additional learning curve for Terraform modules and state management
- Requires disciplined state handling and backend configuration
- Higher baseline AWS costs (EKS control plane, NAT gateways)
- AWS vendor lock-in

### Trade-offs
- Increased upfront setup complexity for long-term scalability and stability
- Managed services cost more but significantly reduce operational risk

## Alternatives Considered

### 1. Manual Infrastructure Provisioning
Rejected due to:
- High risk of configuration drift
- No version control
- Difficult environment replication

### 2. Self-managed Kubernetes on EC2
Rejected due to:
- High operational overhead
- Control plane management burden
- Upgrade and security patch complexity

### 3. ECS with Fargate
Rejected because:
- Less Kubernetes ecosystem flexibility
- Migration risk if multi-cloud strategy is required

### 4. Fully Serverless (Lambda-based)
Rejected because:
- Not suitable for long-running services
- Architectural limitations for our microservices

## Date
2026-01-25

## Authors / Reviewers

**Authors:**
- DevOps Team
- Backend Lead

**Reviewers:**
- Engineering Manager
- Security Team
