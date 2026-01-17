# Docker Image Build and Push Workflow

This project uses **custom-built Docker images** for each microservice.

All images were built locally from source code using Dockerfiles and then pushed to Docker Hub for deployment via Docker Compose.

This document explains the complete image lifecycle.

---

## 📦 Microservices Covered

The project consists of **7 custom microservices**, each packaged as an independent Docker image.

| No | Microservice | Image Name |
|----|--------------|------------|
| 1 | Ecommerce UI | ecommerce-ui |
| 2 | Profile Management | profile-management |
| 3 | Product Catalog | product-catalog |
| 4 | Product Inventory | product-inventory |
| 5 | Order Management | order-management |
| 6 | Shipping & Handling | shipping-and-handling |
| 7 | Contact Support Team | contact-support-team |

---

## 📁 Source Code Structure

Each microservice has its own folder containing:

- Application source code
- Dependency files
- Dedicated Dockerfile

Example structure:

# Docker Image Build and Push Workflow

This project uses **custom-built Docker images** for each microservice.

All images were built locally from source code using Dockerfiles and then pushed to Docker Hub for deployment via Docker Compose.

This document explains the complete image lifecycle.

---

## 📦 Microservices Covered

The project consists of **7 custom microservices**, each packaged as an independent Docker image.

| No | Microservice | Image Name |
|----|--------------|------------|
| 1 | Ecommerce UI | ecommerce-ui |
| 2 | Profile Management | profile-management |
| 3 | Product Catalog | product-catalog |
| 4 | Product Inventory | product-inventory |
| 5 | Order Management | order-management |
| 6 | Shipping & Handling | shipping-and-handling |
| 7 | Contact Support Team | contact-support-team |

---

## 📁 Source Code Structure

Each microservice has its own folder containing:

- Application source code
- Dependency files
- Dedicated Dockerfile


This design allows each service to be:

- built independently
- versioned independently
- deployed independently

---

## 🔐 Docker Hub Authentication

Before pushing images, login to Docker Hub:

```bash
docker login
```
⚠️ Now Replace <dockerhub-username> with your own Docker Hub username.

## Ecommerce UI Microservice
```
cd ecommerce-ui

docker build -t <dockerhub-username>/ecommerce-ui .

docker push <dockerhub-username>/ecommerce-ui
```

## Profile Management Microservice
```
cd profile-management

docker build -t <dockerhub-username>/profile-management .

docker push <dockerhub-username>/ecommerce-ui
```

## Shipping and Handling Microservice
```
cd shipping-and-handling

docker build -t <dockerhub-username>/shipping-and-handling .

docker push <dockerhub-username>/shipping-and-handling
```

## Contact Support Team Microservice
```
cd contact-support-team

docker build -t <dockerhub-username>/contact-support-team .

docker push <dockerhub-username>/contact-support-team
```

## Product Inventory Microservice
```
cd product-inventory

docker build -t <dockerhub-username>/ product-inventory .

docker push <dockerhub-username>/product-inventory
```

## Product Catalog Microservice
```
cd product-catalog

docker build -t <dockerhub-username>/product-catalog .

docker push <dockerhub-username>/product-catalog
```

## Order Management Microservice
```
cd order-management

docker build -t <dockerhub-username>/order-management .

docker push <dockerhub-username>/order-management
```

### 🚀 Runtime Deployment

Once all images are pushed to Docker Hub, the entire platform can be deployed using:
```
docker compose up -d
```

Docker Compose will automatically:

pull all required images

create internal networks

create persistent volumes

start services in dependency order

### 🔁 Image Lifecycle Summary
```
Source Code
     ↓
Dockerfile
     ↓
docker build
     ↓
Docker Image
     ↓
docker push
     ↓
Docker Hub Registry
     ↓
docker compose pull
     ↓
docker compose up
```
###📌 Summary

This image build and push strategy reflects real-world DevOps practices used in enterprise environments:

One image per microservice

Independent versioning

Central image registry

Declarative runtime orchestration