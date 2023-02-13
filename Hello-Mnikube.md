# 搭建环境Ubuntu 22.04

1. Minikube start
   虚拟环境未设置开机启动Minikube，需要手动开启，开机自启设置参考如下
      创建systemd服务配置文件：
      bash
      Copy code
      sudo nano /etc/systemd/system/minikube.service
      将以下内容复制到配置文件中：
      makefile
      Copy code
      [Unit]
      Description=Minikube

      [Service]
      ExecStart=/usr/local/bin/minikube start
      ExecStop=/usr/local/bin/minikube stop
      Restart=always

      [Install]
      WantedBy=multi-user.target
      保存并退出配置文件。

      启用服务：
      Copy code
      sudo systemctl enable minikube
      重启系统，以验证Minikube虚拟机是否自动启动。

2. Minikube kubectl -- get po -A
   查看启动插件状态

3. Minikube dashboard
   启动系统自带的仪表盘

4. alias kubectel="minikube kubectl --"
   给命令设置别名

5. kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
   命令用于在Kubernetes集群中创建新部署，部署将在Kubernetes集群中运行kicbase/echo-server镜像的1.0版本。
   可以使用kubectl get deployments命令检查部署的状态，并使用kubectl describe deployment命令查看部署的详细信息。

6. kubectl expose deployment hello-minikube --type=NodePort --port=8080

   为镜像设置端口类型和端口号

   在kubectl expose命令中，--type选项用于指定服务的类型。下面是--type的可选模式：

   1. ClusterIP：该类型的服务仅在集群内部可见，并且具有一个固定的Cluster IP地址。
   2. NodePort：该类型的服务在集群内和集群外均可见，并且具有一个固定的Cluster IP地址和一个可用于访问服务的NodePort。
   3. LoadBalancer：该类型的服务在集群内和集群外均可见，并且具有一个外部负载均衡器，该负载均衡器为服务提供了一个公共IP地址。
   4. ExternalName：该类型的服务允许将一个外部域名映射到集群内的服务，但不会暴露该服务的内部实现。

   在使用kubectl expose命令时，请根据您的需求选择合适的类型。例如，如果您希望从外部访问您的服务，则可以选择NodePort或LoadBalancer类型。如果您希望仅在集群内部使用服务，则可以选择ClusterIP类型。

7.  kubectl get services hello-minikube

   查看服务状态

   "kubectl get services"是Kubernetes命令行工具中的一条命令，用于查看集群中的所有服务或指定服务的详细信息。该命令将返回一个表格，其中包含每个服务的名称、命名空间、Cluster IP地址、外部IP地址（如果存在）、端口等信息。

8.  minikube service hello-minikube

   minikube自行启动浏览器访问

9.  kubectl port-forward service/hello-minikube 7080:8080

   将8080端口转发到7080，使用localhost:7080访问

   "kubectl port-forward"是Kubernetes命令行工具中的一条命令，用于将本地主机的端口映射到集群中的某个pod的端口。这样，您可以使用本地主机的浏览器或命令行工具连接到运行在集群中的服务，而无需从集群外部访问。

10. 
