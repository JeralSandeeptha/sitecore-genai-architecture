# Features and Requirements

## 1. Functional Requirements

### 1.1 Authentication

- Users must be able to sign up
- Users must be able to log in
- JWT-based / OAuth based authentication
- Secure password storage

---

### 1.2 Profile Management

Users can update:

- basic user details
- add / update v0 API Key

System requirements:

- The system must encrypt API keys before storing

---

### 1.3 v0 Integration

- The system must use the user’s v0 API key
- The system must create a new chat in the user’s personal v0 account
- The system must send:
  - Prompt
  - Optional image
  - Retrieved RAG context

---

### 1.4 RAG Component Generation

- The system must retrieve relevant components from vector database
- Use Qdrant for similarity search
- Inject Sitecore field patterns into the prompt

The system must generate:

- React component
- TypeScript code
- Sitecore field bindings

---

### 1.5 Microservice Responsibilities

#### User Service

- Manage users
- Store API keys
- Handle profile updates

#### AI Service

- Retrieve user API key
- Process prompt
- Send data to RabbitMQ

#### Code Generation Service

- Consume RabbitMQ messages
- Call v0 API

#### Knowledge Service (Python)

- Store embeddings in Qdrant
- Handle vector search

#### Gateway Service

- Connect all the services via this service

---

## 2. Non-Functional Requirements

- High scalability
- Secure API key encryption
- 99% uptime target
- Horizontal scaling capability
- Microservice isolation
