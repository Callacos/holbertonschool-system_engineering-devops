# 1. Distributed web infrastructure

## Infrastructure Overview

This web infrastructure is composed of:
- **1 Load Balancer** (HAProxy)
- **2 Servers**, each containing:
  - 1 Nginx Web Server
  - 1 Application Server
  - 1 Set of Application Files (Codebase)
  - 1 MySQL Database
![Simple Web Stack](task1)
---

##  Element Explanations

### Load Balancer (HAProxy)
**Why?**  
To distribute incoming traffic between multiple servers to ensure high availability, better performance, and fault tolerance.

### Web Servers (Nginx)
**Why?**  
To serve static content (HTML, CSS, JS) and forward dynamic requests to the application server.

### Application Servers
**Why?**  
To process application logic and handle dynamic user requests.

### Application Files
**Why?**  
Each server contains a full copy of the application to ensure redundancy and scalability.

### MySQL Databases
**Why?**  
Each server includes a database to store and retrieve persistent data for the application.

---

##  Load Balancer Algorithm

### Algorithm: **Round Robin**
**How it works:**  
Each new incoming request is forwarded to the next server in the list in a rotating fashion. This ensures an even distribution of traffic under normal load conditions.

---

## Active-Active vs Active-Passive

### Current Setup: **Active-Active**
**Explanation:**  
Both servers are running simultaneously and receiving traffic from the load balancer. This maximizes resource usage and performance.

**Difference:**
- **Active-Active:** All nodes handle traffic at the same time.
- **Active-Passive:** One node handles all traffic, others are on standby in case of failure.

---

##  Primary-Replica Cluster (Database)

### How it works:
- The **Primary** node handles all write operations.
- The **Replica(s)** receive updates from the Primary and handle **read-only** queries.

**Benefits:**  
Improved read performance and data redundancy.

### Application Point of View:
- Writes are directed to the **Primary**
- Reads can be distributed across **Replicas**

---

##  Infrastructure Issues

### 1. **SPOF (Single Point of Failure)**
- If the **load balancer** fails, the whole system becomes unreachable.
- If each server has its own database with no replication, data inconsistency or loss may occur.

### 2. **Security Issues**
- **No firewall:** All services are directly exposed to the internet.
- **No HTTPS:** Traffic is not encrypted, allowing potential man-in-the-middle attacks.

### 3. **No Monitoring**
- There’s no way to detect downtime, performance issues, or attacks in real time.
- Lack of alerts can delay incident response and troubleshooting.

---


