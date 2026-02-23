# Teralis Architecture Repository

This repository contains the complete **software architecture documentation** for the project, including system design artifacts, architectural decisions, and deployment details.  
It serves as a **single source of truth** for understanding the system’s structure, behavior, and rationale behind design choices.

---

## Table of Contents

### 1. **Software Requirements Specification (SRS)**
- Defines the project’s purpose, scope, and objectives.  
- Includes detailed **functional and non-functional requirements**.  
- Serves as a reference for development, QA, and future scaling decisions.

### 2. **System Architecture**
- High-level system design and component interactions.  
- Includes:
  - Architectural diagrams (C4 model / UML)
  - Technology stack overview
  - Data flow and API design
  - Integration and communication patterns

### 3. **Kubernetes (K8s) Configuration**
- Deployment and infrastructure setup for containerized services.  
- Includes:
  - Deployment manifests
  - Services, Ingress, and ConfigMaps
  - CI/CD pipeline integration overview
  - Scalability and resilience strategies

### 4. **Architecture Decision Records (ADR)**
- A collection of documented **key design decisions** made during system evolution.  
- Each ADR includes:
  - **Context** — background and motivation  
  - **Decision** — the chosen solution  
  - **Consequences** — trade-offs and implications  
- Promotes transparency and long-term maintainability.

---

## ⚙️ Technologies Covered
- **Backend:** _e.g., Spring Boot / Express / .NET / Django_  
- **Frontend:** _e.g., React / Angular / Vue_  
- **Database:** _e.g., PostgreSQL / MySQL / MongoDB_  
- **Infrastructure:** Docker, Kubernetes, Nginx, CI/CD (GitHub Actions / Jenkins)  
- **Cloud / Deployment:** _e.g., AWS / GCP / Azure_
- **AI:** _e.g., *RAG Architecture*

---

## 🧩 Purpose
This repository is intended for:
- **Developers** — to understand system design decisions.  
- **Architects** — to analyze and refine the overall architecture.  
- **New team members** — to quickly onboard and grasp the project structure.  
- **Stakeholders** — to view the system from a high-level business perspective.

---

## 📁 Repository Structure

```bash
├── srs/
│   └── software_requirements_specification.md
├── infra/
│   ├── diagrams/
│   └── system_architecture_overview.md
│   └── system_architecture_overview.drawio
├── k8s/
│   ├── deployments/
│   └── services/
├── adr/
│   ├── 001-initial-architecture-decision.md
│   └── 002-database-choice.md
└── README.md
```

---

## 🧭 How to Use
1. Start with the **SRS** to understand the problem space.  
2. Explore the **Architecture** section for design and component details.  
3. Review **ADRs** to learn the reasoning behind major decisions.  
4. Use the **K8s configs** for deployment and scalability insights.

---

## 👤 Author
**Jeral Sandeeptha**  
Full Stack Software Engineer  
📧 [jeral.sandeeptha1@gmail.com](mailto:jeral.sandeeptha1@gmail.com)  
🌐 [LinkedIn](https://www.linkedin.com/in/jeral-sandeeptha-983b38253/)
