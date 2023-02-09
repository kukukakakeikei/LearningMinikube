# 搭建环境Ubuntu 22.04

1. sudo apt-get update -y

   -y 命令指的是所有提问都是 ‘是’

2. sudo apt-get install ca-certificates curl gnupg lsb-release apt-transport-https -y

   **“ca-certificates”**是一个包，包含了各种证书颁发机构（CA）的根证书集合。这些根证书用于验证网站、电子邮件服务器和其他网络服务提供的SSL/TLS证书的真实性。

   通过安装“ca-certificates”包，您可以为系统提供一组受信任的根证书，这些证书可以由系统的证书存储、Web浏览器和其他需要证书验证的软件使用。这允许这些应用程序与远程服务器建立安全连接，并防止中间人攻击，以及其他安全优势。

   “ca-certificates”通常用于基于Unix的系统，例如Linux发行版和macOS，通常由“apt-get”、“yum”或“homebrew”等软件包管理器管理。

   

   **cURL**是一种开源的网络传输工具，用于在命令行中发送HTTP、FTP、SMTP等协议的请求，并获取服务器的响应。cURL支持多种数据传输格式，包括文本、图像和视频，并具有许多实用的特性，例如代理支持、认证、cookies和自动跟踪重定向。

   cURL通常用于自动化和脚本化Web服务，例如：从Web API获取数据、从FTP服务器下载文件、提交Web表单等。cURL是许多编程语言，包括C、PHP、Perl和Python等，都内置了对cURL的支持。

   

   GNU Privacy Guard（简称GNUPG或GPG）是一种开源的加密工具，它是一个用于数字签名、加密和解密文件的软件包。它是公开密钥加密的实现，允许您保护文件和电子邮件的隐私和完整性。

   Linux系统中安装的GNUPG通常用于对电子邮件和文件进行加密，以保护数据的隐私和完整性。它也可以用于数字签名，以确保文件的完整性和真实性。GNUPG可以通过一些软件包管理工具（如apt-get、yum等）在Linux系统上安装。

   

   **lsb-release**是一个命令行工具，用于在Linux系统上显示发行版信息。它读取系统中的/etc/lsb-release文件，并显示关于发行版名称、版本、代号名称等的信息。

   lsb-release主要用于在脚本或程序中确定系统发行版信息，以便进行特定于版本的操作。它常常与其他Linux服务器管理工具一起使用，以方便在不同发行版上执行标准操作。lsb-release通常是LSB（Linux Standard Base）软件包的一部分，并通过一些软件包管理工具（如apt-get、yum等）在Linux系统上安装。

   

   **apt-transport-https**是一个APT（Advanced Package Tool）传输方式，用于从HTTPS（Hypertext Transfer Protocol Secure）源下载软件包。它是APT软件包管理系统的一部分，用于在Debian和Ubuntu等Linux发行版中安装、升级和删除软件包。

   apt-transport-https提供了安全的软件包下载方式，可以防止软件包在下载过程中遭到篡改。它是通过HTTPS协议从远程服务器下载软件包，并使用证书进行身份验证。使用apt-transport-https可以确保软件包的安全性和完整性。它通常可以通过一些软件包管理工具（如apt-get、yum等）在Linux系统上安装。

3. sudo apt-get remove docker docker-engine docker.io containerd runc -y

   **runc**是Docker容器引擎的一部分，用于在容器中启动和管理进程。它是OCI（Open Container Initiative）规范的实现，与Docker容器一起使用，可以在Linux系统中创建、配置和管理容器。

   runc是一个命令行工具，用于执行容器的生命周期管理操作，如启动、停止、重启等。它通过创建一个独立的进程空间，以便在容器中执行应用程序和服务。runc与Docker镜像一起使用，以在Linux系统中创建轻量级的、可移植的容器。

   runc是Docker容器引擎的关键组件，用于在容器中运行应用程序和服务。它提供了一种安全、高效和可移植的容器运行环境，可以在多个平台和系统之间进行快速部署和管理。

   

   **Docker engine**是Docker的核心组件，用于构建、运行和管理Docker容器。它包含了所有用于创建、运行和管理容器的功能，例如Docker镜像管理、容器生命周期管理、网络管理等。

   Docker engine是Docker平台的基础，提供了一种简单、高效和可扩展的容器管理方式。它是一个开放源代码工具，支持多种操作系统，如Linux、macOS和Windows。通过使用Docker engine，开发人员可以更方便地部署、测试和管理应用程序，并实现快速迭代。

   

   **Docker.io**是一个Docker镜像仓库。它是一个存储Docker镜像的公共在线平台，可以用来从其中下载Docker镜像，并在本地计算机上使用。

   Docker镜像是一种二进制文件，包含了所有用于运行应用程序的代码、库、配置文件等。使用Docker.io的镜像仓库，开发人员可以快速访问和下载各种类型的Docker镜像，以便在本地使用。

   除了Docker.io，还有很多其他Docker镜像仓库可供选择，例如Docker Hub、Quay.io等。这些镜像仓库提供了不同的特性、工具和服务，可以根据需求选择合适的镜像仓库使用。

   

   **Containerd**是一个开源容器运行时，是Docker生态系统中的一个重要组件。它是用于管理容器生命周期的高性能和可靠的运行时，可以让开发人员在更低层次上控制容器的生命周期。

   Containerd提供了一个简单的API，可以让应用程序在后台处理容器的启动、停止、删除等生命周期操作，并管理容器的镜像和状态。它的核心特点是简单性和高性能，可以满足大多数应用程序的需求。

   在Docker生态系统中，Containerd与Docker引擎协同工作，为Docker容器提供生命周期管理功能，提高了Docker容器的可用性和稳定性。因此，Containerd是构建和部署容器化应用程序的重要工具。

   

   **容器运行时**是一个软件，可以在计算机系统上运行容器。它是容器技术的核心组件，负责管理容器的生命周期，包括容器的启动、停止、删除等。

   容器运行时利用了操作系统的容器技术，如Linux内核的namespaces和cgroups，为容器创建一个隔离的环境，以便容器中的应用程序可以独立于其他应用程序运行。容器运行时还管理容器的资源，如内存、CPU和网络，确保容器获得充足的资源以保证其正常运行。

   容器运行时是容器技术的基础，为开发人员提供了一种在容器环境中构建和部署应用程序的简便方法。它可以解决传统虚拟机技术存在的繁琐和资源浪费的问题，提高了容器技术的可用性和灵活性。因此，容器运行时是很多现代云计算和DevOps工具中不可或缺的组件。

4. curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

   "**curl -fssl"** 命令中的 "-fssl" 参数是指 "fail silently on SSL failures"，即如果 SSL 证书验证失败，则静默失败。

   cURL 是一个强大的命令行工具，可用于从网络中获取数据。使用 "-fssl" 参数时，如果 cURL 尝试访问的网站有一个无效的 SSL 证书，cURL 将不会显示错误信息，并直接返回一个错误代码。

   例如，当您希望从网络下载数据，并希望在 SSL 证书验证失败时不显示错误信息时，您可以使用 "curl -fssl" 命令。但是，如果您正在与重要的安全网站进行通信，请慎重使用此选项，因为在不验证 SSL 证书的情况下通信可能导致安全问题。

   

   **"gpg --dearmor -o"** 命令是用于将 ASCII 形式的 GPG 签名文件（通常以 .asc 结尾）转换为二进制形式，以便它可以用于 GPG 身份验证。

   "--dearmor" 参数告诉 GPG 进行解链接操作，而 "-o" 参数指定了输出文件的名称和路径。例如，如果您的 ASCII 形式的 GPG 签名文件的名称为 "signature.asc"，并且您希望将其转换为 "signature.gpg"，则您可以使用以下命令：

   ```
   cssCopy code
   gpg --dearmor -o signature.gpg signature.asc
   ```

   这将使用 GPG 工具将 ASCII 形式的签名文件 "signature.asc" 转换为二进制形式的文件 "signature.gpg"。您可以使用这种形式的签名文件进行 GPG 身份验证，以确保下载的文件已被授权人签名。

5. sudo chmod a+r /etc/apt/keyrings/docker.gpg

   "chmod a+r" 命令用于更改文件或目录的读取权限。在这种情况下，"a" 表示 "all"，因此 "a+r" 表示为所有用户（即所有者、组和其他）添加读取权限，这将导致任何用户都可以读取该文件，但不能修改或写入该文件。

   "chmod" 命令可以更改文件或目录的访问权限。它的用法非常灵活，可以通过使用数字代码或符号形式来设置权限。

   一种常见的用法是使用数字代码，例如：

   ```
   bashCopy code
   chmod 755 file.txt
   ```

   在此示例中，"755" 代表权限：

   - 7：所有者具有读、写和执行权限
   - 5：组用户具有读和执行权限
   - 5：其他用户具有读和执行权限

   另一种常见的用法是使用符号形式，例如：

   ```
   bashCopy code
   chmod u+x file.txt
   ```

   在此示例中，"u+x" 表示为所有者添加执行权限。其他常用的符号形式包括：

   - `u+r`：为所有者添加读取权限
   - `g+w`：为组用户添加写入权限
   - `o-r`：删除其他用户的读取权限

6. tee命令

   tee 命令在 Linux 中是一个非常常用的命令，它的作用是将输入的数据同时输出到标准输出（通常是屏幕）和一个文件中。这样，你可以查看命令的输出结果，同时也可以将结果保存到文件中。它是一个很方便的工具，能够让你同时在屏幕上和文件中查看命令的输出。

   语法：

   ```
   bashCopy code
   command | tee [选项] 文件
   ```

   常见选项： -a：以追加的方式向文件写入数据。 -i：忽略 SIGINT 信号。

   例如：

   ```
   bashCopy code
   ls -l | tee ls-l.txt
   ```

   这个命令会将 `ls -l` 的输出结果同时输出到屏幕上和 `ls-l.txt` 文件中。

7. sudo usermod -aG docker "$USER"

   "$USER"表示当前用户，将当前用户添加到docker组

8. bash: cd: docker: 权限不够

   sudo chmod 755 docker -R

   `chmod -R` 命令是用来修改文件的读写执行权限的，-R 参数表示递归处理，对当前目录以及子目录下的所有文件进行权限修改。

9. 

10. 

11. 

12. 

    

    
