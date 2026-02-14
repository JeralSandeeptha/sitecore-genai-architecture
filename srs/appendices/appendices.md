# Appendices

---

### Appendix A – System Architecture Diagram (Logical)

```
User  
↓  
Frontend  
↓  
API Gateway  
↓  

| User Service (MongoDB)       |  
| AI Service                   |  
| Knowledge Service (Qdrant)   |  
| RabbitMQ                     |  
| Code Generation Service      |  

↓  
v0 Platform (User Account)
```

---

## Appendix B – Database Schema (Simplified)

### User Collection (MongoDB)

```json
{
  "_id": "ObjectId",
  "name": "string",
  "email": "string",
  "password": "hashed",
  "v0ApiKey": "encrypted_string",
  "createdAt": "date",
  "updatedAt": "date"
}
```

## Appendix C – Future Enhancements
- Component versioning
- Template marketplace
- Team collaboration
- Component preview sandbox
- Auto deployment to XM Cloud
- Billing & subscription system