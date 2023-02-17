# Learning Kubernetes  Architecture

<https://devopscube.com/cka-exam-study-guide/>

## ControlPlan

### 1. **Kube API-Server**

   支持http（127.0.0.1：8080）和https（6443）
   使用kubectl --v=8 get pods打开调试格式来查看每个API调用格式，其他日志级别如下：

      0：只输出命令执行的结果，不显示额外的信息。
      1：显示更详细的输出，包括HTTP请求和响应的基本信息。
      2：显示HTTP请求和响应的header和body信息。
      3：显示与API服务器的交互信息，包括API版本、对象
         类型、请求方法、请求路径等信息。
      4：显示REST客户端的行为，如URL构造、认证、缓存等
         信息。
      5：显示与API服务器交互的完整URL。
      6：显示每个请求的go-restful库调试信息。
      7：显示每个请求的HTTP客户端库调试信息。
      8：显示详细的调试信息，包括请求和响应的所有信
         息、 HTTP客户端库的调试信息以及Kubernetes命令
         行工具内部的一些状态信息等。
   使用kubectl api-versions

      命令用于显示Kubernetes API的版本信息。该命令会列出Kubernetes API的所有版本，以及它们的状态、资源组和API服务。
   使用kubectl api-resources --api-group=storage.k8s.io

      命令用于列出Kubernetes API服务器上可用的资源类型。使用该命令可以获取到所有可用的Kubernetes资源类型及其对应的短名称、API组、API版本等详细信息。这个命令可以帮助用户快速了解 Kubernetes 支持的所有 API 资源，并且可以帮助用户在使用 kubectl 时更快地查询和操作这些资源。
   通过/swaggerapi查看Swagger API

      使用--enable-swagger-ui=true可以通过/swagger-ui 访问Swagger UI
   通过/openapi/v2查看OpenAPI

      根据API可以生成各种语言的客户端访问API
   认证、授权和准入控制
   **认证**

      在 Kubernetes 中，kube-apiserver 启动时默认使用TLS（Transport Layer Security）加密与认证机制保护其通信安全。具体来说，kube-apiserver 默认使用TLS进行以下两种通信方式的加密与认证：

      HTTPS：用于保护 API 服务器的 RESTful API 服务，包括 API 对象的创建、查询和修改等操作。kube-apiserver 会在启动时生成一个自签名的 CA 根证书和一个 Server 证书，使用它们来实现 HTTPS 服务。同时，也支持使用外部颁发的证书和私钥来替换自签名证书，以增加信任度和安全性。认证成功后用户的username会传入授权机制模块，认证失败则返回HTTP401。API-Server对HTTP请求不做认证

      gRPC：用于保护 kubelet 和其他组件与 API 服务器之间的通信。在这种情况下，kube-apiserver 会生成一个自签名的 CA 根证书和一个 Server 证书，kubelet 和其他组件会使用这些证书来加密和认证与 kube-apiserver 的通信。

      为了确保安全性，Kubernetes 要求使用 TLS 加密所有的 API 请求，包括 kube-apiserver 对 etcd、kubelet 和其他组件的请求。同时，Kubernetes 还支持为集群中的每个用户或服务配置单独的证书和私钥，以实现更加精细的认证和授权策略。
   **授权**

      授权成功， 则用户的请求会发送到准入控制模块做进一步的请求验证； 而对于授权失败的请求则返回 HTTP 403.

   **准入控制**

      Kubernetes API Server Admission Control（准入控制）是 Kubernetes 的一项核心功能，用于对所有 API 请求进行处理，以确保请求的有效性和安全性。Admission Control 机制主要由两部分组成：准入控制器和准入 Webhook。

      准入控制器是 Kubernetes API Server 中的一个插件，用于对 API 请求进行预处理和过滤。它能够拦截并处理各种类型的 API 请求，例如 Pod、Service、ReplicationController、Deployment 等对象的创建、更新和删除请求，还能够进行权限验证、自动注入数据、自动扩展等处理。

         Kubernetes API Server Admission Control 支持多种类型的准入控制器，每个控制器都有自己的一组规则和处理逻辑。常见的准入控制器包括：

         NamespaceLifecycle：负责创建和删除 Namespace，并且可以在创建 Namespace 时自动注入标签和注释信息。

         LimitRanger：用于对容器和 Pod 等资源的使用进行限制和管理，以避免资源的滥用和浪费。

         ResourceQuota：允许对 Kubernetes 集群中的资源配额进行限制和管理，以确保每个 Namespace 和用户都能够得到足够的资源。

         ServiceAccount：用于自动创建和管理 Service Account，并且可以为不同的 Service Account 分配不同的权限和访问控制策略。

         PodSecurityPolicy：负责对 Pod 安全性进行审计和控制，以防止 Pod 的滥用和攻击。

      另一方面，准入 Webhook 是 Kubernetes API Server 的一种扩展机制，它允许管理员为 Kubernetes API Server 注册自定义的准入控制器。通过准入 Webhook，管理员可以将 API 请求转发到外部的 HTTP 服务中进行处理，实现更加灵活和强大的准入控制。准入 Webhook 可以用于访问控制、安全审计、自动化操作等方面。

      综上所述，Kubernetes API Server Admission Control 是 Kubernetes 中一项重要的安全机制，它通过准入控制器和准入 Webhook 来对 API 请求进行过滤和处理，保障 Kubernetes 集群的稳定性和安全性。
   **API-Server相关参数说明**
   
      kube-apiserver 是 Kubernetes API Server 组件，它提供了 Kubernetes API 的访问入口，负责处理所有来自客户端的 API 请求并将其转换为集群内部的操作。kube-apiserver 的启动参数非常丰富，包括以下几个方面：

      API Server 监听地址和端口
         --advertise-address：指定 kube-apiserver 广播给集群其他组件的 IP 地址。

         --bind-address：指定 kube-apiserver 监听的 IP 地址。

         --secure-port：指定 kube-apiserver 监听的安全端口，默认为 6443。

         --insecure-port：指定 kube-apiserver 监听的非安全端口，默认为 8080。

      证书和加密配置
         --tls-cert-file 和 --tls-private-key-file：指定 kube-apiserver 的证书和私钥文件，用于启用 HTTPS 通信协议。

         --client-ca-file：指定 kube-apiserver 的客户端 CA 证书文件，用于验证客户端请求的合法性。

         --etcd-cafile、--etcd-certfile 和 --etcd-keyfile：指定 kube-apiserver 与 etcd 通信时使用的证书和私钥文件。

      认证和授权配置
         --authentication-mode：指定 kube-apiserver 的认证模式，支持 Token、Basic、ClientCertificate、Webhook 等几种方式。

         --authorization-mode：指定 kube-apiserver 的授权模式，支持 ABAC、RBAC、Node、Webhook 等几种方式。

         --service-account-issuer、--service-account-signing-key-file 和 --service-account-api-audiences：用于配置 Service Account 和 Token 的签发者、签名密钥和接收者。

      API Server 的特殊行为
         --proxy-client-cert-file、--proxy-client-key-file 和 --proxy-ca-file：用于配置 kube-apiserver 代理访问客户端的证书和 CA 文件。

         --enable-admission-plugins 和 --disable-admission-plugins：用于启用或禁用各种 Admission Controller 插件。

         --audit-policy-file 和 --audit-log-path：用于配置审计策略和审计日志的路径。

      其他配置参数
         --allow-privileged、--disable-admission-plugins 和 --enable-admission-plugins：分别用于控制容器的权限、启用或禁用 Admission Controller 插件。

         --runtime-config：用于配置 Kubernetes API Server 的运行时参数，如 api/all、api/extensions 等。

         --tls-cipher-suites：指定 kube-apiserver 启用的 TLS 密码套件。
      访问控制相关参数
         --anonymous-auth：指定是否允许匿名用户访问 kube-apiserver，默认为 true。

         --tls-cert-file 和 --tls-private-key-file：指定 kube-apiserver 的证书和私钥文件，用于启用 HTTPS 通信协议。

      API Server 组件相关参数
         --etcd-servers：指定 kube-apiserver 与 etcd 的连接地址，默认为 http://127.0.0.1:2379。

         --kubelet-preferred-address-types：用于指定 kube-apiserver 与 kubelet 通信时使用的地址类型，默认为 [Hostname,InternalIP,ExternalIP]。

         --kubelet-client-certificate 和 --kubelet-client-key：用于配置 kube-apiserver 与 kubelet 通信时使用的客户端证书和私钥文件。

         --kubelet-certificate-authority：用于配置 kube-apiserver 与 kubelet 通信时使用的 CA 证书文件。

         --proxy-client-cert-file、--proxy-client-key-file 和 --proxy-ca-file：用于配置 kube-apiserver 代理访问客户端的证书和 CA 文件。

         --tls-cert-file 和 --tls-private-key-file：指定 kube-apiserver 的证书和私钥文件，用于启用 HTTPS 通信协议。

      高级配置参数
         --audit-log-maxage 和 --audit-log-maxbackup：用于配置审计日志的最大保留天数和最大备份数量。

         --disable-admission-plugins 和 --enable-admission-plugins：分别用于启用或禁用各种 Admission Controller 插件。

         --etcd-cafile、--etcd-certfile 和 --etcd-keyfile：指定 kube-apiserver 与 etcd 通信时使用的证书和私钥文件。

         --max-requests-inflight 和 --max-mutating-requests-inflight：用于配置 kube-apiserver 处理请求的并发限制。

         --storage-backend：用于指定 kube-apiserver 使用的数据存储后端，支持 etcd3 和 CRDB。

      以上是 kube-apiserver 的一部分参数，总结来看，kube-apiserver 的参数涉及到访问控制、API Server 组件、高级配置等方面，包括了证书和加密、认证和授权、API Server 特殊行为、其他配置参数等。管理员可以根据需要调整相应的参数。

### 2. **etcd**

### 3. **kube-scheduler**

### 4. **kube-controller-manager**

### 5. **cloud-controller-manager**
