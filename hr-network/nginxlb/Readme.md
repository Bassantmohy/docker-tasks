# 🌐 Task 2 – Multi-Homed NGINX Load Balancer

This task demonstrates a **multi-homed container architecture** where an **NGINX Load Balancer** connects to **two isolated custom bridge networks**.  
It separates **frontend (client)** traffic from **backend (service)** communication while letting the load balancer act as a secure routing bridge.

---

## ⚙️ Requirements

| Component | Details |
|------------|----------|
| **Network 1 (Frontend)** | Name: `frontend-net`  •  Subnet: `10.1.1.0/24` |
| **Network 2 (Backend)** | Name: `backend-net`   •  Subnet: `10.1.2.0/24` |
| **Containers** | `nginx-lb` → connected to both networks (multi-homed)<br>`client-tester` → frontend only<br>`backend-db` → backend only |

---

## 🧱 Execution Steps

### 1️⃣ Create the Custom Networks
```bash
docker network create --subnet 10.1.1.0/24 frontend-net
docker network create --subnet 10.1.2.0/24 backend-net --internal
```
2.**inspect loadbalancer**
```bash
docker inspect nginx-lb
```
3.**ckeck client-server (frontend net) can't connect with backend-db (backend net)**
```bash
ping backend-db
```

---

## 🌐 **2️⃣ NGINX Load Balancer (Multi-Homed) Task Mermaid Diagram**

```markdown
## 🖼️ Network Diagram

```mermaid
graph TB
    subgraph Frontend-Network ["frontend-net (10.1.1.0/24)"]
        C[client-tester 💻]:::client
        LB1[nginx-lb 🌐]:::lb
    end

    subgraph Backend-Network ["backend-net (10.1.2.0/24)"]
        LB2[nginx-lb 🌐]:::lb
        D[backend-db 🗄️]:::backend
    end

    C --> LB1
    LB2 --> D

    classDef lb fill:#f6b93b,stroke:#e58e26,stroke-width:2px,color:#000;
    classDef client fill:#82ccdd,stroke:#3c6382,stroke-width:2px,color:#000;
    classDef backend fill:#b8e994,stroke:#079992,stroke-width:2px,color:#000;

