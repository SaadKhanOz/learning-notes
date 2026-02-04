##Virtual Machines (VMs)

## Why Virtual Machines Exist

DevOps focuses on **efficient resource utilization**.

### Real-World Analogy
- You own 1 acre of land
- You only use half
- Rent the other half

➡ Better utilization = virtualization

---

## Traditional Server Problem

- One application per physical server
- Example:
  - Server: 100 GB RAM, 100 CPU cores
  - App uses only 4 GB RAM, 4 CPU cores

➡ 90% resources wasted

---

## Virtualization

Virtualization allows **logical separation** of a physical server into multiple virtual machines.

### Hypervisor
- Software that creates and manages VMs
- Installed on physical servers

Examples:
- VMware
- Xen
- KVM

---

## Virtual Machine (VM)

- A virtual environment acting as a computer
- Has its own:
  - CPU
  - Memory
  - OS
- Isolated from other VMs

<p align="center">
  <img src="images/VM.png" width="600">
</p>


---

## Cloud Example (AWS EC2)

- AWS owns physical data centers
- Hypervisors run on physical servers
- EC2 = Virtual Machine

### VM Creation Flow
1. User requests EC2 from AWS Console / API
2. Request goes to regional data center
3. Hypervisor creates VM
4. AWS returns IP and access details

---

## Automation in VM Creation

Manual creation ❌ (inefficient)
Automation ✅ (DevOps way)

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

