# Architecture Documentation

## Overview

This project implements a **microservices-based e-commerce platform** deployed using **Docker Compose** on an **AWS EC2 instance**.

Each business capability is developed, deployed, and scaled independently while communicating over Docker’s internal networking.

The architecture follows industry-standard principles used in real production systems.

---

## Architecture Diagram

![Architecture Diagram](Screenshots/architecture.png)

---

## Core Architectural Principles

- Microservices architecture
- Database-per-service pattern
- Stateless application containers
- Stateful databases using persistent volumes
- Internal-only service communication
- External access limited to application APIs
- Cloud-ready deployment model

---

## Service Communication Model

All containers are connected to a **single Docker bridge network** automatically created by Docker Compose.

Docker provides:

- Internal DNS resolution
- Service discovery using container names
- Isolated private networking

### Example:

product-inventory → postgres_product_inventory

order-management → product-inventory

ecommerce-ui → backend APIs
```

No IP addresses are hardcoded.

---

## Request Flow Example

### User placing an order:

1. User accesses React UI (`ecommerce-ui`)
2. UI calls `profile-management` for authentication
3. UI fetches products from `product-catalog`
4. Inventory validation via `product-inventory`
5. Order created in `order-management`
6. Shipping triggered via `shipping-and-handling`
7. Support requests handled by `contact-support-team`

All traffic remains internal to Docker except frontend access.

---

## Microservices Breakdown

| Service | Technology | Database |
|------|-----------|----------|
| ecommerce-ui | React | None |
| profile-management | Python | MySQL |
| product-catalog | Node.js | MongoDB |
| product-inventory | Python | PostgreSQL |
| order-management | Java (Spring Boot) | MongoDB |
| shipping-and-handling | Go | MongoDB |
| contact-support-team | Python | MongoDB |

---

## Database Architecture

The system uses **polyglot persistence**.

Each service owns its database:

- No database sharing
- No cross-service joins
- Independent schema lifecycle

### Databases Used

| Database | Used By |
|--------|---------|
| MySQL 8 | Profile Management |
| PostgreSQL | Inventory |
| MongoDB | Catalog, Orders, Shipping, Support |

---

## Persistent Storage Model

All databases use Docker volumes:

/var/lib/mysql
/var/lib/postgresql
/data/db


This ensures:

- Data persistence across restarts
- Safe container recreation
- Production-aligned durability

---

## Security Model

- Databases not exposed publicly
- Only application ports are published
- Internal communication via Docker bridge network
- Credentials injected using environment variables
- No secrets embedded inside Docker images

This model closely mirrors private subnet communication inside AWS VPCs.

---

## Cloud Deployment Architecture

- Platform: AWS EC2
- OS: Ubuntu 22.04 LTS
- Container Runtime: Docker
- Orchestration: Docker Compose
- Storage: EBS root volume (100 GB)

This architecture is fully compatible with future migration to:

- Amazon ECS
- Kubernetes (EKS)

---

## Scalability Considerations

- Stateless services can be horizontally scaled
- Databases remain isolated per service
- Load balancer can be added in front of frontend
- Reverse proxy (NGINX) can manage HTTPS

---

## Summary

This architecture demonstrates:

- Real-world microservices design
- Cloud-ready container deployment
- Strong separation of concerns
- Secure service communication
- Production-style operational model



