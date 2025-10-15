# 🐳 Docker Networking Tasks

This repository contains two Docker networking exercises demonstrating **custom bridge networks**, **multi-homed containers**, and **internal service discovery** using Docker’s built-in DNS resolution.

---

## 📘 Task 1: HR Application Network

### 🎯 Objective
Establish a **dedicated and isolated Custom Bridge Network** for an HR application stack running on a single Docker host.  
The goal is to enable **service discovery via container names** and avoid **IP conflicts** with the corporate VPN network using the `172.17.0.0/16` range.

---

### ⚙️ Requirements
| Component | Value |
|------------|--------|
| Network Type | Custom Bridge |
| Network Name | `hr-app-net` |
| Subnet | `192.168.20.0/24` |
| Gateway | `192.168.20.1` |
| Server Container | `nginx-server` (NGINX Web Frontend) |
| Client Container | `alpine-tester` (for diagnostics and connectivity testing) |

---

### 🧩 Steps

1. **Create the Custom Bridge Network**
   ```bash
   docker network create --driver bridge \
   --subnet 192.168.20.0/24 \
   --gateway 192.168.20.1 hr-app-net
   ```

![Network Created](https://github.com/Bassantmohy/docker-tasks/blob/main/hr-network/HR-netCreate.png)


2.**Inspect the network**
```bash
docker inspect alpine-tester
docker inspect nginx-server
```
![Alpine Inspected]([./alpine-tester.png)](https://github.com/Bassantmohy/docker-tasks/blob/main/hr-network/alpine-tester.png)

![Nginx Inspected]([./alpine-tester.png)](https://github.com/Bassantmohy/docker-tasks/blob/main/hr-network/nginx-server-inspect.png)

3.**Check the network inside alpine-tester**
```bash
ping nginx-server
```
![Network Checked]([./alpine-tester.png)](https://github.com/Bassantmohy/docker-tasks/blob/main/hr-network/ping_alpine-nginx-DNS.png)


## 🖼️ Network Diagram

```mermaid
graph LR
    subgraph HR-App-Network ["Custom Bridge: hr-app-net (192.168.20.0/24)"]
        A[nginx-server 🧩]:::server
        B[alpine-tester 🧪]:::client
    end

    A <--> B

    classDef server fill:#f8c291,stroke:#b33939,stroke-width:2px,color:#000;
    classDef client fill:#82ccdd,stroke:#3c6382,stroke-width:2px,color:#000;







