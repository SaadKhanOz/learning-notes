# Absolute Prerequisites for Learning DevOps

This document explains **how software requirements flow inside a company**, the **roles involved**, and **where DevOps fits in the SDLC**. It also introduces **Virtual Machines and virtualization**, which are foundational DevOps concepts.

---

## 1. Roles in a Company (Requirement Flow)

Let’s take an example of **Amazon Fresh** (grocery delivery).

### Business Context
- Customers want groceries delivered quickly
- Example requirements:
  - Deliver groceries within **15 minutes**
  - Integrate a **payment gateway (Stripe)**

---

### Key Roles and Responsibilities

#### Customer
- The most important stakeholder
- Provides business needs and expectations

#### Business Analyst (BA)
- Interacts directly with customers
- Gathers requirements
- Prepares **BRD (Business Requirement Document)**

```
Customer ↔ BA → BRD
```

#### Product Manager (PM)
- Owns **product vision and roadmap**
- Prioritizes requirements (e.g., Jan, Feb releases)
- Works closely with BA

#### Product Owner (PO)
- Takes prioritized requirements from PM
- Breaks them into **Epics and Features**
  - UI
  - Backend
  - Database

#### Software Architect / Solution Architect (SA)
- Highly technical role
- Creates:
  - **HLD (High-Level Design)**
  - **LLD (Low-Level Design)**
- Validates feasibility and technical skills
- Provides feedback to PM and PO

> BA, PM, and PO are **less technical** compared to SA.

---

### Execution Roles (Scrum Team)

#### Developers
- Convert epics into user stories
- Write application code

#### DevOps Engineers
- Provide infrastructure and automation
- Kubernetes clusters
- Dockerfiles
- CI/CD pipelines
- Git workflows
- Infrastructure provisioning

#### QA / QE (Quality Engineers)
- Test features manually and via automation

#### DBA (Database Administrator)
- Manages database performance, backups, tuning
- DB provisioning may be done by DevOps

#### SRE (Site Reliability Engineer)
- Ensures reliability, availability, scalability
- Monitoring dashboards
- Alerts and incident response

#### Technical Writers
- Document features, APIs, and workflows

---

### Simplified Flow

```
Customer
  ↓
BA (BRD)
  ↓
PM (Prioritization)
  ↓
PO (Epics & Features)
  ↓
Software Architect (HLD & LLD)
  ↓
---------------------------------------
| Developers | DevOps | QA | DBA |
---------------------------------------
  ↓
SRE (Monitoring & Reliability)
```

> BA, PM, PO, and SA are **shared across teams** and are considered *non-delivery roles*.

---

## 2. SDLC (Software Development Life Cycle)

1. **Planning** – Requirement gathering
2. **Analysis** – Feasibility study
3. **Design** – HLD & LLD (Architect)
4. **Implementation** – Devs, DevOps, QA
5. **Testing** – QA
6. **Maintenance** – SRE

<p align="center">
  <img src="images/SDLC-cycle.jpg" width="600">
</p>

---

### Important Question

**Do DevOps engineers only take requirements from developers?**

❌ No.

### What DevOps Actually Does
- Identify bottlenecks in SDLC
- Automate repetitive processes
- Increase delivery speed and reliability

Examples:
- Integrate test scripts into CI/CD pipelines
- Run automated tests on every code change
- Integrate security scanning
- Automate infrastructure provisioning

DevOps = **Automation + Efficiency + Collaboration**

---


AWS provides APIs to automate everything.

### Ways to Create EC2 Instances
1. AWS Console (manual)
2. AWS CLI
3. AWS SDK / APIs
4. AWS CloudFormation (CFT)
5. Terraform
6. AWS CDK

---

### Automation Benefits
- No manual intervention
- Fewer errors
- Scalable
- Repeatable

Even creating **1 VM via script** follows DevOps principles.

---

## Interview Question

**How do you create 10 VMs at once?**

### Answer
- VM = Infrastructure
- EC2 = Infrastructure
- Use IaC tools:
  - Terraform
  - CloudFormation
  - AWS CLI / SDK

Choice depends on organization standards.

---

## Key Takeaway

DevOps is not a role limited to infrastructure.
It is a **culture of automation, efficiency, and reliability**.
