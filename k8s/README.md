# Kubernetes

## What is K8s

Kubernetes (K8s) is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. The name "K8s" comes from the 8 letters between "K" and "s" in "Kubernetes".

Kubernetes was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF). It provides a platform for managing containerized workloads and services, facilitating both declarative configuration and automation.

## What problem it solves

Kubernetes addresses several critical challenges in modern application deployment:

### 1. **Container Orchestration Complexity**

- Manages hundreds or thousands of containers across multiple hosts
- Handles container lifecycle (start, stop, restart, scale)
- Ensures high availability and fault tolerance

### 2. **Service Discovery and Load Balancing**

- Automatically discovers services and routes traffic
- Provides built-in load balancing across containers
- Handles internal and external service communication

### 3. **Storage Orchestration**

- Manages persistent storage for stateful applications
- Supports various storage backends (local, cloud, network)
- Handles volume mounting and data persistence

### 4. **Automated Rollouts and Rollbacks**

- Enables zero-downtime deployments
- Supports blue-green and canary deployments
- Provides automatic rollback capabilities

### 5. **Self-Healing**

- Automatically replaces failed containers
- Restarts containers that don't respond to health checks
- Kills containers that don't meet health requirements

### 6. **Secret and Configuration Management**

- Securely stores and manages sensitive information
- Handles configuration updates without rebuilding containers
- Supports environment-specific configurations

## Why we use K8s

### **Scalability**

- Horizontal scaling: Add more containers to handle increased load
- Vertical scaling: Increase resource allocation to existing containers
- Auto-scaling based on CPU/memory usage or custom metrics

### **Portability**

- Run applications consistently across different environments
- Cloud-agnostic: Works on AWS, GCP, Azure, on-premises
- Hybrid and multi-cloud deployments

### **Resource Efficiency**

- Better resource utilization through containerization
- Efficient scheduling and resource allocation
- Cost optimization through better resource management

### **Developer Productivity**

- Simplified deployment and operations
- Consistent development and production environments
- Faster time-to-market for applications

### **Operational Excellence**

- Reduced operational overhead
- Automated monitoring and logging
- Built-in security features and compliance

## Main components of K8s

### **Control Plane Components**

#### 1. **kube-apiserver**

- The front-end of the Kubernetes control plane
- Exposes the Kubernetes API
- Handles all administrative operations

#### 2. **etcd**

- Distributed key-value store
- Stores all cluster data
- Source of truth for cluster state

#### 3. **kube-scheduler**

- Watches for newly created Pods
- Assigns Pods to nodes based on resource requirements
- Considers hardware/software constraints

#### 4. **kube-controller-manager**

- Runs controller processes
- Manages node, replication, endpoints, service accounts, and tokens
- Ensures desired state matches actual state

### **Node Components**

#### 1. **kubelet**

- Primary node agent
- Manages Pod lifecycle on the node
- Ensures containers are running in a Pod

#### 2. **kube-proxy**

- Network proxy running on each node
- Maintains network rules
- Enables communication to Pods from network sessions

#### 3. **Container Runtime**

- Software responsible for running containers
- Examples: containerd, CRI-O, Docker

### **Kubernetes Objects**

#### 1. **Pods**

- Smallest deployable units in Kubernetes
- Contains one or more containers
- Shares network and storage resources

#### 2. **Services**

- Abstract way to expose applications
- Provides load balancing and service discovery
- Types: ClusterIP, NodePort, LoadBalancer, ExternalName

#### 3. **Deployments**

- Manages ReplicaSets and Pods
- Provides declarative updates
- Supports rolling updates and rollbacks

#### 4. **ConfigMaps and Secrets**

- Stores configuration data and sensitive information
- Injected into containers as environment variables or files

#### 5. **Volumes**

- Provides persistent storage for Pods
- Supports various storage backends
- Types: emptyDir, hostPath, persistentVolumeClaim

## How it works

### **1. Cluster Architecture**

```
┌─────────────────────────────────────────────────────────────┐
│                    Control Plane                            │
├─────────────────────────────────────────────────────────────┤
│  kube-apiserver │ etcd │ kube-scheduler │ kube-controller   │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      Worker Nodes                           │
├─────────────────────────────────────────────────────────────┤
│  kubelet │ kube-proxy │ Container Runtime │ Pods           │
└─────────────────────────────────────────────────────────────┘
```

### **2. Pod Lifecycle**

1. **Pending**: Pod is accepted by the system, but containers are not yet running
2. **Running**: Pod is bound to a node, and all containers are created
3. **Succeeded**: All containers terminated successfully
4. **Failed**: At least one container terminated in failure
5. **Unknown**: Pod state cannot be determined

### **3. Service Discovery**

- **DNS-based**: Services get DNS names automatically
- **Environment variables**: Pods receive service information as env vars
- **Load balancing**: Traffic distributed across Pod endpoints

### **4. Scheduling Process**

1. Pod creation request sent to API server
2. Scheduler watches for unscheduled Pods
3. Scheduler evaluates nodes based on:
   - Resource requirements
   - Node affinity/anti-affinity
   - Taints and tolerations
   - Hardware/software constraints
4. Pod assigned to best-fit node
5. Kubelet on target node creates and runs containers

### **5. Self-Healing Mechanisms**

- **Health Checks**: Liveness and readiness probes
- **Replication**: ReplicaSets ensure desired number of Pods
- **Node Failure**: Pods rescheduled to healthy nodes
- **Container Failure**: Containers restarted automatically

### **6. Networking Model**

- **Pod Network**: Each Pod gets unique IP address
- **Service Network**: Services have cluster IPs
- **Node Network**: Physical/virtual network connectivity
- **CNI Plugins**: Network implementation (Calico, Flannel, etc.)

### **7. Storage Management**

- **Persistent Volumes**: Storage resources in the cluster
- **Persistent Volume Claims**: Storage requests from users
- **Storage Classes**: Different types of storage with different characteristics
- **Dynamic Provisioning**: Automatic volume creation

This comprehensive overview covers the fundamental aspects of Kubernetes, making it easier to understand its role in modern containerized application deployment and management.
