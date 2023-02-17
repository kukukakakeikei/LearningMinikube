# Learning Kubernetes  Architecture

<https://devopscube.com/cka-exam-study-guide/>

## Prerequisites

1. **Distributed（分布式） system**

   CAP**定理**（也称为 Brewer 定理）指出分布式数据库系统只能保证这三个特性中的两个：一致性、可用性和分区容错性。

### 一致性

   如果所有节点同时看到相同的数据，则称系统是一致的。

   简单地说，如果我们在一个一致的系统上执行读操作，它应该返回最近一次写操作的值。这意味着，读取应该导致所有节点返回相同的数据，即最近写入的值。

### 可用性

   分布式系统中的可用性可确保系统在 100% 的时间内保持运行。无论节点的个体状态如何，每个请求都会得到一个（非错误）响应。

   注意：这不能保证响应包含最新的写入。

   左图说明了一个“不可用”的系统。

### 分区容错

   这种情况表明系统不会失败，无论消息是否在系统中的节点之间被丢弃或延迟。

   在分布式系统中，分区容错性已成为一种必需品，而不是一种选择。通过跨节点和网络的组合充分复制记录，这成为可能。

2. **Authentication & Authorization**

3. **Key Value Store**:

4. **API**

5. **YAML**

6. **Container**

7. **Service Discovery**

8. **Networking Basis**

## Architecture

<https://devopscube.com/kubernetes-architecture-explained/>

1. **控制平面组件：**了解每个组件的作用，如 API 服务器、etcd、调度程序和控制器管理器。

   API-Server

   - **API 管理**：公开集群 API 端点并处理所有 API 请求。
   - **身份验证**（使用客户端证书、承载令牌和 HTTP 基本身份验证）和**授权**（ABAC 和 RBAC 评估）
   - 处理 API 请求并验证 API 对象（如 pod、服务等）的数据（验证和变更准入控制器）
   - 它是唯一与 etcd 通信的组件。
   - api-server 协调控制平面和工作节点组件之间的所有进程。

   Etcd

   - 强一致性、分布式、键值对存储

   - etcd 存储 Kubernetes 对象（pod、secrets、daemonsets、 deployments、configmaps、statefulsets 等）的所有配置、状态和元数据。
   - etcd 允许客户端使用 API 订阅事件Watch() 。Kubernetes api-server 使用 etcd 的监视功能来跟踪对象状态的变化。
   - etcd使用 gRPC公开键值 API 。此外，gRPC 网关是一个 RESTful 代理，可将所有 HTTP API 调用转换为 gRPC 消息。它使它成为 Kubernetes 的理想数据库。
   - etcd以key-value格式存储/registry目录key下的所有对象。例如，可以在/registry/pods/default/nginx下找到 default 命名空间中名为 Nginx 的 pod 的信息

​ kube-scheduler

​   调度程序的主要任务是识别创建请求并为创建请求选择最佳节点满足要求的pod。

​    Kube Controller Manager

1. **工作节点组件**：了解 Kube Proxy、Kubelet、Container Runtime

   kubelete kubeproxy Container Runtime

2. **插件组件：** CoreDNS、网络插件（Calico、weave 等）、Metric Server

3. **集群高可用性：**大多数组织使用托管 Kubernetes 服务（GKE、EKS、AKS 等）。因此，云提供商负责集群控制平面的高可用性。但是，了解在多区域和区域中扩展集群的高可用性概念非常重要。它将帮助您进行实时项目和 devops 面试。

4. **网络设计**：虽然在开放网络中不受限制地设置集群很容易，但在公司网络中却不是那么容易。作为 DevOps 工程师，您应该了解 Kubernetes 网络设计和要求，以便更好地**与网络团队协作**。例如，当我在谷歌云上使用 kubernetes 设置时，我们使用了一个在公司网络中不可路由的 CIDR pod 范围。作为解决方法，我们必须为 pod 网络部署 IP 伪装。

## Understand Kubeconfig File

<https://devopscube.com/kubernetes-kubeconfig-file/>
