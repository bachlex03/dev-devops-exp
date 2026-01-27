# KUBERNETES BASIC V2

Description: All things you need to know as a beginner.
## Table of Contents

- [Kubernetes](#kubernetes)

# Core Concepts

## Kubernetes
- **en**:
  - **What**: Kubernetes (K8s) is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.
  - **Who**: Originally designed by Google, it is now maintained by the Cloud Native Computing Foundation (CNCF).
  - **Where**: It can run on-premise, in public clouds, or in hybrid environments.
  - **When**: Use Kubernetes when you need to manage multiple containers across multiple hosts, handle automatic scaling, or ensure high availability.
  - **Why**: It significantly reduces the complexity of managing microservices, ensures self-healing, and provides efficient resource utilization.
  - **How**: It works by defining a "desired state" in YAML files, which the control plane continuously monitors and maintains across worker nodes.
- **vi**:
  - **What (Cái gì)**: Kubernetes (K8s) là một nền tảng điều phối container mã nguồn mở giúp tự động hóa việc triển khai, mở rộng và quản lý các ứng dụng container hóa.
  - **Who (Ai)**: Ban đầu được thiết kế bởi Google, hiện nay được duy trì bởi Cloud Native Computing Foundation (CNCF).
  - **Where (Ở đâu)**: Có thể chạy tại chỗ (on-premise), trên các đám mây công cộng (public cloud), hoặc trong môi trường hỗn hợp (hybrid).
  - **When (Khi nào)**: Sử dụng Kubernetes khi bạn cần quản lý nhiều container trên nhiều host, xử lý việc tự động mở rộng, hoặc đảm bảo tính sẵn sàng cao.
  - **Why (Tại sao)**: Nó giúp giảm đáng kể sự phức tạp khi quản lý microservices, đảm bảo khả năng tự phục hồi (self-healing) và cung cấp khả năng sử dụng tài nguyên hiệu quả.
  - **How (Như thế nào)**: Hoạt động bằng cách định nghĩa "trạng thái mong muốn" trong các tệp YAML, sau đó thành phần điều khiển (control plane) sẽ liên tục giám sát và duy trì trạng thái đó trên các worker node.

> **Note**:
> - **en**: **Hosts** in Kubernetes refer to **Nodes** (worker machines), which can be either physical machines or virtual machines.
> - **vi**: **Hosts** trong Kubernetes dùng để chỉ các **Nodes** (máy worker), có thể là máy vật lý hoặc máy ảo.

### Benifits

ref: "https://devops.vn/posts/bai-1-gioi-thieu-kubernetes-va-khai-niem-cluster-cho-ckad/"

## Pod
- **en**:
  - **What**: The smallest, most basic deployable object in Kubernetes. It represents a single instance of a running process in your cluster.
  - **Where**: Runs on an individual Node.
  - **When**: Created by controllers like Deployments or StatefulSets to run your application containers.
  - **Why**: To encapsulate one or more containers (like an application container and a sidecar) that **share the same network IP, storage, and lifecycle**.
  - **How**: Pods are defined in YAML manifests and scheduled onto Nodes by the Kubernetes scheduler.
- **vi**:
  - **What (Cái gì)**: Đối tượng nhỏ nhất và cơ bản nhất có thể triển khai trong Kubernetes. Nó đại diện cho một instance duy nhất của một tiến trình đang chạy trong cluster.
  - **Where (Ở đâu)**: Chạy trên một Node cụ thể.
  - **When (Khi nào)**: Được tạo bởi các controller như Deployment hoặc StatefulSet để chạy các ứng dụng container của bạn.
  - **Why (Tại sao)**: Để đóng gói một hoặc nhiều container (như ứng dụng chính và sidecar) **dùng chung địa chỉ IP, bộ lưu trữ và vòng đời**.
  - **How (Như thế nào)**: Pod được định nghĩa trong các tệp YAML và được lập lịch lên các Node bởi bộ lập lịch (scheduler) của Kubernetes.

> **Note on Volumes & mountPath**:
> - **en**: The `mountPath` is **local to each container**. Different containers in the same Pod can mount the **same volume** at **different paths**. For example, an init-container can mount a volume at `/work-dir` to write data, while the main container mounts it at `/app/data` to read that same data.
> - **vi**: `mountPath` là **riêng biệt cho từng container**. Các container khác nhau trong cùng một Pod có thể gắn (mount) **cùng một volume** tại **các đường dẫn khác nhau**. Ví dụ: một init-container có thể mount volume tại `/work-dir` để ghi dữ liệu, trong khi container chính mount volume đó tại `/app/data` để đọc cùng một dữ liệu đó.

## Node
- **en**:
  - **What**: A worker machine in Kubernetes; it can be a virtual or physical machine.
  - **Where**: Part of a Kubernetes cluster.
  - **When**: Added to the cluster to provide compute power; can be scaled up or down based on load.
  - **Why**: To provide the necessary environment (CPU, RAM, network) to run Pods.
  - **How**: Each Node runs a `kubelet` (agent), a `container runtime` (like Docker/containerd), and a `kube-proxy` for networking.
- **vi**:
  - **What (Cái gì)**: Một máy worker trong Kubernetes; có thể là máy ảo hoặc máy vật lý.
  - **Where (Ở đâu)**: Là một phần của cụm (cluster) Kubernetes.
  - **When (Khi nào)**: Được thêm vào cụm để cung cấp sức mạnh tính toán; có thể mở rộng hoặc thu hẹp tùy theo tải.
  - **Why (Tại sao)**: Cung cấp môi trường cần thiết (CPU, RAM, mạng) để chạy các Pod.
  - **How (Như thế nào)**: Mỗi Node chạy một `kubelet` (agent), một `container runtime` (như Docker/containerd) và một `kube-proxy` để quản lý mạng.

## Cluster
- **en**:
  - **What**: A set of Node machines for running containerized applications managed by Kubernetes.
  - **Where**: Can be hosted on-premise, in the cloud (EKS, GKE, AKS), or locally (Minikube, Kind).
  - **Why**: To provide a unified, highly available platform that can manage applications at scale across multiple machines.
  - **How**: Consists of at least one **Control Plane** (the brain) and multiple **Worker Nodes** (where apps run).
- **vi**:
  - **What (Cái gì)**: Một tập hợp các máy Node để chạy các ứng dụng container hóa được quản lý bởi Kubernetes.
  - **Where (Ở đâu)**: Có thể được lưu trữ tại chỗ (on-premise), trên đám mây (EKS, GKE, AKS), hoặc cục bộ (Minikube, Kind).
  - **Why (Tại sao)**: Cung cấp một nền tảng thống nhất, có tính sẵn sàng cao để quản lý ứng dụng trên quy mô lớn trên nhiều máy khác nhau.
  - **How (Như thế nào)**: Bao gồm ít nhất một **Control Plane** (bộ não điều khiển) và nhiều **Worker Nodes** (nơi ứng dụng thực sự chạy).

# Storages (Persistent Volumes & Persistent Volume Claims)
- **en**:
  - **What**: **PersistentVolume (PV)** is a piece of storage in the cluster provisioned by an administrator or dynamically via Storage Classes. **PersistentVolumeClaim (PVC)** is a request for storage by a user (Pod).
  - **Where**: PVs are cluster-wide resources, whereas PVCs exist within a specific **Namespace**.
  - **When**: Use them when your application needs to store data that survives Pod restarts, rescheduling, or updates (e.g., Databases).
  - **Why**: To decouple storage implementation from storage consumption. Developers don't need to know the underlying storage tech (NFS, AWS EBS), they just request "10GB of storage" via a PVC.
  - **How**: A user creates a PVC. Kubernetes looks for a matching PV (size, access mode). If found, they are "bound" together. The Pod then mounts this PVC as a volume.
- **vi**:
  - **What (Cái gì)**: **PersistentVolume (PV)** là phần không gian lưu trữ trong cụm được cung cấp bởi quản trị viên hoặc cấp phát động qua Storage Class. **PersistentVolumeClaim (PVC)** là yêu cầu sử dụng lưu trữ từ phía người dùng (hoặc Pod).
  - **Where (Ở đâu)**: PV là tài nguyên cấp cụm (cluster-wide), trong khi PVC tồn tại trong một **Namespace** cụ thể.
  - **When (Khi nào)**: Sử dụng khi ứng dụng cần lưu trữ dữ liệu bền vững, không bị mất đi khi Pod khởi động lại, được lập lịch lại hoặc cập nhật (ví dụ: Cơ sở dữ liệu).
  - **Why (Tại sao)**: Để tách biệt việc triển khai lưu trữ khỏi việc tiêu thụ lưu trữ. Lập trình viên không cần biết công nghệ lưu trữ bên dưới (NFS, AWS EBS), họ chỉ cần yêu cầu "10GB lưu trữ" thông qua PVC.
  - **How (Như thế nào)**: Người dùng tạo một PVC. Kubernetes tìm kiếm một PV phù hợp (dung lượng, chế độ truy cập). Nếu tìm thấy, chúng sẽ được "liên kết" (bound) với nhau. Pod sau đó sẽ gắn (mount) PVC này như một volume.


# Other Concepts

## Container Command and Args
- **en**:
  - **What**: `command` and `args` in Kubernetes define the executable and its parameters for a container. They correspond to Docker's `ENTRYPOINT` and `CMD`.
  - **Who**: Defined by the developer or DevOps engineer in the Pod specification.
  - **Where**: Specified within the `spec.containers` field of a Pod, Deployment, or other workload objects.
  - **When**: Use them to override the image's default startup behavior or to pass specific flags/scripts to the container at runtime.
  - **Why**: To gain precise control over what process runs inside the container and how it is configured without modifying the container image itself.
  - **How**: `command` overrides the Docker `ENTRYPOINT`, and `args` overrides the Docker `CMD`. If `command` is provided, it becomes the entry point; if `args` is also provided, they are passed as arguments to that command.
- **vi**:
  - **What (Cái gì)**: `command` và `args` trong Kubernetes xác định file thực thi và các tham số của nó cho một container. Chúng tương ứng với `ENTRYPOINT` và `CMD` trong Docker.
  - **Who (Ai)**: Được định nghĩa bởi lập trình viên hoặc kỹ sư DevOps trong cấu hình Pod.
  - **Where (Ở đâu)**: Được khai báo trong trường `spec.containers` của Pod, Deployment hoặc các đối tượng workload khác.
  - **When (Khi nào)**: Sử dụng để ghi đè hành vi khởi động mặc định của image hoặc để truyền các tham số/script cụ thể vào container khi chạy.
  - **Why (Tại sao)**: Để kiểm soát chính xác tiến trình nào chạy bên trong container và cách nó được cấu hình mà không cần sửa đổi chính container image đó.
  - **How (Như thế nào)**: `command` ghi đè `ENTRYPOINT` của Docker, và `args` ghi đè `CMD` của Docker. Nếu `command` được khai báo, nó trở thành điểm khởi đầu; nếu `args` cũng được khai báo, chúng sẽ được truyền vào làm tham số cho lệnh đó.

> **Execution Rules**:
> - **en**: If you define `command` but no `args`, only the command is run. If you define `args` but no `command`, the image's default `ENTRYPOINT` is run with your `args`.
> - **vi**: Nếu bạn xác định `command` nhưng không có `args`, chỉ lệnh đó được chạy. Nếu bạn xác định `args` nhưng không có `command`, lệnh `ENTRYPOINT` mặc định của image sẽ chạy với các `args` của bạn.

## Deployment & ReplicaSet
- **en**:
  - **What**: **ReplicaSet** ensures a stable set of replica Pods running at any given time (ensure the right number of pods are running). **Deployment** is a higher-level controller that manages ReplicaSets to provide declarative updates (rolling updates) and rollbacks and desired state (number of pods, replica sets).
  - **Where**: Deployed within a Kubernetes Cluster.
  - **When**: Use **Deployment** for stateless applications that need automatic scaling, high availability, and versioned updates. It is the standard way to deploy apps; ReplicaSets are rarely managed directly.
  - **Why**: To automate application deployment, maintain the desired number of replicas (self-healing), and manage seamless updates without downtime.
  - **How**: You define the desired state in a YAML manifest (e.g., image version, replica count). The Deployment controller handles the transition from the current state to the desired state by creating and scaling ReplicaSets.
- **vi**:
  - **What (Cái gì)**: **ReplicaSet** đảm bảo một số lượng Pod bản sao (replica) nhất định luôn chạy ổn định (đảm bảo đúng số lượng pod đang chạy). **Deployment** là một controller cấp cao hơn, quản lý các ReplicaSet để cung cấp các bản cập nhật khai báo (rolling updates) và khả năng hoàn tác (rollbacks).
  - **Where (Ở đâu)**: Được triển khai bên trong cụm (Cluster) Kubernetes.
  - **When (Khi nào)**: Sử dụng **Deployment** cho các ứng dụng stateless (không lưu trạng thái) cần tự động mở rộng, có tính sẵn sàng cao và cập nhật theo phiên bản. Đây là cách tiêu chuẩn để triển khai ứng dụng; ReplicaSet hiếm khi được quản lý trực tiếp.
  - **Why (Tại sao)**: Để tự động hóa việc triển khai ứng dụng, duy trì số lượng bản sao mong muốn (tự phục hồi) và quản lý cập nhật mượt mà không gây gián đoạn dịch vụ.
  - **How (Như thế nào)**: Bạn định nghĩa trạng thái mong muốn trong tệp YAML (ví dụ: phiên bản image, số lượng bản sao). Deployment controller sẽ xử lý quá trình chuyển đổi từ trạng thái hiện tại sang trạng thái mong muốn bằng cách tạo và điều chỉnh các ReplicaSet.

## Configmaps and Secrets
- **en**:
  - **What**: **ConfigMap** is an API object used to store non-confidential data in key-value pairs. **Secret** is a similar object used to store sensitive data (like passwords, OAuth tokens, or ssh keys).
  - **Where**: Stored in the Kubernetes cluster's etcd and can be mounted into Pods as environment variables or files in a volume.
  - **When**: Use **ConfigMap** for application configuration files or command-line arguments. Use **Secret** for any sensitive data that shouldn't be in plain text in Pod specs or container images.
  - **Why**: To separate configuration settings from application code (Decoupling) and to manage sensitive information securely without hardcoding it.
  - **How**: You create them via YAML or `kubectl create`, then reference them in a Pod's `spec.containers.env` or `spec.volumes` section.
- **vi**:
  - **What (Cái gì)**: **ConfigMap** là một đối tượng API dùng để lưu trữ dữ liệu không bảo mật dưới dạng cặp key-value. **Secret** là một đối tượng tương tự nhưng dùng để lưu trữ dữ liệu nhạy cảm (như mật khẩu, OAuth tokens, hoặc ssh keys).
  - **Where (Ở đâu)**: Được lưu trữ trong etcd của cụm Kubernetes và có thể được gắn (mount) vào Pod dưới dạng biến môi trường hoặc tệp trong một volume.
  - **When (Khi nào)**: Sử dụng **ConfigMap** cho các tệp cấu hình ứng dụng hoặc tham số dòng lệnh. Sử dụng **Secret** cho bất kỳ dữ liệu nhạy cảm nào không nên để ở dạng văn bản thuần túy trong Pod spec hoặc container image.
  - **Why (Tại sao)**: Để tách biệt các thiết lập cấu hình khỏi mã nguồn ứng dụng (Decoupling) và quản lý thông tin nhạy cảm một cách an toàn mà không cần viết cứng (hardcode) vào mã.
  - **How (Như thế nào)**: Bạn tạo chúng qua YAML hoặc lệnh `kubectl create`, sau đó tham chiếu chúng trong phần `spec.containers.env` hoặc `spec.volumes` của Pod.

> **Note**:
> - **en**: 
>   - **Naming**: Kubernetes resource names (like ConfigMaps) must be lowercase and follow RFC 1123 (e.g., `my-configmap`, NOT `my-ConfigMap`).
>   - **Binary Data**: Use `binaryData` for base64-encoded content. Ensure the base64 string is valid and not a placeholder.
> - **vi**:
>   - **Đặt tên**: Tên tài nguyên Kubernetes (như ConfigMaps) phải viết thường và tuân theo chuẩn RFC 1123 (ví dụ: `my-configmap`, KHÔNG phải `my-ConfigMap`).
>   - **Dữ liệu nhị phân**: Sử dụng `binaryData` cho nội dung được mã hóa base64. Đảm bảo chuỗi base64 hợp lệ và không phải là text giữ chỗ.


### Benifits of ConfigMaps and Secrets

ref: [ConfigMaps and Secrets](https://devops.vn/posts/bai-4-su-dung-configmap-va-secret-trong-yaml/)


## Probes
- **en**:
  - **What**: Probes are health checks performed by the `kubelet` to monitor the status of containers.
  - **Who**: Defined by developers/DevOps engineers in the Pod specification.
  - **Where**: Executed locally on the Node by the `kubelet`.
  - **When**: Throughout the container's lifecycle to ensure reliability and availability.
  - **Why**: To enable self-healing (restarting crashed apps) and ensure traffic only flows to ready instances.
  - **How**: Using three main types: **Liveness**, **Readiness**, and **Startup**.
- **vi**:
  - **What (Cái gì)**: Probes là các bước kiểm tra sức khỏe được thực hiện bởi `kubelet` để giám sát trạng thái của các container.
  - **Who (Ai)**: Do lập trình viên hoặc kỹ sư DevOps định nghĩa trong cấu hình Pod.
  - **Where (Ở đâu)**: Được thực hiện cục bộ trên Node bởi `kubelet`.
  - **When (Khi nào)**: Diễn ra trong suốt vòng đời của container để đảm bảo tính tin cậy và sẵn sàng.
  - **Why (Tại sao)**: Để cho phép tự phục hồi (khởi động lại app bị treo) và đảm bảo lưu lượng truy cập chỉ đến được các instance đã sẵn sàng.
  - **How (Như thế nào)**: Gồm ba loại chính: **Liveness**, **Readiness**, và **Startup**.

### Liveness Probe
- **en**:
  - **What**: A check to see if a container is still alive and running correctly.
  - **Why**: To automatically restart containers that enter an unrecoverable state (e.g., deadlock, infinite loop).
  - **When**: Throughout the entire lifecycle of the container after it successfully starts.
  - **How**: If it fails, Kubernetes kills the container and starts a new one based on the `restartPolicy`.
- **vi**:
  - **What (Cái gì)**: Kiểm tra xem container còn "sống" và hoạt động bình thường không.
  - **Why (Tại sao)**: Để tự động khởi động lại các container rơi vào trạng thái lỗi không thể phục hồi (ví dụ: bị treo deadlock).
  - **When (Khi nào)**: Trong suốt vòng đời của container sau khi nó đã bắt đầu chạy.
  - **How (Như thế nào)**: Nếu thất bại, Kubernetes sẽ xóa container đó và khởi tạo lại theo `restartPolicy`.

### Readiness Probe
- **en**:
  - **What**: A check to see if a container is ready to accept and process incoming network traffic.
  - **Why**: To ensure users don't hit an app that is still initializing, loading data, or temporarily overloaded.
  - **When**: Before routing traffic and periodically while the Pod is active in a Service.
  - **How**: If it fails, the Pod's IP is removed from all Service endpoints (traffic is stopped but the container keeps running).
- **vi**:
  - **What (Cái gì)**: Kiểm tra xem container đã sẵn sàng nhận và xử lý các yêu cầu mạng chưa.
  - **Why (Tại sao)**: Đảm bảo người dùng không truy cập vào app đang khởi tạo, đang tải dữ liệu hoặc đang bị quá tải.
  - **When (Khi nào)**: Trước khi điều phối traffic và định kỳ khi Pod đang nằm trong một Service.
  - **How (Như thế nào)**: Nếu thất bại, IP của Pod sẽ bị gỡ khỏi danh sách Service endpoints (ngừng nhận traffic nhưng container vẫn chạy).

### Startup Probe
- **en**:
  - **What**: A check designed specifically for the initial startup phase of slow-starting applications.
  - **Why**: To prevent Liveness probes from killing an app before it has finished its heavy initialization (e.g., loading a large JVM).
  - **When**: Only during the initial container startup.
  - **How**: It disables Liveness and Readiness probes until it succeeds. Once it succeeds, the other probes take over.
- **vi**:
  - **What (Cái gì)**: Kiểm tra dành riêng cho giai đoạn khởi động ban đầu của các ứng dụng cần nhiều thời gian.
  - **Why (Tại sao)**: Ngăn Liveness probe khởi động lại app khi nó chưa kịp hoàn tất các bước khởi tạo nặng (như load JVM).
  - **When (Khi nào)**: Chỉ diễn ra trong quá trình khởi động ban đầu.
  - **How (Như thế nào)**: Nó sẽ tạm dừng các Liveness và Readiness probe cho đến khi nó thành công. Sau khi thành công, các probe kia mới bắt đầu làm việc.

### Probe Check Mechanisms
- **en**:
  - **Exec**: Runs a command inside the container. Success is exit code 0. Use for non-networked apps or local file checks.
  - **HTTP GET**: Performs an HTTP request. Success is status code 200-399. The standard choice for web apps and APIs.
  - **TCP Socket**: Attempts to open a TCP connection to a port. Success if port is open. Use for DBs, Redis, or non-HTTP services.
  - **gRPC**: Performs a gRPC health check (v1.24+). Success if status is `SERVING`. Native choice for gRPC-based microservices.
- **vi**:
  - **Exec (Thực thi)**: Chạy một lệnh trong container. Thành công nếu exit code là 0. Dùng cho app không có mạng hoặc kiểm tra file cục bộ.
  - **HTTP GET**: Gửi một request HTTP. Thành công nếu status code từ 200-399. Là lựa chọn tiêu chuẩn cho web app và API.
  - **TCP Socket**: Thử mở kết nối TCP tới một cổng. Thành công nếu cổng đó đang mở. Dùng cho DB, Redis hoặc các dịch vụ không phải HTTP.
  - **gRPC**: Thực hiện kiểm tra sức khỏe qua gRPC (bản v1.24+). Thành công nếu trạng thái là `SERVING`. Lựa chọn tối ưu cho gRPC microservices.

### Probe Configuration Parameters
- **en**:
  - **initialDelaySeconds**: Number of seconds after the container has started before liveness or readiness probes are initiated. (Default: 0).
  - **periodSeconds**: How often (in seconds) to perform the probe. (Default: 10. Minimum: 1).
  - **timeoutSeconds**: Number of seconds after which the probe times out. (Default: 1. Minimum: 1).
  - **successThreshold**: Minimum consecutive successes for the probe to be considered successful after having failed. (Default: 1. Must be 1 for liveness).
  - **failureThreshold**: When a probe fails, Kubernetes will try failureThreshold times before giving up. (Default: 3. Minimum: 1).
- **vi**:
  - **initialDelaySeconds**: Số giây chờ sau khi container khởi động trước khi bắt đầu thực hiện các probe. (Mặc định: 0).
  - **periodSeconds**: Khoảng thời gian giữa các lần thực hiện probe (tính bằng giây). (Mặc định: 10. Tối thiểu: 1).
  - **timeoutSeconds**: Số giây tối đa để đợi kết quả từ probe trước khi coi là thất bại. (Mặc định: 1. Tối thiểu: 1).
  - **successThreshold**: Số lần thành công liên tiếp tối thiểu để coi probe là thành công sau khi đã từng thất bại. (Mặc định: 1. Phải là 1 đối với liveness).
  - **failureThreshold**: Số lần thất bại liên tiếp tối đa trước khi Kubernetes coi là thất bại hoàn toàn và thực hiện hành động (như restart). (Mặc định: 3. Tối thiểu: 1).

> **Pro-Tip**:
> - **en**: Use a high `failureThreshold` with a short `periodSeconds` for stable monitoring without accidental restarts.
> - **vi**: Sử dụng `failureThreshold` cao kết hợp với `periodSeconds` ngắn để giám sát ổn định mà không gây ra khởi động lại nhầm.


## Service
- **en**:
  - **What**: An abstract way to expose an application running on a set of Pods as a network service.
  - **Where**: Lives within a Namespace and provides a stable DNS name/IP for Pods.
  - **When**: Use it whenever one part of your application (e.g., frontend) needs to talk to another part (e.g., backend) or when you need to expose your app to external users.
  - **Why**: Pods are ephemeral; their IPs change when they restart. Services provide a **persistent endpoint** that doesn't change.
  - **How**: It uses **Selectors** to track Pods with specific labels and automatically balances traffic among them.
- **vi**:
  - **What (Cái gì)**: Một cách trừu tượng để lộ diện một ứng dụng đang chạy trên một nhóm các Pod dưới dạng một dịch vụ mạng.
  - **Where (Ở đâu)**: Tồn tại bên trong một Namespace và cung cấp một tên DNS/IP ổn định cho các Pod.
  - **When (Khi nào)**: Sử dụng bất cứ khi nào một phần của ứng dụng (frontend) cần giao tiếp với phần khác (backend) hoặc khi bạn cần lộ diện ứng dụng cho người dùng bên ngoài.
  - **Why (Tại sao)**: Các Pod có tính chất tạm thời; IP của chúng thay đổi khi khởi động lại. Service cung cấp một **điểm cuối bền vững** không đổi.
  - **How (Như thế nào)**: Nó sử dụng **Selector** để theo dõi các Pod có nhãn (label) cụ thể và tự động cân bằng tải giữa các Pod đó.

### Service Types
- **en**:
  - **ClusterIP (Default)**: Exposes the Service on a cluster-internal IP. Reachable only from within the cluster.
  - **NodePort**: Exposes the Service on each Node's IP at a static port (30000-32767). Reachable from outside via `<NodeIP>:<NodePort>`.
  - **LoadBalancer**: Exposes the Service externally using a cloud provider's load balancer. Automatically creates NodePort and ClusterIP.
  - **ExternalName**: Maps the Service to a DNS name (CNAME record). Used for connecting to external services like DBs outside K8s.
- **vi**:
  - **ClusterIP (Mặc định)**: Cung cấp IP nội bộ trong cụm. Chỉ có thể truy cập từ bên trong cluster.
  - **NodePort**: Mở một cổng tĩnh trên IP của mỗi Node (30000-32767). Có thể truy cập từ bên ngoài qua `<NodeIP>:<NodePort>`.
  - **LoadBalancer**: Sử dụng bộ cân bằng tải của nhà cung cấp Cloud (AWS, GCP, Azure). Tự động tạo NodePort và ClusterIP.
  - **ExternalName**: Ánh xạ Service tới một tên miền DNS (bản ghi CNAME). Dùng để kết nối với các dịch vụ bên ngoài cụm.

#### Service with No Selector (Manual Endpoints)
- **en**:
  - **What**: A Service defined without a `selector`. You must manually create an `Endpoints` object with the same name.
  - **Why**: Used to point to services **outside** the cluster (e.g., an external DB, a legacy server).
- **vi**:
  - **What (Cái gì)**: Một Service được định nghĩa không có `selector`. Bạn phải tự tạo thủ công một đối tượng `Endpoints` có cùng tên.
  - **Why (Tại sao)**: Dùng để trỏ tới các dịch vụ nằm **ngoài** cluster (ví dụ: DB bên ngoài, server cũ).
  - **Note on "IP"**:
    - **en**: The `ip` field in `Endpoints` specifies the **Target Destination**. It maps the internal Service Name to a fixed external address.
    - **vi**: Trường `ip` trong `Endpoints` chỉ định **Địa chỉ Đích**. Nó giúp ánh xạ Tên Service nội bộ tới một địa chỉ bên ngoài cố định.

#### ClusterIP vs NodePort Comparison
| Feature | ClusterIP | NodePort |
| :--- | :--- | :--- |
| **Reachability** | **Internal Only** (Inside cluster) | **External** (via Node IP) |
| **IP/Port** | Internal Virtual IP / Any Port | Node IP / Port 30000-32767 |
| **Relationship** | Basic service | Includes a ClusterIP automatically |
| **Use case** | Microservice communication | Dev/Testing or Simple Exposure |

| Đặc điểm | ClusterIP | NodePort |
| :--- | :--- | :--- |
| **Truy cập** | **Chỉ nội bộ** (Trong cụm) | **Bên ngoài** (Qua IP của Node) |
| **IP/Cổng** | IP ảo nội bộ / Cổng bất kỳ | IP của Node / Cổng 30000-32767 |
| **Mối quan hệ** | Service cơ bản | Tự động bao gồm cả ClusterIP |
| **Ứng dụng** | Giao tiếp giữa các Service | Test hoặc lộ diện app đơn giản |


## Networking and Load Balancing
- **en**:
  - **What**: An abstraction layer that enables communication between Pods, Services, and external traffic. Main objects include **Services** (ClusterIP, NodePort, LoadBalancer) for internal/external access and **Ingress** for HTTP/HTTPS routing.
  - **Where**: Operates at the cluster level and at the cluster edge.
  - **When**: Use a **Service** when you need a stable entry point (IP/DNS) for ephemeral Pods. Use **Ingress** when you need to expose multiple services under a single IP and manage SSL/TLS.
  - **Why**: Pod IPs are dynamic and change if they restart. Networking objects provide a persistent identity and automatic Load Balancing across Pod replicas.
  - **How**: Services use **Selectors** to track Pods; `kube-proxy` manages the routing logic. Ingress controllers (like Nginx) act as reverse proxies to route traffic based on hostnames or paths.
- **vi**:
  - **What (Cái gì)**: Một lớp trừu tượng cho phép giao tiếp giữa các Pod, Service và lưu lượng bên ngoài. Các đối tượng chính bao gồm **Service** (ClusterIP, NodePort, LoadBalancer) để truy cập nội bộ/bên ngoài và **Ingress** để điều hướng HTTP/HTTPS.
  - **Where (Ở đâu)**: Hoạt động ở cấp độ cụm (cluster) và tại biên của cụm.
  - **When (Khi nào)**: Sử dụng **Service** khi bạn cần một điểm truy cập ổn định (IP/DNS) cho các Pod có tính chất tạm thời. Sử dụng **Ingress** khi bạn cần lộ diện nhiều service dưới một IP duy nhất và quản lý SSL/TLS.
  - **Why (Tại sao)**: IP của Pod là động và sẽ thay đổi nếu chúng khởi động lại. Các đối tượng Networking cung cấp một định danh bền vững và tự động Cân bằng tải (Load Balancing) giữa các bản sao của Pod.
  - **How (Như thế nào)**: Service sử dụng **Selector** để theo dõi các Pod; `kube-proxy` quản lý logic điều hướng. Ingress controller (như Nginx) đóng vai trò là reverse proxy để điều hướng lưu lượng dựa trên hostname hoặc đường dẫn.
 
### Load Balancing
- **en**:
  - **What**: Distributes network traffic across multiple healthy Pod replicas.
  - **Why**: Ensures no single Pod is overwhelmed and provides high availability (HA).
  - **Who**: Handled by `kube-proxy` (internal) and Cloud Load Balancers (external).
  - **How**: 
    - **Standard Service**: L4 (TCP/UDP) balancing using iptables/IPVS.
    - **Ingress**: L7 (HTTP/HTTPS) balancing with advanced features like path-routing.
- **vi**:
  - **What (Cái gì)**: Phân phối lưu lượng mạng đến nhiều Pod bản sao đang khỏe mạnh.
  - **Why (Tại sao)**: Đảm bảo không có Pod nào bị quá tải và cung cấp tính sẵn sàng cao (HA).
  - **Who (Ai)**: Được xử lý bởi `kube-proxy` (nội bộ) và Cloud Load Balancers (bên ngoài).
  - **How (Như thế nào)**: 
    - **Service chuẩn**: Cân bằng tải ở tầng L4 (TCP/UDP) dùng iptables/IPVS.
    - **Ingress**: Cân bằng tải ở tầng L7 (HTTP/HTTPS) với các tính năng nâng cao như điều hướng theo đường dẫn.


### Network Policy
- **en**:
  - **What**: An L3/L4 firewall for Pods that controls traffic flow based on labels.
  - **Why**: By default, K8s allows all pod-to-pod communication. Network policies implement a "Default Deny" or selective allow security model.
  - **Who**: Managed by DevOps/Security teams.
  - **How**: It defines **Ingress** (incoming) and **Egress** (outgoing) rules using `podSelector`, `namespaceSelector`, or `ipBlock`.
- **vi**:
  - **What (Cái gì)**: Một tường lửa tầng L3/L4 cho Pod, kiểm soát luồng traffic dựa trên các nhãn (labels).
  - **Why (Tại sao)**: Mặc định K8s cho phép mọi Pod gọi nhau. Network Policy giúp thực hiện mô hình bảo mật "Chặn mặc định" hoặc "Cho phép có chọn lọc".
  - **Who (Ai)**: Được quản lý bởi đội ngũ DevOps/Bảo mật.
  - **How (Như thế nào)**: Định nghĩa các quy tắc **Ingress** (vào) và **Egress** (ra) bằng cách dùng `podSelector`, `namespaceSelector`, hoặc `ipBlock`.

#### Policy Types
- **en**:
  - **Ingress**: Controls incoming traffic to the Pod. You can limit who can call your app.
  - **Egress**: Controls outgoing traffic from the Pod. You can limit which external APIs or databases your app can talk to.
  - **Default Deny**: A security best practice where you block all traffic by default and then selectively allow only what is necessary (Whitelist approach).
- **vi**:
  - **Ingress**: Kiểm soát lưu lượng truy cập **vào** Pod. Bạn có thể giới hạn ai được phép gọi đến ứng dụng của mình.
  - **Egress**: Kiểm soát lưu lượng truy cập **ra** từ Pod. Bạn có thể giới hạn ứng dụng chỉ được phép gọi ra các API hoặc Database cụ thể.
  - **Default Deny (Chặn mặc định)**: Một nguyên tắc bảo mật tốt nhất, trong đó bạn chặn toàn bộ lưu lượng theo mặc định, sau đó chỉ mở cho những gì thực sự cần thiết (mô hình Whitelist).

> **Key Concept**:
> - **en**: If no policy matches a Pod, it is "Non-Isolated" (All traffic allowed). As soon as a policy selects a Pod, it becomes "Isolated" for that traffic type.
> - **vi**: Nếu không có chính sách nào khớp với Pod, nó ở trạng thái "Không bị cô lập" (Cho phép mọi traffic). Ngay khi có một chính sách chọn trúng Pod đó, nó sẽ trở thành "Bị cô lập" cho loại traffic tương ứng.

### DNS in Kubernetes
- **en**:
  - **What**: A built-in service (CoreDNS) that provides name resolution for Pods and Services.
  - **Why**: Allows applications to find each other using stable names (e.g., `db-svc`) instead of ephemeral IP addresses.
  - **Where**: Runs as a Service/Pod in the `kube-system` namespace.
  - **How**: Follows the pattern `<svc-name>.<namespace>.svc.cluster.local`.
- **vi**:
  - **What (Cái gì)**: Một dịch vụ tích hợp sẵn (CoreDNS) cung cấp khả năng phân giải tên cho Pod và Service.
  - **Why (Tại sao)**: Cho phép các ứng dụng tìm thấy nhau bằng tên ổn định (ví dụ: `db-svc`) thay vì địa chỉ IP hay thay đổi.
  - **Where (Ở đâu)**: Chạy dưới dạng Service/Pod trong namespace `kube-system`.
  - **Where (Ở đâu)**: Chạy dưới dạng Service/Pod trong namespace `kube-system`.
  - **How (Như thế nào)**: Tuân theo cấu trúc `<tên-svc>.<namespace>.svc.cluster.local`.
 
+#### dnsPolicy Types
+- **en**:
+  - **ClusterFirst (Default)**: Queries are sent to the cluster DNS. Non-internal names are forwarded to the node's upstream DNS.
+  - **Default**: Inherits DNS settings directly from the Node's `/etc/resolv.conf`.
+  - **ClusterFirstWithHostNet**: Required for Pods with `hostNetwork: true` to access internal cluster DNS.
+  - **None**: Ignores k8s DNS; requires manual configuration via `dnsConfig`.
+- **vi**:
+  - **ClusterFirst (Mặc định)**: Truy vấn gửi tới DNS của cluster. Các tên miền bên ngoài được chuyển tiếp tới DNS của Node.
+  - **Default**: Kế thừa cấu hình DNS trực tiếp từ file `/etc/resolv.conf` của Node.
+  - **ClusterFirstWithHostNet**: Cần thiết cho các Pod dùng `hostNetwork: true` nếu muốn truy cập DNS nội bộ của cluster.
+  - **None**: Bỏ qua DNS của k8s; yêu cầu cấu hình thủ công thông qua `dnsConfig`.
+
 
 ### Ingress


### Ingress
- **en**:
  - **What**: An API object that manages external access to the services in a cluster, typically HTTP/HTTPS.
  - **Why**: Used for SSL termination, path-based routing (e.g., `/nginx` vs `/httpd`), and virtual hosting (multiple domains on one IP).
  - **Who**: Implemented by an **Ingress Controller** (e.g., NGINX).
  - **How**: It defines rules to route traffic from a single entry point to multiple backend Services.
- **vi**:
  - **What (Cái gì)**: Một đối tượng API quản lý việc truy cập từ bên ngoài vào các service trong cluster, thông thường là HTTP/HTTPS.
  - **Why (Tại sao)**: Dùng để quản lý SSL, điều hướng dựa trên đường dẫn (ví dụ: `/nginx` so với `/httpd`), và chạy nhiều tên miền trên cùng một IP (virtual hosting).
  - **Who (Ai)**: Được thực thi bởi một **Ingress Controller** (ví dụ: NGINX).
  - **How (Như thế nào)**: Nó định nghĩa các quy tắc để điều hướng traffic từ một điểm truy cập duy nhất tới nhiều Service xử lý bên dưới.

+### Lab: Path-Based Routing with Rewrite
+- **en**:
+  - **Goal**: Route `/nginx` to a web service and `/httpd` to another, while using the same base URL.
+  - **Key Annotation**: `nginx.ingress.kubernetes.io/rewrite-target: /`
+  - **Why**: Most apps listen at the root (`/`). If you don't rewrite, the Ingress sends the full path (e.g., `/nginx`) to the app, which usually results in a 404.
+  - **Example**:
+    ```yaml
+    annotations:
+      nginx.ingress.kubernetes.io/rewrite-target: /
+    ```
+- **vi**:
+  - **Mục tiêu**: Điều hướng `/nginx` tới một web service và `/httpd` tới một service khác, dùng chung một URL gốc.
+  - **Cấu hình then chốt**: `nginx.ingress.kubernetes.io/rewrite-target: /`
+  - **Tại sao**: Hầu hết ứng dụng lắng nghe ở đường dẫn gốc (`/`). Nếu không có rule rewrite, Ingress sẽ gửi toàn bộ đường dẫn (ví dụ: `/nginx`) tới ứng dụng, dẫn đến lỗi 404 (Not Found).
+  - **Ví dụ**:
+    ```yaml
+    annotations:
+      nginx.ingress.kubernetes.io/rewrite-target: /
+    ```

## Resource Requests and Limits
- **en**:
  - **What**: Mechanisms to manage CPU and Memory for containers. **Requests** is the minimum guaranteed amount; **Limits** is the maximum allowed amount.
  - **Who**: Specified by developers in the Pod manifest.
  - **Where**: Defined per-container under `resources` field.
  - **When**: Should be used in all production environments to ensure cluster stability.
  - **Why**: To help the scheduler place Pods correctly (via Requests) and prevent "Noisy Neighbor" issues (via Limits).
  - **How**:
    - **Memory**: Exceeding limits leads to **OOMKilled**.
    - **CPU**: Exceeding limits leads to **Throttling** (slowing down).
- **vi**:
  - **What (Cái gì)**: Các cơ chế quản lý CPU và Bộ nhớ cho container. **Requests** là mức tối thiểu được đảm bảo; **Limits** là mức tối đa được phép dùng.
  - **Who (Ai)**: Do lập trình viên chỉ định trong tệp YAML của Pod.
  - **Where (Ở đâu)**: Được định nghĩa cho từng container trong trường `resources`.
  - **When (Khi nào)**: Nên được sử dụng trong mọi môi trường production để đảm bảo sự ổn định của cụm cluster.
  - **Why (Tại sao)**: Giúp bộ lập lịch đặt Pod vào Node phù hợp (qua Requests) và ngăn chặn vấn đề "Noisy Neighbor" (qua Limits).
  - **How (Như thế nào)**:
    - **Memory**: Vượt quá giới hạn sẽ bị **OOMKilled** (bị giết).
    - **CPU**: Vượt quá giới hạn sẽ bị **Throttling** (bị bóp tốc độ).

> **Important Difference**:
> - **en**: **Requests** are used during scheduling (deciding where the Pod goes). **Limits** are enforced during runtime (preventing resource hogging).
> - **vi**: **Requests** được dùng khi lập lịch (quyết định Pod chạy ở đâu). **Limits** được thực thi khi chạy (ngăn chặn việc chiếm dụng tài nguyên).


## Quality of Service (QoS) Classes
- **en**:
  - **What**: A classification system Kubernetes uses to prioritize Pods for eviction when a Node is under resource pressure.
  - **Who**: Automatically assigned by Kubernetes based on the `requests` and `limits` defined.
  - **Where**: Visible in `kubectl describe pod` under the "QoS Class" field.
  - **Why**: To ensure that critical applications (Guaranteed) keep running while less important ones (BestEffort) are sacrificed to maintain Node stability.
  - **How**: Pods are categorized into three levels:
    - **Guaranteed**: `requests == limits` for all containers. (Highest priority).
    - **Burstable**: `requests < limits` or only requests/limits defined. (Medium priority).
    - **BestEffort**: No requests or limits defined. (Lowest priority, killed first).
- **vi**:
  - **What (Cái gì)**: Một hệ thống phân loại mà Kubernetes dùng để ưu tiên các Pod khi cần giải phóng tài nguyên (eviction) trên Node.
  - **Who (Ai)**: Được Kubernetes tự động gán dựa trên cấu hình `requests` và `limits`.
  - **Where (Ở đâu)**: Có thể xem trong lệnh `kubectl describe pod` tại trường "QoS Class".
  - **Why (Tại sao)**: Đảm bảo các ứng dụng quan trọng (Guaranteed) vẫn chạy, trong khi các ứng dụng ít quan trọng hơn (BestEffort) bị hy sinh để bảo vệ Node.
  - **How (Như thế nào)**: Pod được chia làm ba cấp độ:
    - **Guaranteed (Được đảm bảo)**: `requests == limits` cho tất cả container. (Ưu tiên cao nhất).
    - **Burstable (Có thể bùng nổ)**: `requests < limits` hoặc chỉ định nghĩa một trong hai. (Ưu tiên trung bình).
    - **BestEffort (Nỗ lực tối đa)**: Không định nghĩa requests hay limits. (Ưu tiên thấp nhất, bị giết đầu tiên).


## Parameters Tuning
- **en**:
  - **What**: The process of adjusting configuration values (CPU/Memory, Kernel limits, Application flags) to optimize performance, cost, and reliability.
  - **Who**: Performed by DevOps engineers or SREs based on monitoring data (metrics) and load testing.
  - **Where**: Can be applied at the Pod level (`resources`, `env`), Application level (ConfigMaps), or Node/Kernel level (`sysctls`).
  - **When**: During the move from development to production or when scaling up to handle higher traffic.
  - **Why**: To prevent resource bottleneck issues like **Throttling** or **OOMKilled**, and to ensure the most efficient use of infrastructure.
  - **How**:
    - **Resource Tuning**: Refining `requests` and `limits`.
    - **Kernel Tuning**: Using `securityContext.sysctls` for network/file system tweaks.
    - **App Tuning**: Adjusting thread pools or memory heaps (e.g., `-Xmx` for Java).
- **vi**:
  - **What (Cái gì)**: Quá trình điều chỉnh các giá trị cấu hình (CPU/RAM, giới hạn Kernel, tham số ứng dụng) để tối ưu hóa hiệu năng, chi phí và độ tin cậy.
  - **Who (Ai)**: Thực hiện bởi kỹ sư DevOps hoặc SRE dựa trên dữ liệu giám sát (metrics) và kiểm thử chịu tải (load test).
  - **Where (Ở đâu)**: Có thể áp dụng ở cấp độ Pod (`resources`, `env`), cấp độ Ứng dụng (ConfigMaps), hoặc cấp độ Node/Kernel (`sysctls`).
  - **When (Khi nào)**: Thường diễn ra khi chuyển từ môi trường phát triển sang production hoặc khi cần mở rộng hệ thống để chịu tải cao hơn.
  - **Why (Tại sao)**: Để ngăn chặn các điểm nghẽn tài nguyên như **Throttling** hoặc **OOMKilled**, và đảm bảo sử dụng hạ tầng hiệu quả nhất.
  - **How (Như thế nào)**:
    - **Tinh chỉnh tài nguyên**: Điều chỉnh chính xác `requests` và `limits`.
    - **Tinh chỉnh Kernel**: Sử dụng `securityContext.sysctls` cho các tùy chỉnh về mạng/hệ thống tệp.
    - **Tinh chỉnh App**: Điều chỉnh thread pools hoặc bộ nhớ heap (ví dụ: `-Xmx` cho Java).


## Resource Quotas
- **en**:
  - **What**: A tool to provide constraints that limit aggregate resource consumption per Namespace (e.g., total CPU, Memory, or number of Pods).
  - **Where**: Applied within a specific **Namespace**.
  - **When**: Use when multiple teams or projects share the same cluster to prevent one team from consuming all available resources (Noisy Neighbor problem).
  - **Why**: To ensure fair resource distribution across the cluster and to manage costs and capacity efficiently.
  - **How**: Defined in a YAML file as a `ResourceQuota` object and applied to a namespace. If a request exceeds the quota, the Kubernetes API server will reject the creation of the resource.
- **vi**:
  - **What (Cái gì)**: Một công cụ cung cấp các ràng buộc nhằm giới hạn tổng mức tiêu thụ tài nguyên trên mỗi Namespace (ví dụ: tổng CPU, Memory, hoặc số lượng Pod).
  - **Where (Ở đâu)**: Được áp dụng bên trong một **Namespace** cụ thể.
  - **When (Khi nào)**: Sử dụng khi có nhiều nhóm hoặc dự án dùng chung một cụm (cluster) để ngăn chặn một nhóm tiêu thụ hết tất cả tài nguyên có sẵn (vấn đề "Noisy Neighbor").
  - **Why (Tại sao)**: Để đảm bảo phân phối tài nguyên công bằng trong cụm và quản lý chi phí cũng như dung lượng một cách hiệu quả.
  - **How (Như thế nào)**: Được định nghĩa trong tệp YAML dưới dạng đối tượng `ResourceQuota` và áp dụng cho một namespace. Nếu một yêu cầu vượt quá hạn ngạch, API server của Kubernetes sẽ từ chối việc tạo tài nguyên đó.

## Stateful Apps and Stateless Apps
- **en**:
  - **What**: **Stateless Apps** do not store client data from one session to use in the next (e.g., Nginx, web frontends). **Stateful Apps** require the system to remember previous interactions and store persistent data (e.g., Databases like PostgreSQL, Redis, MongoDB).
  - **Where**: Managed in Kubernetes using **Deployments** (Stateless) and **StatefulSets** (Stateful).
  - **When**: Use **Stateless** for applications that can be easily scaled up or down without worry about data loss. Use **Stateful** for applications that require stable network identities or persistent storage across restarts.
  - **Why**: To distinguish between apps that are interchangeable (Stateless) and those that are unique/dependent on history (Stateful), allowing for proper resource management and storage strategy.
  - **How**: Stateless apps are scaled by increasing replica counts in a Deployment. Stateful apps use **StatefulSets** which provide stable hostnames (pod-0, pod-1) and link each pod to its own **PersistentVolume**.
- **vi**:
  - **What (Cái gì)**: **Stateless Apps** không lưu trữ dữ liệu của người dùng từ phiên này để sử dụng cho phiên sau (ví dụ: Nginx, web frontend). **Stateful Apps** yêu cầu hệ thống phải nhớ các tương tác trước đó và lưu trữ dữ liệu bền vững (ví dụ: Cơ sở dữ liệu như PostgreSQL, Redis, MongoDB).
  - **Where (Ở đâu)**: Được quản lý trong Kubernetes bằng **Deployments** (cho Stateless) và **StatefulSets** (cho Stateful).
  - **When (Khi nào)**: Sử dụng **Stateless** cho các ứng dụng có thể dễ dàng mở rộng hoặc thu hẹp mà không lo mất dữ liệu. Sử dụng **Stateful** cho các ứng dụng yêu cầu định danh mạng ổn định hoặc bộ nhớ lưu trữ bền vững qua các lần khởi động lại.
  - **Why (Tại sao)**: Để phân biệt giữa các ứng dụng có thể thay thế lẫn nhau (Stateless) và những ứng dụng là duy nhất/phụ thuộc vào lịch sử dữ liệu (Stateful), từ đó có chiến lược quản lý tài nguyên và lưu trữ phù hợp.
  - **How (Như thế nào)**: Các ứng dụng Stateless được mở rộng bằng cách tăng số lượng bản sao trong Deployment. Các ứng dụng Stateful sử dụng **StatefulSet** cung cấp hostname ổn định (pod-0, pod-1) và liên kết mỗi pod với một **PersistentVolume** riêng.


## Patterns

### Sidecar Pattern

- **en**:
  - **What**: A design pattern where a secondary container (the sidecar) is deployed alongside the main application container within the same Pod.
  - **Where**: Implemented within a Kubernetes Pod, where both containers share the same lifecycle, network namespace, and storage volumes.
  - **Why**: To extend or enhance the functionality of the main application without modifying its code (e.g., logging, monitoring, proxying).
  - **How**: Defined in the Pod specification under the `containers` array, with shared volumes for data exchange if needed.

- **vi**:
  - **What (Cái gì)**: Một mẫu thiết kế trong đó một container phụ (sidecar) được triển khai cùng với container ứng dụng chính trong cùng một Pod.
  - **Where (Ở đâu)**: Được triển khai bên trong một Kubernetes Pod, nơi cả hai container chia sẻ cùng vòng đời, không gian mạng (network namespace) và các ổ đĩa lưu trữ (volumes).
  - **Why (Tại sao)**: Để mở rộng hoặc tăng cường chức năng của ứng dụng chính mà không cần sửa đổi mã nguồn của nó (ví dụ: thu thập log, giám sát, proxy).
  - **How (Như thế nào)**: Được định nghĩa trong đặc tả Pod bên dưới mảng `containers`, sử dụng chung volumes để trao đổi dữ liệu nếu cần.

### Adapter Pattern

- **en**:
  - **What**: A pattern that standardizes and transforms the output of the main application container to match a specific external format.
  - **Where**: Part of a multi-container Pod, acting as an intermediate layer between the application and external systems like monitoring tools.
  - **Why**: To ensure compatibility with unified monitoring or logging systems when the application itself produces non-standard output.
  - **How**: The adapter container reads data from the main container (e.g., via a shared volume or local API) and serves it in the required format (e.g., Prometheus metrics).

- **vi**:
  - **What (Cái gì)**: Một mẫu thiết kế giúp tiêu chuẩn hóa và chuyển đổi đầu ra của container ứng dụng chính để phù hợp với một định dạng bên ngoài cụ thể.
  - **Where (Ở đâu)**: Là một phần của Pod đa container, đóng vai trò là lớp trung gian giữa ứng dụng và các hệ thống bên ngoài như công cụ giám sát.
  - **Why (Tại sao)**: Để đảm bảo khả năng tương thích với các hệ thống giám sát hoặc ghi log tập trung khi bản thân ứng dụng tạo ra đầu ra không chuẩn.
  - **How (Như thế nào)**: Container adapter đọc dữ liệu từ container chính (ví dụ: qua volume dùng chung hoặc API nội bộ) và cung cấp nó dưới định dạng yêu cầu (ví dụ: Prometheus metrics).

### Ambassador Pattern

- **en**:
  - **What**: A pattern where a container acts as a proxy for the main application to handle external communications.
  - **Where**: Deployed within the same Pod as the application, representing the network interface for outbound or inbound traffic.
  - **Why**: To simplify how the application connects to external services (e.g., database sharding, circuit breaking, service discovery).
  - **How**: The application connects to `localhost` on a specific port, and the ambassador container routes that traffic to the appropriate external destination.

- **vi**:
  - **What (Cái gì)**: Một mẫu thiết kế trong đó một container đóng vai trò là proxy cho ứng dụng chính để xử lý các giao tiếp bên ngoài.
  - **Where (Ở đâu)**: Được triển khai trong cùng một Pod với ứng dụng, đại diện cho giao diện mạng cho lưu lượng truy cập ra ngoài hoặc vào trong.
  - **Why (Tại sao)**: Để đơn giản hóa cách ứng dụng kết nối với các dịch vụ bên ngoài (ví dụ: phân mảnh cơ sở dữ liệu - sharding, ngắt mạch - circuit breaking, phát hiện dịch vụ - service discovery).
  - **How (Như thế nào)**: Ứng dụng kết nối tới `localhost` trên một cổng cụ thể, và container ambassador sẽ điều phối lưu lượng đó đến đích bên ngoài phù hợp.


# Troubleshooting & Common Errors

## OOMKilled
- **en**:
  - **What**: Stands for "Out Of Memory Killed" (Exit Code 137). It means the container was terminated because it exceeded its memory limit or the node ran out of RAM.
  - **Who**: Triggered by the Linux Kernel's OOM Killer or the Kubernetes container runtime.
  - **Where**: Monitored at the Node level and reported in the Pod status.
  - **When**: Occurs when an application has a memory leak, is under heavy load, or is assigned insufficient resources.
  - **Why**: To prevent a single container from crashing the entire host node by consuming all available memory.
  - **How to Fix**: Increase `resources.limits.memory` in the YAML, optimize application memory usage, or add more nodes to the cluster.
- **vi**:
  - **What (Cái gì)**: Viết tắt của "Out Of Memory Killed" (Mã thoát 137). Nghĩa là container bị buộc dừng vì sử dụng vượt quá giới hạn RAM cho phép hoặc Node bị hết RAM.
  - **Who (Ai)**: Được kích hoạt bởi OOM Killer của nhân Linux hoặc bộ điều phối container của Kubernetes.
  - **Where (Ở đâu)**: Được giám sát ở cấp độ Node và báo cáo trong trạng thái của Pod.
  - **When (Khi nào)**: Xảy ra khi ứng dụng bị rò rỉ bộ nhớ (memory leak), đang chịu tải quá cao, hoặc được cấp phát quá ít tài nguyên.
  - **Why (Tại sao)**: Để ngăn chặn một container đơn lẻ làm sập toàn bộ máy host bằng cách chiếm dụng hết bộ nhớ còn lại.
  - **How to Fix (Cách khắc phục)**: Tăng `resources.limits.memory` trong tệp YAML, tối ưu hóa việc sử dụng RAM của ứng dụng, hoặc thêm Node mới vào cluster.


## CrashLoopBackOff
- **en**:
  - **What**: A status indicating a container is failing repeatedly and Kubernetes is waiting for an increasing amount of time before restarting it.
  - **The "BackOff"**: An exponential delay (10s, 20s, 40s... up to 5 mins) to prevent overloading the system with restart attempts.
  - **Why**: Typically caused by application bugs, missing configurations (ConfigMaps/Secrets), OOMKilled events, or port conflicts.
  - **How to Fix**: Check logs using `kubectl logs <pod-name>` or events using `kubectl describe pod <pod-name>` to identify the root cause inside the application.
- **vi**:
  - **What (Cái gì)**: Trạng thái báo hiệu container bị lỗi liên tục và Kubernetes đang trì hoãn việc khởi động lại nó trong một khoảng thời gian tăng dần.
  - **Phần "BackOff"**: Thời gian chờ tăng theo cấp số nhân (10s, 20s, 40s... tối đa 5 phút) để tránh làm quá tải hệ thống bởi các lần khởi động lại liên tục.
  - **Why (Tại sao)**: Thường do lỗi code, thiếu tệp cấu hình (ConfigMaps/Secrets), do bị OOMKilled, hoặc xung đột cổng kết nối (port).
  - **How to Fix (Cách khắc phục)**: Kiểm tra log bằng lệnh `kubectl logs <pod-name>` hoặc xem sự kiện bằng lệnh `kubectl describe pod <pod-name>` để xác định lỗi cụ thể bên trong ứng dụng.
 
+## Ingress Namespace Mismatch
+- **en**:
+  - **What**: A configuration error where the Ingress object cannot find its backend Services.
+  - **Why**: Ingress is a **Namespaced resource**. It can generally only route traffic to Services located in the same Namespace.
+  - **When**: Common when deploying an Ingress in `default` while Services are in a custom namespace (like `exam`).
+  - **Symptoms**: `kubectl describe ingress` shows `<error: endpoints "..." not found>`.
+  - **How to Fix**: Redeploy the Ingress in the same Namespace as your Services using `metadata.namespace: <your-namespace>`.
+- **vi**:
+  - **What (Cái gì)**: Lỗi cấu hình khi đối tượng Ingress không thể tìm thấy các Service xử lý bên dưới.
+  - **Why (Tại sao)**: Ingress là một **tài nguyên theo Namespace**. Thông thường, nó chỉ có thể điều hướng traffic tới các Service nằm trong cùng một Namespace với nó.
+  - **When (Khi nào)**: Thường gặp khi tạo Ingress ở namespace `default` nhưng Service lại nằm ở một namespace tùy chỉnh (như `exam`).
+  - **Symptoms (Dấu hiệu)**: Lệnh `kubectl describe ingress` báo lỗi `<error: endpoints "..." not found>`.
+  - **How to Fix (Cách khắc phục)**: Triển khai lại Ingress trong cùng Namespace với Service bằng cách thêm `metadata.namespace: <your-namespace>`.
 
+ 

+**Example Error Output**:
+```bash
+PS D:\devops\dev-devops-exp> kubectl describe ingress demo-ingress
+Name:             demo-ingress
+Namespace:        default
+Rules:
+  Host        Path  Backends
+  ----        ----  --------
+  *
+              /nginx   nginx-service:80 (<error: endpoints "nginx-service" not found>)
+              /httpd   httpd-service:80 (<error: endpoints "httpd-service" not found>)
+```


# CLIs

-`kubectl config view`
```bash
PS D:\devops\dev-devops-exp> kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority: C:\Users\BALE\.minikube\ca.crt
    extensions:
    - extension:
        last-update: Wed, 21 Jan 2026 22:58:34 +07
        provider: minikube.sigs.k8s.io
        version: v1.37.0
      name: cluster_info
    server: https://127.0.0.1:53768
  name: minikube
contexts:
- context:
    cluster: minikube
    extensions:
    - extension:
        last-update: Wed, 21 Jan 2026 22:58:34 +07
        provider: minikube.sigs.k8s.io
        version: v1.37.0
      name: context_info
    namespace: default
    user: minikube
  name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
- name: minikube
  user:
    client-certificate: C:\Users\BALE\.minikube\profiles\minikube\client.crt
    client-key: C:\Users\BALE\.minikube\profiles\minikube\client.key
```

`kubectl get pods -A -o wide`
```bash
NAMESPACE              NAME                                         READY   STATUS    RESTARTS      AGE   IP             NODE       NOMINATED NODE   READINESS GATES
default                my-dep-b458fdbb4-9hzph                       1/1     Running   1 (26d ago)   29d   10.244.0.11    minikube   <none>           <none>
kube-system            coredns-66bc5c9577-ms27t                     1/1     Running   1 (26d ago)   30d   10.244.0.13    minikube   <none>           <none>
kube-system            etcd-minikube                                1/1     Running   1 (26d ago)   30d   192.168.49.2   minikube   <none>           <none>
kube-system            kube-apiserver-minikube                      1/1     Running   1 (24h ago)   30d   192.168.49.2   minikube   <none>           <none>
kube-system            kube-controller-manager-minikube             1/1     Running   1 (26d ago)   30d   192.168.49.2   minikube   <none>           <none>
kube-system            kube-proxy-dwb5p                             1/1     Running   1 (26d ago)   30d   192.168.49.2   minikube   <none>           <none>
kube-system            kube-scheduler-minikube                      1/1     Running   1 (26d ago)   30d   192.168.49.2   minikube   <none>           <none>
kube-system            storage-provisioner                          1/1     Running   3 (24h ago)   30d   192.168.49.2   minikube   <none>           <none>
kubernetes-dashboard   dashboard-metrics-scraper-77bf4d6c4c-wpn6h   1/1     Running   1 (26d ago)   30d   10.244.0.12    minikube   <none>           <none>
kubernetes-dashboard   kubernetes-dashboard-855c9754f9-99cmn        1/1     Running   2 (24h ago)   30d   10.244.0.14    minikube   <none>           <none>
```

```bash
PS D:\devops\dev-devops-exp> kubectl describe pod my-dep-b458fdbb4-9hzph
Name:             my-dep-b458fdbb4-9hzph
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Wed, 24 Dec 2025 14:16:10 +0700
Labels:           app=my-dep
                  pod-template-hash=b458fdbb4
Annotations:      <none>
Status:           Running
IP:               10.244.0.11
IPs:
  IP:           10.244.0.11
Controlled By:  ReplicaSet/my-dep-b458fdbb4
Containers:
  nginx:
    Container ID:   docker://c367deff3816c069cd39c2955c6ff2417245fe8c5cb004cf390ca0801d3809d2
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:c881927c4077710ac4b1da63b83aa163937fb47457950c267d92f7e4dedf4aec
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 21 Jan 2026 22:59:04 +0700
    Last State:     Terminated
      Reason:       Completed
      Exit Code:    0
      Started:      Wed, 24 Dec 2025 14:16:14 +0700
      Finished:     Sat, 27 Dec 2025 02:36:54 +0700
    Ready:          True
    Restart Count:  1
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-smwkq (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-smwkq:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:                      <none>
```

`kubectl get nodes`
```bash
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   30d   v1.34.0
```

`kubectl get configmap`
```bash
NAME               DATA   AGE
kube-root-ca.crt   1      30d
my-cm              2      82m
my-configmap       3      59m
```

`kubectl get secret`
```bash
NAME        TYPE     DATA   AGE
my-secret   Opaque   3      45m
```


`PS D:\devops\dev-devops-exp> `kubectl describe cm my-cm`

```bash
Name:         my-cm
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
key2:
----
value2
key1:
----
value1

BinaryData
====

Events:  <none>
```

`kubectl describe secret my-secret`

```bash
Name:         my-secret
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
api-key:   7 bytes
password:  11 bytes
username:  5 bytes
```


`kubectl describe deployment my-deployment`

```bash
Name:                   my-deployment
Namespace:              default
CreationTimestamp:      Sat, 24 Jan 2026 12:43:17 +0700
Labels:                 <none>
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=myapp
Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        10
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=myapp
  Containers:
   nginx:
    Image:         nginx:1.14
    Port:          <none>
    Host Port:     <none>
    Environment:   <none>
    Mounts:        <none>
  Volumes:         <none>
  Node-Selectors:  <none>
  Tolerations:     <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  my-rs (0/0 replicas created)
NewReplicaSet:   my-deployment-5486565dbf (3/3 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  74s   deployment-controller  Scaled up replica set my-deployment-5486565dbf from 0 to 1
  Normal  ScalingReplicaSet  63s   deployment-controller  Scaled down replica set my-rs from 3 to 2
  Normal  ScalingReplicaSet  63s   deployment-controller  Scaled up replica set my-deployment-5486565dbf from 1 to 2
  Normal  ScalingReplicaSet  52s   deployment-controller  Scaled down replica set my-rs from 2 to 1
  Normal  ScalingReplicaSet  52s   deployment-controller  Scaled up replica set my-deployment-5486565dbf from 2 to 3
  Normal  ScalingReplicaSet  40s   deployment-controller  Scaled down replica set my-rs from 1 to 0
```


```bash
PS D:\devops\dev-devops-exp> kubectl rollout status deployment/my-deployment
deployment "my-deployment" successfully rolled out
PS D:\devops\dev-devops-exp> kubectl set image deployment/my-deployment nginx=nginx:1.16
deployment.apps/my-deployment image updated
PS D:\devops\dev-devops-exp> kubectl rollout status deployment/my-deployment
Waiting for deployment "my-deployment" rollout to finish: 3 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 3 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 3 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 3 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 3 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 4 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 4 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 4 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 4 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 4 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 4 out of 5 new replicas have been updated...
Waiting for deployment "my-deployment" rollout to finish: 2 old replicas are pending termination...
Waiting for deployment "my-deployment" rollout to finish: 2 old replicas are pending termination...
Waiting for deployment "my-deployment" rollout to finish: 2 old replicas are pending termination...
Waiting for deployment "my-deployment" rollout to finish: 2 old replicas are pending termination...
Waiting for deployment "my-deployment" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "my-deployment" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "my-deployment" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "my-deployment" rollout to finish: 4 of 5 updated replicas are available...
deployment "my-deployment" successfully rolled out
PS D:\devops\dev-devops-exp> kubectl rollout history deployment/my-deployment                                     
deployment.apps/my-deployment 
REVISION  CHANGE-CAUSE
0         <none>
1         <none>
2         <none>

PS D:\devops\dev-devops-exp> kubectl rollout undo deployment/my-deployment
deployment.apps/my-deployment rolled back
```

### Useful CLI Flags & PowerShell Tips

- **The Watch Flag (`-w` / `--watch`)**:
  - **en**: Keeps the command open and streams changes in real-time. Useful for monitoring state transitions (e.g., `ContainerCreating` -> `Running`).
  - **vi**: Giữ lệnh luôn mở và cập nhật thay đổi theo thời gian thực. Hữu ích để theo dõi quá trình chuyển trạng thái của Pod.
  - **Example**: `kubectl get pods -w`

- **PowerShell Filtering (`Select-String`)**:
  - **en**: Use `Select-String` instead of `grep` on Windows PowerShell to filter output.
  - **vi**: Sử dụng `Select-String` thay cho `grep` trên Windows PowerShell để lọc dữ liệu đầu ra.
  - **Example**: `kubectl get events | Select-String "my-pod"`

- **Interactive Exec (`kubectl exec -it`)**:
  - **en**: Access a container's shell environment.
    - `-i` (stdin): Keep stdin open even if not attached.
    - `-t` (tty): Allocate a pseudo-TTY (interactive terminal).
  - **vi**: Truy cập vào môi trường shell của container.
    - `-i`: Giữ đầu vào (stdin) luôn mở.
    - `-t`: Cấp phát một terminal ảo để tương tác.
  - **Example**: `kubectl exec -it <pod-name> -- /bin/sh`

- **Testing Internal Connectivity (`kubectl run`)**:
  - **en**: Run a temporary Pod to test network access to other Services using internal DNS names.
    - `--rm`: Automatically deletes the Pod after it exits.
    - `-it`: Runs in interactive mode.
    - `--restart=Never`: Ensures it's a single Pod, not a controller (like Deployment).
    - `--`: Separates kubectl flags from the container's command.
    - `sh -c "..."`: Runs a shell command inside the container.
  - **vi**: Chạy một Pod tạm thời để kiểm tra kết nối mạng tới các Service khác bằng tên DNS nội bộ.
    - `--rm`: Tự động xóa Pod sau khi thoát.
    - `-it`: Chạy ở chế độ tương tác.
    - `--restart=Never`: Đảm bảo nó là Pod đơn lẻ, không phải controller.
    - `--`: Ngăn cách các cờ của kubectl với câu lệnh bên trong container.
    - `sh -c "..."`: Chạy một câu lệnh shell bên trong container.
  - **Example & Response**:
    ```powershell
    PS D:\devops\dev-devops-exp> kubectl run test-pod --image=busybox --rm -it --restart=Never -- sh -c "wget -qO- http://nginx-service-yaml:8080"
    <!DOCTYPE html>
    <html>
    <head>
    <title>Welcome to nginx!</title>
    ...
    <h1>Welcome to nginx!</h1>
    ...
    </html>
    pod "test-pod" deleted
    ```

- **Resource Inspection (Describe vs YAML)**:
  - **en**:
    - **Describe**: Use `kubectl describe <type> <name>` to see human-readable details, status, and **Events** (best for troubleshooting).
    - **Export YAML**: Use `kubectl get <type> <name> -o yaml` to see the full, raw configuration (best for auditing or cloning).
  - **vi**:
    - **Describe (Mô tả)**: Sử dụng `kubectl describe <type> <name>` để xem chi tiết, trạng thái và các **Sự kiện (Events)** của tài nguyên (tốt nhất để tìm lỗi).
    - **Xuất YAML**: Sử dụng `kubectl get <type> <name> -o yaml` để xem toàn bộ cấu hình thô của tài nguyên (tốt nhất để kiểm tra cấu hình hoặc sao chép).
  - **Example**:
    - `kubectl describe deployment nginx-app`
    - `kubectl get deployment nginx-app -o yaml`
    - `kubectl describe svc nginx-service-yaml`
    - `kubectl get svc nginx-service-yaml -o yaml`
  - Example response:
    ```yaml
    PS D:\devops\dev-devops-exp> kubectl get deployment nginx-app -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"name":"nginx-app","namespace":"default"},"spec":{"replicas":3,"selector":{"matchLabels":{"app":"nginx"}},"template":{"metadata":{"labels":{"app":"nginx"}},"spec":{"containers":[{"image":"nginx:alpine","name":"nginx","ports":[{"containerPort":80}]}]}}}}
  creationTimestamp: "2026-01-26T05:14:15Z"
  generation: 1
  name: nginx-app
  namespace: default
  resourceVersion: "526485"
  uid: 98a1949c-7e4b-4c87-98a7-ed9c98a04943
spec:
  progressDeadlineSeconds: 600
  replicas: 3
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: nginx
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - image: nginx:alpine
        imagePullPolicy: IfNotPresent
        name: nginx
        ports:
        - containerPort: 80
          protocol: TCP
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  availableReplicas: 3
  conditions:
  - lastTransitionTime: "2026-01-26T05:14:38Z"
    lastUpdateTime: "2026-01-26T05:14:38Z"
    message: Deployment has minimum availability.
    reason: MinimumReplicasAvailable
    status: "True"
    type: Available
  - lastTransitionTime: "2026-01-26T05:14:15Z"
    lastUpdateTime: "2026-01-26T05:14:38Z"
    message: ReplicaSet "nginx-app-54fc99c8d" has successfully progressed.
    reason: NewReplicaSetAvailable
    status: "True"
    type: Progressing
  observedGeneration: 1
  readyReplicas: 3
  replicas: 3
  updatedReplicas: 3
    ```

  - Example Service response:
    ```yaml
    PS D:\devops\dev-devops-exp> kubectl get svc nginx-service-yaml -o yaml
apiVersion: v1
kind: Service
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"name":"nginx-service-yaml","namespace":"default"},"spec":{"ports":[{"port":8080,"protocol":"TCP","targetPort":80}],"selector":{"app":"nginx"},"type":"ClusterIP"}}
  creationTimestamp: "2026-01-26T05:38:44Z"
  name: nginx-service-yaml
  namespace: default
  resourceVersion: "527660"
  uid: ac735cff-83e3-4b8b-be77-71a2d73610ef
