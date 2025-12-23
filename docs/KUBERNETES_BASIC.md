# KUBERNETES BASIC

Description: All things you need to know as a beginner.
Reference document: https://kubernetes.io/docs/home/

## Table of Contents
- [What is Kubernetes?](#kubernetes)
- [Core Concepts](#core-concepts)
  - [Cluster](#cluster)
  - [Node](#node)
  - [Pod](#pod)
  - [Deployment](#deployment)
  - [Service](#service)
  - [ConfigMap and Secret](#configmap-and-secret)
  - [Namespace](#namespace)
  - [PersistentVolume and PersistentVolumeClaim](#persistentvolume-and-persistentvolumeclaim)
- [Kubernetes Architecture](#kubernetes-architecture)
  - [Control Plane Components](#control-plane-components)
  - [Node Components](#node-components)
  - [Addons](#addons)
- [Basic Commands](#basic-commands)
- [Best Practices](#best-practices)

## Kubernetes
- **What**: An open-source container orchestration platform for automating deployment, scaling, and management of containerized applications.
- **Where**: Runs on a cluster of machines (physical or virtual), on-premises, or in the cloud.
- **When**: Use when you need to manage containerized applications across multiple hosts, scale applications, or ensure high availability.
- **Why**: Provides automated deployment, scaling, and operations of application containers across clusters of hosts.
- **How**: Define desired state in YAML/JSON manifests, and Kubernetes works to maintain that state.

## Core Concepts

### Cluster
- **What**: A set of node machines for running containerized applications managed by Kubernetes.
- **Where**: Comprises at least one control plane and multiple worker nodes.
- **When**: Created when setting up a Kubernetes environment to run containerized applications.
- **Why**: Provides the infrastructure to run and manage containerized applications at scale.

#### CLI: Cluster management
```
kubectl cluster-info
kubectl get nodes
kubectl describe node <node-name>
```

### Node
- **What**: A worker machine in Kubernetes, which may be a VM or physical machine.
- **Where**: Part of the Kubernetes cluster, can be on-premises or in the cloud.
- **When**: Added to scale the cluster's compute resources.
- **Why**: To provide the compute resources needed to run containerized applications.

#### CLI: Node operations
```
kubectl get nodes
kubectl describe node <node-name>
kubectl drain <node-name> --ignore-daemonsets
kubectl uncordon <node-name>
```

### Pod
- **What**: The smallest deployable unit in Kubernetes, representing a single instance of a running process.
- **Where**: Runs on nodes in the cluster.
- **When**: Created when deploying containerized applications.
- **Why**: To run one or more containers that share storage and network resources.

#### CLI: Pod management
```
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- /bin/sh
kubectl delete pod <pod-name>
```

### Deployment
- **What**: Manages a set of replica Pods and enables declarative updates for Pods.
- **Where**: Deployed to the Kubernetes cluster.
- **When**: When you need to deploy and update applications.
- **Why**: To ensure that a specified number of pod replicas are running at any given time.

#### CLI: Deployment operations
```
kubectl create deployment <name> --image=<image>
kubectl get deployments
kubectl describe deployment <deployment-name>
kubectl scale deployment <deployment-name> --replicas=3
kubectl rollout status deployment/<deployment-name>
```

### Service
- **What**: An abstraction that defines a logical set of Pods and a policy to access them.
- **Where**: Runs across the cluster.
- **When**: When you need to expose your application running on a set of Pods as a network service.
- **Why**: To enable network access to a set of Pods.

#### CLI: Service management
```
kubectl expose deployment <deployment-name> --port=80 --target-port=80 --type=LoadBalancer
kubectl get services
kubectl describe service <service-name>
```

### ConfigMap and Secret
- **What**: ConfigMap stores non-confidential data in key-value pairs, while Secret is for sensitive data.
- **Where**: Stored in the Kubernetes API and mounted into Pods as files or environment variables.
- **When**: When you need to separate configuration from application code.
- **Why**: To make applications portable and to manage sensitive data securely.

#### CLI: ConfigMap and Secret operations
```
# ConfigMap
kubectl create configmap <config-name> --from-literal=key=value
kubectl get configmaps
kubectl describe configmap <config-name>

# Secret
echo -n 'admin' | base64
kubectl create secret generic <secret-name> --from-literal=username=admin --from-literal=password=secret
kubectl get secrets
```

### Namespace
- **What**: A way to divide cluster resources between multiple users.
- **Where**: Within a Kubernetes cluster.
- **When**: When you need to organize resources and divide cluster resources between multiple users.
- **Why**: To provide a scope for names and to divide cluster resources between multiple users.

#### CLI: Namespace operations
```
kubectl create namespace <namespace-name>
kubectl get namespaces
kubectl config set-context --current --namespace=<namespace-name>
```

### PersistentVolume and PersistentVolumeClaim
- **What**: Storage resources in the cluster and a request for storage by a user.
- **Where**: In the cluster's storage infrastructure.
- **When**: When you need persistent storage for your applications.
- **Why**: To manage storage in a way that's abstracted from the underlying storage infrastructure.

#### CLI: PV and PVC operations
```
# Create a PersistentVolume
kubectl apply -f pv.yaml

# Create a PersistentVolumeClaim
kubectl apply -f pvc.yaml

# List PVs and PVCs
kubectl get pv
kubectl get pvc
```

## Kubernetes Architecture

### Control Plane Components
- **kube-apiserver**: The API server that exposes the Kubernetes API
- **etcd**: Consistent and highly-available key value store used as Kubernetes' backing store
- **kube-scheduler**: Watches for newly created Pods with no assigned node, and selects a node for them to run on
- **kube-controller-manager**: Runs controller processes
- **cloud-controller-manager**: Embeds cloud-specific control logic

### Node Components
- **kubelet**: An agent that runs on each node in the cluster
- **kube-proxy**: Maintains network rules on nodes
- **Container runtime**: The software responsible for running containers

### Addons
- **DNS**: Cluster DNS is a DNS server that provides DNS records for Kubernetes services
- **Dashboard**: A general purpose, web-based UI for Kubernetes clusters
- **Container Resource Monitoring**: Records metrics about containers in a central database

## Basic Commands

### Getting started
```
kubectl version
kubectl cluster-info
kubectl get all
```

### Common operations
```
# Apply a configuration to a resource
kubectl apply -f <filename>

# Get resources
kubectl get <resource-type>
kubectl get <resource-type> -o wide
kubectl get <resource-type> -o yaml

# Describe resources
kubectl describe <resource-type> <resource-name>

# Delete resources
kubectl delete <resource-type> <resource-name>
kubectl delete -f <filename>
```

### Debugging
```
# View pod logs
kubectl logs <pod-name>

# Execute a command in a container
kubectl exec -it <pod-name> -- /bin/sh

# Port forwarding
kubectl port-forward <pod-name> <local-port>:<pod-port>
```

## Best Practices
1. Use declarative configuration (YAML/JSON) rather than imperative commands
2. Use namespaces to organize resources
3. Use ConfigMaps and Secrets for configuration
4. Set resource requests and limits for containers
5. Use liveness and readiness probes
6. Implement proper logging and monitoring
7. Use RBAC for access control
8. Regularly update your cluster and applications
9. Implement network policies
10. Backup etcd regularly

## Next Steps
- Explore more advanced concepts like StatefulSets, DaemonSets, and Jobs
- Learn about Helm for package management
- Implement CI/CD with Kubernetes
- Explore service meshes like Istio or Linkerd
- Learn about Kubernetes security best practices