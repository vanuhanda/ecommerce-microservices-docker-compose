# ecommerce-microservices-docker-compose
E-commerce microservices platform deployed with Docker Compose on AWS EC2, featuring a React frontend, multiple backend services, polyglot databases, internal container networking, and persistent storage.

# 🛒 E-Commerce Microservices Platform (Docker Compose + AWS EC2)

## 📌 Overview

This repository contains a **production-style e-commerce microservices platform** deployed using **Docker Compose** on an **AWS EC2 instance (Ubuntu 22.04)**.

The project demonstrates real-world concepts such as:
- Microservices architecture
- Inter-container communication using Docker networking
- Polyglot persistence (MySQL, PostgreSQL, MongoDB)
- Persistent storage using Docker volumes
- Secure internal service communication
- Cloud deployment on AWS EC2

This project is designed to reflect **enterprise-grade deployment practices** and serves as a strong portfolio project for **DevOps, Cloud, and Backend Engineering roles**.

## Architecture Diagram

![alt text](Screenshots/architecture.png)

---

## 🧱 High-Level Architecture

The application follows a **microservices architecture**, where each service owns its own database and communicates over Docker’s internal network.

### Frontend
- **ecommerce-ui** (React)
- Exposed on port **4000**
- Communicates with backend services using internal Docker DNS

### Backend Services

| Service Name | Responsibility | Port |
|-------------|---------------|------|
| profile-management | User signup & authentication | 3003 |
| product-catalog | Product listing & details | 3001 |
| product-inventory | Inventory & stock management | 3002 |
| order-management | Order processing | 9090 |
| shipping-and-handling | Shipping workflow | 8080 |
| contact-support-team | Customer support | 8000 |

---

## 🗄 Database Architecture (Polyglot Persistence)

Each microservice owns a dedicated database, following **database-per-service** best practices.

| Service | Database Name | Database Type |
|-------|--------------|---------------|
| profile-management | profile_management | MySQL 8 |
| product-inventory | product_inventory | PostgreSQL |
| product-catalog | product_catalog | MongoDB |
| order-management | order_management | MongoDB |
| shipping-and-handling | shipping DB | MongoDB |
| contact-support-team | contact_support | MongoDB |

---

## 📦 Docker Volumes

Persistent storage is handled using Docker volumes to ensure data durability.

```
mongodb_product_catalog_data
mongodb_contact_support_data
mongodb_shipping_data
mongodb_order_management_data
mysql_profile_management_data
postgres_product_inventory_data
```

Volumes prevent data loss during container restarts or upgrades.

---

## 🔐 Security Model

- Internal service-to-service communication using Docker’s default bridge network
- Databases are **not publicly exposed**
- Only application ports are exposed on the EC2 instance
- Credentials are injected using environment variables
- No credentials are hardcoded inside images

This model closely resembles **VPC-style internal communication** used in production environments.

---

## ☁ AWS Deployment Details

| Component | Configuration |
|---------|---------------|
| Instance Type | c7i-flex.large |
| Operating System | Ubuntu 22.04 LTS |
| Root Volume | 100 GB |
| Container Runtime | Docker |
| Orchestration | Docker Compose |

---

## 🚀 Deployment Steps (AWS EC2)

### Install Docker

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu
```
Logout and login again to apply group changes.

### Install Docker Compose
```
sudo apt install -y docker-compose
```
### Clone the Repository

```
git clone https://github.com/vanuhanda/ecommerce-microservices-docker-compose.git
cd <commerce-microservices-docker-compose>
```
### Start the Application
```
docker compose up -d
```
Docker Compose will automatically:

Pull images from Docker Hub

Create networks and volumes

Start services in the correct dependency order

### Verify Running Containers
```
docker ps
```
### Application Access
Replace <EC2_PUBLIC_IP:4000> with your instance’s public IP.
| Service                | URL                           |
| ---------------------- | ----------------------------- |
| Web UI                 | `http://<EC2_PUBLIC_IP>:4000` |
| Profile Management API | `http://<EC2_PUBLIC_IP>:3003` |
| Product Catalog API    | `http://<EC2_PUBLIC_IP>:3001` |
| Inventory API          | `http://<EC2_PUBLIC_IP>:3002` |
| Order Management API   | `http://<EC2_PUBLIC_IP>:9090` |
| Shipping API           | `http://<EC2_PUBLIC_IP>:8080` |

The remaining URL will only work if the ports are open in AWS EC2 security group. 

## 🧪 Key Concepts Demonstrated

- **Docker Compose orchestration**
- **Microservices networking via Docker DNS**
- **Stateful containers with persistent volumes**
- **Multi-database architecture**
- **Cloud deployment on AWS EC2**
- **End-to-end service dependency management**