spec:
  clusterIP: 10.101.153.115
  clusterIPs:
  - 10.101.153.115
  internalTrafficPolicy: Cluster
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - port: 8080
    protocol: TCP
    targetPort: 80
  selector:
    app: nginx
  sessionAffinity: None
  type: ClusterIP
status:
  loadBalancer: {}
    ```

### Local Access (Windows Docker Driver)
- **en**:
  - **Issue**: When using the Docker driver on Windows, `localhost:<NodePort>` doesn't work directly because the Cluster runs inside a container.
  - **Option 1 (Minikube Tunnel)**: Use `minikube service <name> --url`. It creates a bridge and provides a temporary `127.0.0.1:xxxxx` URL.
  - **Option 2 (Port-Forwarding)**: Use `kubectl port-forward service/<name> <local_port>:<svc_port>`. This is stable and works on any cluster.
- **vi**:
  - **Vấn đề**: Khi dùng Docker driver trên Windows, `localhost:<NodePort>` không hoạt động trực tiếp do Cluster chạy trong một container.
  - **Cách 1 (Minikube Tunnel)**: Dùng `minikube service <name> --url`. Nó tạo một cầu nối và cung cấp một đường dẫn `127.0.0.1:xxxxx` tạm thời.
  - **Cách 2 (Port-Forwarding)**: Dùng `kubectl port-forward service/<name> <local_port>:<svc_port>`. Cách này ổn định và hoạt động trên mọi cluster.
- **Examples**:
  - `minikube service nginx-nodeport --url`
  - `kubectl port-forward service/nginx-nodeport 8081:80`

> **Note on Dynamic Ports (Windows/Docker Tunneling)**:
> - **en**: On Windows with the Docker driver, the Minikube node IP (e.g., `192.168.49.2`) is isolated. When you run `minikube service <name> --url`, it creates a tunnel to your localhost (`127.0.0.1`) on a random available port. This port acts as a bridge to the actual `nodePort` inside the cluster.
> - **vi**: Trên Windows dùng Docker driver, IP của Node Minikube (ví dụ: `192.168.49.2`) bị cô lập. Khi chạy `minikube service <name> --url`, nó tạo một tunnel tới localhost (`127.0.0.1`) tại một cổng ngẫu nhiên. Cổng này đóng vai trò là "cầu nối" tới cổng `nodePort` thực tế bên trong cluster.

### Load Balancing & Browser Persistence
- **en**:
  - **Issue**: When refreshing in a browser, you might always see the same Pod responding.
  - **Why**: Modern browsers use **HTTP Keep-Alive** to keep a TCP connection open for faster performance. Kubernetes load balances per *connection*, not per *request*. Since the connection is reused, the traffic stays on the same Pod.
  - **How to verify LB**: Use `curl` in a loop (which opens new connections) or open the link in an **Incognito** window.
- **vi**:
  - **Vấn đề**: Khi tải lại trang trên trình duyệt, bạn có thể thấy chỉ một Pod duy nhất phản hồi liên tục.
  - **Tại sao**: Các trình duyệt hiện đại dùng **HTTP Keep-Alive** để giữ kết nối TCP luôn mở nhằm tăng tốc độ. Kubernetes cân bằng tải theo mỗi *kết nối*, không phải theo mỗi *request*. Vì kết nối được dùng lại, traffic sẽ tiếp tục đi tới cùng một Pod.
  - **Cách kiểm tra LB**: Sử dụng vòng lặp `curl` (mỗi lần gọi là một kết nối mới) hoặc mở link trong cửa sổ **Ẩn danh**.

## Storage (Volumes)

### Ephemeral Storage: emptyDir
- **en**:
  - **What**: A temporary volume that is created when a Pod is assigned to a Node. It exists as long as the Pod is running.
  - **Why**: Used for sharing data between containers in the same Pod or for scratch space.
  - **Important**: Data is deleted when the Pod is deleted.
- **vi**:
  - **What (Cái gì)**: Ổ đĩa tạm thời gắn liền với vòng đời của Pod.
  - **Why (Tại sao)**: Dùng để chia sẻ dữ liệu giữa các container trong cùng 1 Pod hoặc làm bộ nhớ tạm.
  - **Lưu ý**: Dữ liệu mất hoàn toàn khi Pod bị xóa.

#### Lab: Shared emptyDir (Reader/Writer)
- **en**:
  - **Setup**: Container A (Writer) mounts `temp-vol` at `/output`. Container B (Reader) mounts `temp-vol` at `/input`.
  - **Result**: Writer writes to `/output/message.txt` $\rightarrow$ Reader can read from `/input/message.txt`.
  - **Key Insight**: Different **MountPaths** can point to the same **Volume** (USB analogy).
- **vi**:
  - **Thực hành**: Container A (Writer) gắn volume tại `/output`. Container B (Reader) gắn volume tại `/input`.
  - **Kết quả**: Writer ghi vào `/output/message.txt` $\rightarrow$ Reader có thể đọc từ `/input/message.txt`.
  - **Điểm mấu chốt**: Các **MountPath** khác nhau có thể cùng trỏ về một **Volume** duy nhất (Phép ẩn dụ về thẻ nhớ dùng chung).
+
+#### FAQ: Why use different MountPath names?
+- **en**:
+  - **Clarity**: It describes the container's logic (e.g., one container writes to `/output`, another reads from `/input`).
+  - **Collision Prevention**: Mounting at a common path like `/data` might hide original files inside the container image. Using custom names is safer.
+  - **Technical Note**: They **can** be the same, but using different names is a Best Practice for organization.
+- **vi**:
+  - **Sự rõ ràng**: Nó mô tả logic của container (ví dụ: một bên ghi vào `/output`, một bên đọc từ `/input`).
+  - **Tránh xung đột**: Gắn (mount) vào các đường dẫn chung như `/data` có thể làm ẩn đi các file có sẵn của container image. Dùng tên riêng biệt sẽ an toàn hơn.
+  - **Lưu ý kỹ thuật**: Chúng **có thể** giống nhau, nhưng dùng tên khác nhau là một Best Practice để tổ chức code tốt hơn.

+### Node Storage: hostPath
+- **en**:
+  - **What**: Mounts a file or directory from the host node's filesystem directly into your Pod.
+  - **Why**: Used for system-level tools that need access to node internals (e.g., reading logs in `/var/log`).
+  - **Warning**: It creates a security risk and makes your Pod "Node-Dependent" (if the Pod moves to another node, it won't see the same data).
+  - **Types**: `DirectoryOrCreate`, `FileOrCreate`, `Directory`, `File`, `Socket`, etc.
+- **vi**:
+  - **What (Cái gì)**: Gắn (mount) một tệp tin hoặc thư mục trực tiếp từ hệ thống tệp của máy chủ (Node) vào Pod của bạn.
+  - **Why (Tại sao)**: Dùng cho các công cụ hệ thống cần truy cập sâu vào Node (ví dụ: đọc log hệ thống tại `/var/log`).
+  - **Cảnh báo**: Nó tạo ra rủi ro bảo mật và làm cho Pod bị "Lệ thuộc vào Node" (nếu Pod chuyển sang máy khác, nó sẽ không thấy dữ liệu cũ).
+  - **Các loại (Types)**: `DirectoryOrCreate`, `FileOrCreate`, `Directory`, `File`, `Socket`, v.v.

+#### Detailed hostPath Types
+| Type | Description (en) | Mô tả (vi) |
+| :--- | :--- | :--- |
+| **`Directory`** | Must exist. Pod fails if missing. | Thư mục phải tồn tại. Lỗi nếu không tìm thấy. |
+| **`DirectoryOrCreate`** | Create if missing (0755). | Tự tạo thư mục nếu chưa có (quyền 0755). |
+| **`File`** | Must exist. | File phải tồn tại sẵn. |
+| **`FileOrCreate`** | Create if missing (0644). | Tự tạo file trống nếu chưa có (quyền 0644). |
+| **`Socket`** | UNIX socket must exist. | UNIX socket phải tồn tại sẵn. |
+| **`CharDevice`** | Character device (hardware). | File thiết bị dạng ký tự (phần cứng). |
+| **`BlockDevice`** | Block device (disk). | File thiết bị dạng khối (ổ đĩa). |
+
+### Volume Lifecycle Comparison
+- **en**:
+  - **emptyDir**: 
+    - **Persistence**: Transient (Temporary).
+    - **Lifecycle**: Tied to the Pod. Created when the Pod is scheduled; deleted when the Pod is removed from the node.
+    - **Survival**: Data survives container crashes/restarts, but NOT Pod deletion.
+  - **hostPath**:
+    - **Persistence**: External to the Pod.
+    - **Lifecycle**: Independent of the Pod. The data exists on the Node before the Pod starts and remains after the Pod is deleted.
+    - **Identity**: The data is linked to the **Node**, not the Cluster. If the Pod is moved to a new node, it cannot access the data from the old node.
+- **vi**:
+  - **emptyDir**: 
+    - **Tính bền vững**: Tạm thời.
+    - **Vòng đời**: Theo sát Pod. Được tạo khi Pod được lập lịch; bị xóa khi Pod bị gỡ bỏ khỏi node.
+    - **Khả năng sống sót**: Dữ liệu tồn tại được qua việc container bị crash/restart, nhưng KHÔNG sống được nếu Pod bị xóa.
+  - **hostPath**:
+    - **Tính bền vững**: Nằm ngoài Pod.
+    - **Vòng đời**: Độc lập với Pod. Dữ liệu tồn tại trên Node trước khi Pod chạy và vẫn còn đó sau khi Pod bị xóa.
+    - **Định danh**: Dữ liệu gắn liền với **Node**, không phải Cluster. Nếu Pod được chuyển sang node mới, nó sẽ không truy cập được dữ liệu từ node cũ.
+
+
+



## PersistentVolume (PV) and PersistentVolumeClaim (PVC)

### PersistentVolume (PV)
- **en**:
  - **What**: A piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes.
  - **Where**: It is a cluster-wide resource (not namespaced).
  - **Why**: To provide stable, persistent storage that exists independently of any individual Pod's lifecycle.
  - **How**: Defined in YAML with details like capacity, access modes, and the actual storage backend (NFS, Cloud Disk, etc.).
- **vi**:
  - **What (Cái gì)**: Một phần tài nguyên lưu trữ trong cụm đã được quản trị viên cấp phát hoặc được cấp phát động thông qua StorageClass.
  - **Where (Ở đâu)**: Là một tài nguyên ở cấp độ toàn cụm (không thuộc namespace cụ thể).
  - **Why (Tại sao)**: Cung cấp bộ nhớ ổn định và bền vững, tồn tại độc lập với vòng đời của bất kỳ Pod đơn lẻ nào.
  - **How (Như thế nào)**: Được định nghĩa trong tệp YAML với các chi tiết như dung lượng, chế độ truy cập và hạ tầng lưu trữ thực tế (NFS, Cloud Disk, v.v.).

### PersistentVolumeClaim (PVC)
- **en**:
  - **What**: A request for storage by a user (developer). It is similar to a Pod; while Pods consume node resources, PVCs consume PV resources.
  - **Where**: It is a Namespaced resource.
  - **Why**: To allow developers to request storage without needing to know the technical details of the underlying storage hardware.
  - **How**: A user creates a PVC specifying the size and access modes. Kubernetes coordinates the binding between the PVC and a matching PV.
- **vi**:
  - **What (Cái gì)**: Một yêu cầu sử dụng bộ nhớ từ người dùng (lập trình viên). Nó tương tự như Pod; nếu Pod tiêu thụ tài nguyên của Node thì PVC tiêu thụ tài nguyên của PV.
  - **Where (Ở đâu)**: Là một tài nguyên thuộc về một Namespace cụ thể.
  - **Why (Tại sao)**: Cho phép nhà phát triển yêu cầu bộ nhớ mà không cần biết chi tiết kỹ thuật về phần cứng lưu trữ bên dưới.
  - **How (Như thế nào)**: Người dùng tạo một PVC chỉ định kích thước và chế độ truy cập. Kubernetes sẽ điều phối việc ràng buộc giữa PVC và một PV phù hợp.


### Persistent Volumes (PV) & Persistent Volume Claims (PVC) Lifecycle
- **en**:
  - **What**: The lifecycle phases describe the various stages a PersistentVolume (PV) and a PersistentVolumeClaim (PVC) go through, from creation to deletion.
  - **Where**: Managed by the Kubernetes Control Plane (pv-controller).
  - **Why**: To provide a predictable way to manage storage resources, ensuring data persistence and proper resource cleanup.
  - **When**: Triggered by administrator actions (Static provisioning), user requests (PVC creation), or storage class configuration (Dynamic provisioning).
  - **How**: The interaction follows four main phases: **Provisioning**, **Binding**, **Using**, and **Reclaiming**.
- **vi**:
  - **What (Cái gì)**: Các giai đoạn vòng đời mô tả các bước mà PersistentVolume (PV) và PersistentVolumeClaim (PVC) trải qua, từ khi được tạo ra cho đến khi bị xóa bỏ.
  - **Where (Ở đâu)**: Được quản lý bởi Kubernetes Control Plane (thành phần pv-controller).
  - **Why (Tại sao)**: Để cung cấp một cách thức quản lý tài nguyên lưu trữ có thể dự đoán được, đảm bảo tính bền vững của dữ liệu và giải phóng tài nguyên đúng cách.
  - **When (Khi nào)**: Được kích hoạt bởi hành động của quản trị viên (cấp phát tĩnh), yêu cầu của người dùng (tạo PVC), hoặc cấu hình của storage class (cấp phát động).
  - **How (Như thế nào)**: Quá trình tương tác tuân theo bốn giai đoạn chính: **Provisioning**, **Binding**, **Using**, và **Reclaiming**.

#### Detailed Lifecycle Phases
| Phase | Description (en) | Mô tả (vi) |
| :--- | :--- | :--- |
| **1. Provisioning** | **Static**: Admin creates PV. **Dynamic**: StorageClass creates PV automatically when PVC is requested. | **Static**: Admin tạo PV thủ công. **Dynamic**: StorageClass tự động tạo PV khi có yêu cầu PVC. |
| **2. Binding** | The control plane matches a PVC to a suitable PV and binds them together (1-to-1 relationship). | Control plane tìm PV phù hợp cho PVC và ràng buộc chúng với nhau (quan hệ 1-1). |
| **3. Using** | Pods use the PVC as a volume. The cluster mounts the PV into the Pod. | Pod sử dụng PVC như một volume. Cluster sẽ gắn (mount) PV vào trong Pod. |
| **4. Reclaiming** | Defines what happens to the PV when the PVC is deleted. | Xác định điều gì xảy ra với PV khi PVC bị xóa. |

### Reclaim Policy
- **en**:
  - **What**: A policy that tells Kubernetes what to do with a PersistentVolume after it is released from its claim (PVC).
  - **Why**: To manage the automation of storage cleanup and ensure data security or persistence.
  - **Where**: Defined in the PersistentVolume (PV) spec or the StorageClass.
  - **How**: There are three main types: **Retain**, **Delete**, and **Recycle**.

- **vi**:
  - **What (Cái gì)**: Một chính sách cho Kubernetes biết phải làm gì với PersistentVolume sau khi nó được giải phóng khỏi yêu cầu sử dụng (PVC).
  - **Why (Tại sao)**: Để quản lý việc dọn dẹp bộ nhớ tự động và đảm bảo an toàn dữ liệu hoặc tính bền vững.
  - **Where (Ở đâu)**: Được định nghĩa trong thông số (spec) của PersistentVolume (PV) hoặc trong StorageClass.
  - **How (Như thế nào)**: Có ba loại chính: **Retain**, **Delete**, và **Recycle**.

#### Detailed Reclaim Policies Breakdown
| Policy | Behavior (en) | Hành vi (vi) |
| :--- | :--- | :--- |
| **Retain** | **Manual reclamation**: When the PVC is deleted, the PV still exists and the volume is considered "released". It must be manually cleaned up by an admin. | **Thu hồi thủ công**: Khi PVC bị xóa, PV vẫn tồn tại và volume được coi là "đã giải phóng". Quản trị viên phải tự dọn dẹp thủ công. |
| **Delete** | **Automatic reclamation**: When the PVC is deleted, Kubernetes automatically removes the PV object as well as the associated storage asset in the external infrastructure (e.g., AWS EBS, GCE PD). | **Thu hồi tự động**: Khi PVC bị xóa, Kubernetes tự động xóa đối tượng PV cũng như tài nguyên lưu trữ liên quan ở hạ tầng bên ngoài (ví dụ: AWS EBS, GCE PD). |
| **Recycle** | **Basic data scrubbing**: Performs a basic scrub (`rm -rf /thevolume/*`) and makes it available again for a new claim. | **Dọn dẹp dữ liệu cơ bản**: Thực hiện lệnh xóa cơ bản (`rm -rf /thevolume/*`) và cho phép PV sẵn sàng để một PVC khác sử dụng lại. |

> **Warning**: **Recycle** is deprecated. The recommended approach is to use Dynamic Provisioning with the **Delete** policy.

#### PV Status (Phases)
- **en**:
  - **Available**: Free resource, not yet bound.
  - **Bound**: Successfully linked to a PVC.
  - **Released**: PVC was deleted, but PV is not yet reclaimed.
  - **Failed**: Automated reclamation failed.
- **vi**:
  - **Available (Sẵn sàng)**: Tài nguyên rảnh, chưa bị ràng buộc.
  - **Bound (Đã buộc)**: Đã kết nối thành công với một PVC.
  - **Released (Đã giải phóng)**: PVC đã bị xóa, nhưng PV chưa được thu hồi.
  - **Failed (Lỗi)**: Quá trình thu hồi tự động gặp lỗi.

## StorageClass
- **en**:
  - **What**: A Kubernetes resource that acts as a "blueprint" or "template" for storage. it defines different "classes" of storage (e.g., fast SSD vs. cheap HDD).
  - **Why**: To enable **Dynamic Provisioning**. Instead of an admin manually creating PVs, the StorageClass automatically creates the PV when a user requests a PVC. This decouples developers from infrastructure details.
  - **Where**: A cluster-wide resource.
  - **When**: Triggered when a PVC is created that specifies a storageClassName.
  - **How**: It uses a **Provisioner** (a plugin like AWS EBS, Azure Disk, or GCE PD) and a set of **Parameters** to determine how the physical storage should be created.

- **vi**:
  - **What (Cái gì)**: Một tài nguyên trong Kubernetes đóng vai trò như một "bản thiết kế" hoặc "khuôn mẫu" cho bộ nhớ. Nó định nghĩa các loại bộ nhớ khác nhau (ví dụ: SSD tốc độ cao so với HDD giá rẻ).
  - **Why (Tại sao)**: Để cho phép **Cấp phát động (Dynamic Provisioning)**. Thay vì quản trị viên phải tạo PV thủ công, StorageClass sẽ tự động tạo PV khi người dùng yêu cầu một PVC. Điều này giúp tách biệt lập trình viên khỏi các chi tiết hạ tầng.
  - **Where (Ở đâu)**: Là một tài nguyên ở cấp độ toàn cụm (cluster-wide).
  - **When (Khi nào)**: Được kích hoạt khi một PVC được tạo ra và có chỉ định thuộc tính storageClassName.
  - **How (Như thế nào)**: Nó sử dụng một **Provisioner** (một plugin như AWS EBS, Azure Disk, hoặc GCE PD) và một bộ các **Parameters** (tham số) để quyết định cách bộ nhớ vật lý được tạo ra.

### Key StorageClass Parameters
| Parameter | Description (en) | Mô tả (vi) |
| :--- | :--- | :--- |
| **provisioner** | The internal or external volume plugin used to create the storage. | Plugin (nội bộ hoặc bên ngoài) được dùng để tạo ra bộ nhớ. |
| **reclaimPolicy** | What happens to the PV when the PVC is deleted (**Delete** or **Retain**). | Điều xảy ra với PV khi PVC bị xóa (**Delete** - Xóa hoặc **Retain** - Giữ lại). |
| **volumeBindingMode** | When the volume should be created (**Immediate** or **WaitForFirstConsumer**). | Thời điểm tạo volume (**Immediate** - Ngay lập tức hoặc **WaitForFirstConsumer** - Chờ Pod được gán vào Node). |
| **allowVolumeExpansion** | Whether the volume size can be increased after creation. | Cho phép tăng kích thước volume sau khi đã tạo hay không. |

> **Note**: If a PVC does not specify a storageClassName, it will use the **Default StorageClass** of the cluster (if configured).
