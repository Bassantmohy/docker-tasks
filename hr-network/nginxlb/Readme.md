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
graph TD
```mermaid
    subgraph Frontend Network (10.1.1.0/24)
        C[client-tester]
        L[nginx-lb]
    end

    subgraph Backend Network (10.1.2.0/24)
        L2[nginx-lb]
        B[backend-db]
    end

    C --> L
    L2 --> B
