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

**Create Pod**:
Describe: Creates a new Pod in the cluster. The imperative approach creates a Pod directly from the command line with specified parameters, while the declarative approach uses a YAML manifest file to define the Pod configuration. The declarative approach is preferred as it allows version control and easier management.

- Imperative:
`kubectl run simple-pod --image=busybox --restart=Never --command -- sleep 3600`

- Declarative:
`kubectl apply -f example-pod.yaml`


**Describe Pod**:
Describe: Displays detailed information about a specific Pod, including its status, events, container details, resource requests/limits, and configuration. Useful for debugging issues, understanding Pod state, and troubleshooting why a Pod might not be running correctly.

`kubectl describe pod example-pod`

**Delete Pod**:
Describe: Removes a Pod from the cluster. Can delete by Pod name or by referencing a YAML file. The `--force --grace-period=0` option immediately terminates the Pod without waiting for graceful shutdown. Use label selectors to delete multiple Pods matching specific criteria.

`kubectl delete pod <pod-name>`
`kubectl delete -f my-pod.yaml`

Option: delete immediately not wait to terminate
`--force --grace-period=0`

Option: delete many
`kubectl delete pods -l app=myapp`


**Exec pod**:
Describe: Executes a command inside a running container within a Pod. The `-it` flags provide an interactive terminal session. Commonly used to debug issues, inspect files, or run diagnostic commands inside the container.

`kubectl exec -it <pod-name> -- /bin/sh`

**Logs**:
Describe: Retrieves and displays logs from a container running in a Pod. Use the `-c` flag to specify a container name when the Pod has multiple containers. The `-f` flag follows the log output in real-time, similar to `tail -f`.

`kubectl logs <pod-name> [-c <container>]`

Option: follow realtime by `-f`

**Port Forward**:
Describe: Forwards network traffic from a local port on your machine to a port on a Pod. This allows you to access Pod services locally without exposing them through a Service. Useful for testing, debugging, or accessing applications that aren't exposed externally.

`kubectl port-forward pod/<pod-name> 8080:80`


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


## ConfigMap

**Create ConfigMap**:

- Imperative:

`kubectl create configmap my-cm --from-literal=key1=value1 --from-literal=key2=value2`

- Declarative (YAML)

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap
data:
  key1: value1
  config.properties: |  # Multi-line file
    property1=val1
    property2=val2
binaryData:  # Cho binary, base64-encoded
  binary-key: <base64-data>
immutable: true  # Optional
```

`kubectl apply -f cm.yaml`

**Get**:

`kubectl get configmap`

**Describe**:

`kubectl describe cm my-cm`
<!-- (hiển thị data plain) -->

**Edit**:

`kubectl edit cm my-cm`

**Delete**:

`kubectl delete cm my-cm`

**Xem data**:

`kubectl get cm my-cm -o yaml | grep data -A 10`

## Secret

**Create Secret**:

- Imperative:
+ Generic: `kubectl create secret generic my-secret --from-literal=password=supersecret --from-file=ssh-key=/path/to/key`

+ TLS: `kubectl create secret tls my-tls --cert=path/to/cert --key=path/to/key`

+ Docker registry: `kubectl create secret docker-registry my-reg --docker-server=... --docker-username=...`

- Declarative (YAML)

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque  # Generic
data:
  password: c3VwZXJzZWNyZXQ=  # echo -n 'supersecret' | base64
  api-key: YXBpa2V5Cg==  
stringData:  # Plain text, Kubernetes sẽ encode
  username: admin
immutable: true
```

`kubectl apply -f secret.yaml`

Note: Sử dụng stringData để tránh encode thủ công.

**Get**:

`kubectl get secret`

**Describe**:

`kubectl describe secret my-secret`
<!-- (không hiển thị data) -->

**Edit**:

`kubectl edit cm my-cm`

**Delete**:

`kubectl delete cm my-cm`

**Xem data**:

`kubectl get secret my-secret -o jsonpath='{.data.password}' | base64 -d`

## Mount ConfigMap/Secret Vào Pod Trong YAML

### Mount Làm Environment Variables

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: app
    image: busybox
    env:
    - name: KEY1
      valueFrom:
        configMapKeyRef:
          name: my-configmap
          key: key1
    - name: PASSWORD
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: password
```

### Mount Làm Volumes

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: app
    image: nginx
    volumeMounts:
    - name: config-vol
      mountPath: /etc/config  # Đường dẫn trong container
      readOnly: true
    - name: secret-vol
      mountPath: /etc/secret
  volumes:
  - name: config-vol
    configMap:
      name: my-configmap
      items:  # Optional, chỉ mount key cụ thể
      - key: config.properties
        path: app.conf  # Tên file trong volume
  - name: secret-vol
    secret:
      secretName: my-secret
      items:
      - key: password
        path: db-pass.txt
        mode: 0400  # Permissions
```


