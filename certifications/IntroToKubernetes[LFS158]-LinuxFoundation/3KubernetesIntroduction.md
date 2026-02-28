---

# 🚢 What Is Kubernetes?

According to the official Kubernetes website:

> "Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications."

The word **Kubernetes** comes from the Greek word **κυβερνήτης**, meaning *helmsman* or *ship pilot*.  
With this analogy, Kubernetes acts as the **pilot of a ship of containers**.

Kubernetes is commonly abbreviated as **k8s** (pronounced *Kate's*), because there are 8 letters between **k** and **s**.

Kubernetes is:

- Open-source  
- Written in **Go**
- Licensed under **Apache License 2.0**

It was originally started by Google and officially released as v1.0 in July 2015. Google later donated it to the **Cloud Native Computing Foundation (CNCF)**, a sub-foundation of the Linux Foundation.

New versions are released in 4-month cycles.

---

# 🏗️ From Borg to Kubernetes

Kubernetes was heavily inspired by Google’s internal system:

**:contentReference[oaicite:0]{index=0}**

According to Google’s 2015 Borg paper:

> "Google's Borg system is a cluster manager that runs hundreds of thousands of jobs across clusters with tens of thousands of machines."

For more than a decade, Borg powered Google's global infrastructure including services like:

- Gmail  
- Drive  
- Maps  
- Docs  

Several original Kubernetes developers previously worked on Borg. Their real-world production experience shaped Kubernetes' design.

### Kubernetes Concepts Inspired by Borg:

- API Servers  
- Pods  
- IP-per-Pod model  
- Services  
- Labels  

We will explore these components in detail later in the course.

---

# ⚙️ Kubernetes Features

Kubernetes provides a rich set of production-grade features.

---

## 🔹 Core Features

### 1️⃣ Automatic Bin Packing
Kubernetes automatically schedules containers based on:
- CPU requirements  
- Memory requirements  
- Constraints  

It maximizes resource utilization without sacrificing availability.

---

### 2️⃣ Designed for Extensibility
Kubernetes clusters can be extended with custom features without modifying the core source code.

---

### 3️⃣ Self-Healing
Kubernetes automatically:

- Replaces failed containers  
- Restarts unresponsive containers  
- Reschedules workloads from failed nodes  
- Prevents traffic from reaching unhealthy containers  

---

### 4️⃣ Horizontal Scaling
Applications can scale:

- Manually  
- Automatically (based on CPU or custom metrics)

---

### 5️⃣ Service Discovery & Load Balancing
- Each container gets its own IP address.
- Kubernetes assigns a single DNS name to a group of containers.
- Requests are load-balanced across containers.

---

## 🔹 Additional Features

### 6️⃣ Automated Rollouts & Rollbacks
- Zero-downtime deployments  
- Health monitoring during updates  
- Easy rollback if something fails  

---

### 7️⃣ Secret & Configuration Management
Kubernetes separates sensitive data from container images.

Examples:
- Passwords  
- API keys  
- Tokens  

This prevents exposure of secrets in repositories like GitHub.

---

### 8️⃣ Storage Orchestration
Kubernetes automatically mounts storage from:

- Local storage  
- Cloud providers  
- Distributed storage systems  
- Network storage  

---

### 9️⃣ Batch Execution
Supports:

- Batch jobs  
- Long-running tasks  
- Automatic retry of failed jobs  

---

### 🔟 IPv4 / IPv6 Dual Stack
Kubernetes supports both IPv4 and IPv6 networking.

---

# 🧩 Platform Capabilities

Kubernetes supports Platform-as-a-Service (PaaS) capabilities like:

- Application deployment  
- Scaling  
- Load balancing  

It also allows integration with third-party tools for:

- Monitoring  
- Logging  
- Alerting  

Features such as:

- RBAC (stable since v1.8)
- CronJobs (stable since v1.21)

were initially introduced as alpha/beta features before becoming stable.

---

# 🌍 Why Use Kubernetes?

One of Kubernetes’ strongest advantages is **portability**.

It can run on:

- Local machines  
- Virtual Machines  
- Bare metal servers  
- Public cloud  
- Private cloud  
- Hybrid cloud  
- Multi-cloud environments  

---

## 🔌 Extensibility & Modularity

Kubernetes architecture is:

- Modular  
- Pluggable  
- Microservices-based  

You can extend Kubernetes using:

- Custom Resources (CRDs)  
- Operators  
- Custom APIs  
- Scheduling rules  
- Plugins  

Not only does Kubernetes orchestrate microservices —  
it is itself designed using microservices principles.

---

# 📌 Summary

Kubernetes is:

- A powerful container orchestration platform  
- Inspired by Google’s production-proven Borg system  
- Highly scalable, portable, and extensible  
- Industry-standard in modern DevOps and Cloud Engineering  

It has become the backbone of cloud-native infrastructure worldwide.
