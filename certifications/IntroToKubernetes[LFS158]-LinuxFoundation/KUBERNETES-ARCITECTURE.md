---

# 🏗️ Kubernetes Architecture

At a high level, **:contentReference[oaicite:0]{index=0}** is a cluster of compute systems organized by roles:

- One or more **Control Plane Nodes**
- One or more **Worker Nodes** (optional for learning, recommended for production)

![Kubernetes Architecture](images/kubernetesArcitecture.png)

---

# 🧠 Control Plane Node Overview

The **Control Plane** is the brain of the Kubernetes cluster.

It:

- Manages cluster state
- Makes scheduling decisions
- Maintains desired state
- Responds to user/API requests

Users interact with the cluster via:

- CLI (kubectl)
- Web UI Dashboard
- REST API

⚠️ Keeping the Control Plane running is critical.  
If it fails → cluster management stops → possible downtime.

---

## 🔁 High Availability (HA)

To prevent downtime:

- Multiple control plane nodes can be configured
- Only one is actively managing
- Others stay synchronized
- If active node fails → another takes over

This ensures **fault tolerance**.

---

# 🗄️ Cluster State Storage

Kubernetes stores all cluster state inside a distributed key-value store:

**:contentReference[oaicite:1]{index=1}**

Important:
- Stores only cluster state
- Does NOT store application data
- Only API Server communicates with etcd

---

## 🏗️ etcd Topologies

### 1️⃣ Stacked Topology
- etcd runs on the same control plane node
- Shares resources
- Easier setup (default in kubeadm)

![Stacked etcd Topology](images/stackedetcdtopology.png)

---

### 2️⃣ External Topology
- etcd runs on separate dedicated hosts
- Better isolation
- Requires separate HA configuration
- Higher operational cost

![External etcd Topology](images/externaletcdtopology.png)

---

## 🗳️ etcd and Raft Consensus

etcd uses the **Raft Consensus Algorithm**:

- One leader
- Multiple followers
- Leader elected automatically
- Handles failures gracefully

Leader does NOT outrank others permanently —  
if it fails → new leader elected.

![Raft Leader Election](images/leader.png)

---

# ⚙️ Control Plane Components

Each control plane node runs:

- API Server
- Scheduler
- Controller Managers
- etcd
- Container Runtime
- kubelet
- kube-proxy

---

## 🌐 API Server

The **kube-apiserver**:

- Central communication hub
- Accepts REST requests
- Validates requests
- Reads/writes cluster state to etcd
- Only component that talks to etcd

It can scale horizontally and supports custom API extensions.

---

## 🧮 Scheduler

The **kube-scheduler**:

- Assigns Pods to nodes
- Evaluates:
  - CPU / Memory availability
  - Labels
  - Affinity / Anti-affinity
  - Taints & Tolerations
  - QoS requirements

Process:
1. Filter candidate nodes
2. Score them
3. Select best node
4. Inform API Server

Custom schedulers are supported.

---

## 🔄 Controller Managers

Controllers ensure:

> Desired state = Current state

Two main controller managers:

### 1️⃣ kube-controller-manager
Handles:
- Node failures
- Replica management
- Endpoints
- Service accounts
- API tokens

### 2️⃣ cloud-controller-manager
Handles:
- Cloud load balancers
- Cloud storage volumes
- Node lifecycle in cloud environments

---

# 👷 Worker Node Overview

Worker nodes run application workloads.

Applications run inside:

> **Pods** (smallest scheduling unit)

Pods:
- Contain one or more containers
- Share network namespace
- Share storage volumes
- Scheduled on worker nodes

In multi-node clusters:
- Traffic is handled directly by worker nodes
- Not routed through control plane

---

# 🔧 Worker Node Components

Worker nodes run:

- Container Runtime
- kubelet
- CRI Shims
- kube-proxy
- Add-ons

---

## 📦 Container Runtime

Kubernetes does NOT run containers directly.

It relies on container runtimes like:

- CRI-O
- containerd
- Docker Engine
- Mirantis Container Runtime

Each node must have a runtime.

---

## 🤖 kubelet

The **kubelet**:

- Runs on every node
- Receives Pod specs from API Server
- Talks to container runtime
- Ensures containers are running
- Reports status back

---

## 🔌 CRI (Container Runtime Interface)

kubelet communicates with runtimes via CRI.

It uses:

- gRPC
- Protocol buffers
- CRI shims

![Container Runtime Interface](images/containerruntimeinterface.png)

---

### Examples of CRI Shims

- cri-containerd
- CRI-O
- cri-dockerd (replacement for dockershim)

---

## 🌐 kube-proxy

kube-proxy:

- Runs on every node
- Manages networking rules
- Uses iptables
- Implements Service routing
- Handles TCP, UDP, SCTP

It forwards traffic to correct Pods.

---

# 🔌 Add-ons

Kubernetes core does not include everything by default.

Common add-ons:

- DNS
- Dashboard
- Monitoring
- Logging
- Device Plugins (GPU, FPGA, NIC)

---

# 🌍 Networking Challenges in Kubernetes

Kubernetes networking must support:

1. Container-to-Container (inside Pod)
2. Pod-to-Pod (same node)
3. Pod-to-Pod (across nodes)
4. Service-to-Pod
5. External-to-Service

---

## 📡 Container-to-Container (Inside Pod)

- Containers share same network namespace
- Special "Pause" container creates namespace
- Containers communicate via localhost

---

## 🌐 Pod-to-Pod Across Nodes

Key principle:

> IP-per-Pod

Each Pod:
- Gets unique IP
- No NAT required
- Communicates like VMs

Networking handled by CNI plugins:

Examples:
- Flannel
- Calico
- Cilium
- Weave

![Pod to Pod Networking](images/podtopod.png)

---

## 🌎 External-to-Pod Communication

External traffic enters cluster via:

- Services
- kube-proxy
- iptables rules

Service:
- Provides virtual IP
- Provides stable DNS name
- Load balances across Pods

---

# 📌 Final Summary

Kubernetes architecture is divided into:

- 🧠 Control Plane (brain)
- 👷 Worker Nodes (workload runners)

It is:

- Distributed
- Highly available
- Extensible
- Network-driven
- Self-healing

Understanding architecture is the foundation for:

- CKA certification
- DevOps roles
- Production cluster management
