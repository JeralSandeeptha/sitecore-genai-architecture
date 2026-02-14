# Overall Description

### Product Perspective

This platform is a **cloud-native microservices system** designed to integrate:

- Sitecore XM Cloud Marketplace Application
- Next.js frontend templates
- AI-based component generation
- Vector-based RAG knowledge retrieval

### Architecture Flow

The system follows a distributed architecture pattern to ensure scalability, modularity, and high availability.

```
Frontend → API Gateway → AI service → Message Queue → Code Generation → v0
```

---

### Product Functions

The system allows users to:

- Register & Login
- Manage Profile
- Connect v0 account via adding v0 API Key
- Submit Prompt + Image
- Generate AI-powered Sitecore component
- Personalized chat creation / Automatically create a new chat in their personal v0 account
- Retrieve generated component code

---

### User Classes

| User Type       | Description                                  |
|----------------|----------------------------------------------|
| Sales Engineer | Creates and customizes Sitecore templates    |
| Admin          | Monitors system and manages users            |

---

### Operating Environment

| Layer        | Technology                         |
|-------------|------------------------------------|
| Frontend    | Next.js / React                    |
| Backend     | Express.js & Flask                 |
| Database    | MongoDB                            |
| Vector DB   | Qdrant                             |
| Message Queue | RabbitMQ                         |
| DevOps      | Docker, Kubernetes, GitHub Actions |
| Cloud       | AWS                                |
| Code Generation | v0                             |
| Infrastructure Automation | Terraform                             |

---

### Constraints

- Users must provide their own v0 API key.
- All AI generation must respect Sitecore field structures.
- Services must scale via Kubernetes.