Note: Dùng subPath để mount file cụ thể mà không overwrite thư mục.

## Environment Variables


### Command

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: env-pod
spec:
  containers:
  - name: my-container
    image: busybox
    env:  # Mảng các env var
    - name: STATIC_VAR  # Tên biến (uppercase convention)
      value: "hello world"  # Giá trị tĩnh
    - name: CONFIG_VAR
      valueFrom:
        configMapKeyRef:  # Từ ConfigMap
          name: my-configmap
          key: app.key
          optional: false  # Default false, error nếu không tồn tại
    - name: SECRET_VAR
      valueFrom:
        secretKeyRef:  # Từ Secret
          name: my-secret
          key: password
    - name: POD_NAME  # Downward API
      valueFrom:
        fieldRef:
          fieldPath: metadata.name  # Các field: metadata.name, status.podIP, spec.nodeName, etc.
    - name: CPU_LIMIT  # Resource field
      valueFrom:
        resourceFieldRef:
          containerName: my-container  # Optional
          resource: limits.cpu
    envFrom:  # Inject toàn bộ ConfigMap/Secret làm env vars (prefix optional)
    - configMapRef:
        name: my-configmap
    - secretRef:
        name: my-secret
        prefix: DB_  # Optional, prefix keys
```

### Args


### CLIs

**Tạo Pod với env vars (imperative)**:

`kubectl run env-pod --image=busybox --env="KEY=value" --command -- sleep infinity`

**Xem env vars trong Pod**:

Description: liệt kê tất cả env

`kubectl exec env-pod -- env`

**Describe Pod**:

Description: xem env trong spec

`kubectl describe pod env-pod`

**Edit Pod**:

Description: sửa env, nhưng Pod immutable nên thường recreate

`kubectl edit pod env-pod`

**Generate YAML**:

`kubectl run --dry-run=client -o yaml --env="KEY=val" --command -- echo hello > pod.yaml`

## ReplicaSet

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-rs
  labels:
    app: myapp
spec:
  replicas: 3  # Số lượng Pods
  selector:
    matchLabels:  # Equality-based
      app: myapp
    matchExpressions:  # Set-based (optional)
    - key: tier
      operator: In
      values: [frontend]
  template:  # Pod template
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: nginx
        image: nginx:1.14
        ports:
        - containerPort: 80
```

apply: `kubectl apply -f rs.yaml`

### CLIs

**Tạo Imperative**:

`kubectl create rs my-rs --image=nginx --replicas=3`

note: ít dùng


**Get/List**:

`kubectl get rs`

**Scale**:

`kubectl scale rs my-rs --replicas=5`


## Deployment

Description: Cấu trúc mở rộng từ RS

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:  # Giống RS
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: nginx
        image: nginx:1.14
  strategy:  # Update strategy
    type: RollingUpdate  # Hoặc Recreate (kill all then create)
    rollingUpdate:
      maxSurge: 25%  # Số Pods thêm tối đa (int hoặc %)
      maxUnavailable: 25%  # Số Pods unavailable tối đa
  minReadySeconds: 10  # Thời gian chờ Pod ready trước khi coi success
  revisionHistoryLimit: 10  # Giữ bao nhiêu RS cũ cho rollback
  paused: false  # Pause rollout (optional)
```

### CLIs

**Tạo Imperative**:

`kubectl create deployment my-dep --image=nginx --replicas=3`


**Get/List**:

`kubectl get deployments`
`kubectl get deployments -o wide`


**Describe**:

`kubectl describe deployment my-dep`

**Scale**:

`kubectl scale deployment my-dep --replicas=5`

**Update**:

`kubectl set image deployment/my-dep nginx=nginx:1.16` 
note: trigger rollout

edit YAML: `kubectl edit deployment my-dep`


**Rollout Management**:

Status: `kubectl rollout status deployment/my-dep`
History: `kubectl rollout status deployment/my-dep`
Rollback: `kubectl rollout undo deployment/my-dep --to-revision=2`
Pause/Resume: `kubectl rollout pause deployment/my-dep` / `kubectl rollout resume deployment/my-dep`

**Delete**:

`kubectl delete deployment my-dep`
note: xóa cascade RS và Pods

