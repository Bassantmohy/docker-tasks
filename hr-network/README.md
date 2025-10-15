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

![Network Created](https://github.com/Bassantmohy/docker-tasks/blob/main/hr-network/HR-netCreate.png)

2.**Inspect the network**
```bash
docker inspect alpine-tester
docker inspect nginx-server

![Alpine Inspected](./alpine-tester.png)


