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
