# 用docker部署go项目流程

使用Docker部署Go项目是一种将应用程序与其依赖项打包成容器的方式，以便于跨多个环境部署和运行。以下是一个基本的Docker部署Go项目的流程：

1. **编写Dockerfile：** 在你的Go项目根目录下创建一个名为 `Dockerfile` 的文件。Dockerfile 是用来构建Docker镜像的脚本。示例Dockerfile可能如下：

   ```docker
   DockerfileCopy code# 使用官方的Golang镜像作为基础镜像
   FROM golang:1.16
   
   # 设置工作目录
   WORKDIR /go/src/app
   
   # 复制项目文件到镜像中
   COPY . .
   
   # 构建项目
   RUN go build -o main .
   
   # 暴露端口
   EXPOSE 8080
   
   # 定义启动命令
   CMD ["./main"]
   ```

2. **构建Docker镜像：** 在项目根目录下运行以下命令来构建Docker镜像。将 `your-image-name` 替换为你想要的镜像名称。

   ```bash
   arduinoCopy code
   docker build -t your-image-name .
   ```

3. **运行Docker容器：** 构建完成后，你可以使用以下命令在Docker容器中运行你的Go应用程序。将 `your-container-name` 替换为你想要的容器名称。

   ```bash
   arduinoCopy code
   docker run --name your-container-name -p 8080:8080 -d your-image-name
   ```

   这将在后台运行一个Docker容器，并将宿主机的端口8080映射到容器的端口8080。

4. **访问应用程序：** 在浏览器中访问 `http://localhost:8080`，或者使用其他工具来测试你的Go应用程序是否在Docker容器中正常运行。

5. **管理容器：** 使用以下命令可以对容器进行管理：

   - 停止容器：`docker stop your-container-name`
   - 启动容器：`docker start your-container-name`
   - 删除容器：`docker rm your-container-name`

# dockerfile

| Dockerfile 指令 | 说明                                                         |
| :-------------- | :----------------------------------------------------------- |
| FROM            | 指定基础镜像，用于后续的指令构建。                           |
| MAINTAINER      | 指定Dockerfile的作者/维护者。（已弃用，推荐使用LABEL指令）   |
| LABEL           | 添加镜像的元数据，使用键值对的形式。                         |
| RUN             | 在构建过程中在镜像中执行命令。                               |
| CMD             | 指定容器创建时的默认命令。（可以被覆盖）                     |
| ENTRYPOINT      | 设置容器创建时的主要命令。（不可被覆盖）                     |
| EXPOSE          | 声明容器运行时监听的特定网络端口。                           |
| ENV             | 在容器内部设置环境变量。                                     |
| ADD             | 将文件、目录或远程URL复制到镜像中。                          |
| COPY            | 将文件或目录复制到镜像中。                                   |
| VOLUME          | 为容器创建挂载点或声明卷。                                   |
| WORKDIR         | 设置后续指令的工作目录。                                     |
| USER            | 指定后续指令的用户上下文。                                   |
| ARG             | 定义在构建过程中传递给构建器的变量，可使用 "docker build" 命令设置。 |
| ONBUILD         | 当该镜像被用作另一个构建过程的基础时，添加触发器。           |
| STOPSIGNAL      | 设置发送给容器以退出的系统调用信号。                         |
| HEALTHCHECK     | 定义周期性检查容器健康状态的命令。                           |
| SHELL           | 覆盖Docker中默认的shell，用于RUN、CMD和ENTRYPOINT指令。      |

#  docker-compose的yaml文件

Docker Compose 是一个用于定义和运行多个 Docker 容器的工具，其配置文件采用 YAML（YAML Ain't Markup Language）格式。下面是 Docker Compose YAML 文件中常见的字段：

1. version: 指定 Docker Compose 文件的版本。例如：`version: '3'`。

2. services: 定义各个服务（容器）的配置信息，每个服务都是一个独立的容器。服务名称作为字段名称，字段值是一个对象，包含该服务的配置。

   - image: 指定服务使用的 Docker 镜像。
   - build: 指定服务的构建配置，可以使用 Dockerfile 构建镜像。
   - ports: 指定服务容器和主机之间的端口映射关系。
   - volumes: 定义数据卷的映射关系，用于持久化数据或共享数据。
   - environment: 设置环境变量。
   - depends_on: 指定当前服务依赖的其他服务。
   - command: 指定容器启动后要执行的命令。

3. networks: 定义网络配置，允许不同服务之间进行通信。

4. volumes: 定义数据卷配置，可以在容器之间共享数据。

5. secrets: 定义加密的敏感信息，如密码、API 密钥等。

6. configs: 定义配置文件。

7. extensions: 定义扩展字段，用于引入其他文件或自定义配置。

这些是 Docker Compose YAML 文件中最常见的字段，还可以根据具体需求添加其他字段或使用扩展功能。请注意，不同版本的 Docker Compose 支持的字段可能会有所不同，因此请根据所使用的 Docker Compose 版本查阅相应的文档以获取更详细的信息。

# 在项目中常用命令

Docker是一个强大的容器化平台，用于创建、部署和管理容器化应用程序。以下是在项目中常用的一些Docker命令：

1. **构建镜像：** 使用Dockerfile构建一个新的镜像。

   ```bash
   phpCopy code
   docker build -t <image_name> <path_to_Dockerfile>
   ```

2. **运行容器：** 在一个新的容器中运行一个镜像。

   ```bash
   phpCopy code
   docker run --name <container_name> -p <host_port>:<container_port> -d <image_name>
   ```

3. **列出容器：** 查看当前正在运行的容器。

   ```bash
   Copy code
   docker ps
   ```

   使用 `-a` 参数可以查看所有容器，包括停止的。

4. **停止容器：** 停止一个正在运行的容器。

   ```bash
   arduinoCopy code
   docker stop <container_name>
   ```

5. **启动容器：** 启动一个已经停止的容器。

   ```bash
   phpCopy code
   docker start <container_name>
   ```

6. **删除容器：** 删除一个已经停止的容器。

   ```bash
   bashCopy code
   docker rm <container_name>
   ```

7. **查看日志：** 查看容器的日志输出。

   ```bash
   phpCopy code
   docker logs <container_name>
   ```

8. **查看镜像：** 列出已经下载的镜像。

   ```bash
   Copy code
   docker images
   ```

9. **删除镜像：** 删除一个本地的镜像。

   ```bash
   phpCopy code
   docker rmi <image_name>
   ```

10. **进入容器：** 在容器内部启动一个新的Shell会话。

    ```bash
    bashCopy code
    docker exec -it <container_name> /bin/bash
    ```

11. **复制文件：** 将本地文件复制到容器中。

    ```bash
    phpCopy code
    docker cp <local_path> <container_name>:<container_path>
    ```

12. **导出容器：** 将容器打包成一个可导入的文件。

    ```bash
    phpCopy code
    docker export <container_name> > <output_file.tar>
    ```

13. **导入容器：** 导入一个已经打包的容器。

    ```
    arduinoCopy code
    docker import <input_file.tar>
    ```

14. **构建并运行容器：** 将构建和运行容器合并为一条命令。

    ```
    phpCopy code
    docker run -d -p <host_port>:<container_port> <image_name>
    ```

15. **网络管理：** Docker可以创建网络以连接容器，以及设置容器的网络别名和连接。

    ```bash
    luaCopy code
    docker network create <network_name>
    ```

# 常用命令


当使用Docker进行容器化应用程序的管理和部署时，以下是一些常用的Docker命令：

1. **镜像管理：**
   - 构建镜像：`docker build -t <image_name> <path_to_Dockerfile>`
   - 列出本地镜像：`docker images`
   - 删除本地镜像：`docker rmi <image_name>`
2. **容器管理：**
   - 运行容器：`docker run --name <container_name> -p <host_port>:<container_port> -d <image_name>`
   - 列出正在运行的容器：`docker ps`
   - 列出所有容器（包括停止的）：`docker ps -a`
   - 停止容器：`docker stop <container_name>`
   - 启动容器：`docker start <container_name>`
   - 重启容器：`docker restart <container_name>`
   - 进入容器：`docker exec -it <container_name> /bin/bash`
   - 删除容器：`docker rm <container_name>`
   - 查看容器日志：`docker logs <container_name>`
   - 复制文件到容器：`docker cp <local_path> <container_name>:<container_path>`
3. **网络管理：**
   - 创建网络：`docker network create <network_name>`
   - 列出网络：`docker network ls`
   - 连接容器到网络：`docker network connect <network_name> <container_name>`
   - 断开容器与网络的连接：`docker network disconnect <network_name> <container_name>`
4. **数据卷管理：**
   - 创建数据卷：`docker volume create <volume_name>`
   - 列出数据卷：`docker volume ls`
   - 删除数据卷：`docker volume rm <volume_name>`
5. **Compose管理（用于多容器应用的定义和管理）：**
   - 启动Compose应用：`docker-compose up -d`
   - 关闭Compose应用：`docker-compose down`
6. **其他：**
   - 版本信息：`docker version`
   - 系统信息：`docker info`
   - 清理无用资源：`docker system prune`

这些是一些常见的Docker命令，但Docker提供了更多丰富的功能和选项，以满足不同场景下的需求。你可以通过运行 `docker --help` 或 `docker <command> --help` 来获取更多关于特定命令的帮助信息。

# 字节跳动



## docker 隔离机制

Docker 提供了一种轻量级的容器化解决方案，它使用了多种隔离机制来确保容器之间的相互隔离。这些隔离机制有助于保护容器中的应用程序和进程，防止相互之间的冲突和干扰。以下是 Docker 使用的主要隔离机制：

1. 命名空间（Namespaces）：Docker 使用一系列的命名空间来提供隔离环境。每个容器都有自己的一组命名空间，包括 PID（进程 ID）、网络、文件系统、IPC（进程间通信）和用户等。每个命名空间都为容器提供了一个独立且隔离的视图，使得容器中的进程无法感知到其他容器的存在。
2. 控制组（Control Groups）：控制组是 Linux 内核提供的一种机制，用于限制和管理进程的资源使用。Docker 使用控制组来限制容器的资源（如 CPU、内存、磁盘和网络带宽）使用，并确保容器之间的资源分配互不干扰。通过控制组，Docker 可以对容器的资源进行精确的控制和管理。
3. 文件系统隔离：Docker 使用容器的文件系统隔离来确保容器之间的文件系统相互隔离。每个容器都有自己的根文件系统，容器内的文件系统对外部是不可见的。这使得容器可以拥有自己的文件系统层次结构，并且不会相互干扰。
4. 网络隔离：Docker 使用网络隔离来确保容器之间的网络相互隔离。每个容器都有自己的网络命名空间，独立于主机和其他容器的网络环境。这使得容器可以拥有独立的 IP 地址、网络接口和网络配置，从而实现容器之间的网络隔离和通信。
5. 用户命名空间：Docker 使用用户命名空间来隔离容器内部的用户和用户组。每个容器都有自己的用户命名空间，使得容器内的用户和用户组与主机系统和其他容器的用户和用户组相互隔离。

这些隔离机制的结合使用，使得 Docker 能够提供高度隔离的容器环境。容器内的应用程序和进程可以在相对独立的环境中运行，互不干扰，并且与主机系统和其他容器之间实现良好的隔离。

## 容器虚拟机哪个隔离性更好

**从隔离性的角度来看，虚拟机通常提供比容器更高级别的隔离。**

虚拟机在硬件级别上使用完整的虚拟化技术，每个虚拟机都有自己的操作系统内核和独立的硬件资源。这种隔离性可以确保虚拟机之间的相互隔离，即使一个虚拟机中的应用程序或操作系统崩溃，也不会影响其他虚拟机。虚拟机提供了较高的安全性和隔离级别，适用于需要完全隔离的场景。

容器在操作系统级别上使用虚拟化技术，共享主机操作系统的内核和硬件资源。容器使用命名空间、控制组和文件系统隔离等机制来实现容器之间的相对隔离。虽然容器提供了一定程度的隔离，但它们仍然共享主机操作系统的内核，因此在某些情况下，容器之间的隔离性可能不如虚拟机。

尽管容器的隔离性相对较弱，但容器也提供了一些优势。容器启动和停止更快，资源占用更少，密度更高，部署更简便。容器可以在同一主机上运行更多的实例，提供更高的资源利用率和可伸缩性。容器还具有更好的可移植性，可以轻松在不同环境中部署和迁移。

综上所述，虚拟机在隔离性方面通常更优于容器。但容器在其他方面的优势使其成为许多应用场景的理想选择。在实际应用中，需要根据具体需求和权衡来选择虚拟机或容器，或者使用虚拟机和容器的组合来满足不同的隔离和性能要求。

容器和虚拟机在隔离性方面有一些差异，但无法简单地说哪个具有更好的隔离性，因为这取决于具体的使用情况和需求。

虚拟机（Virtual Machine）是基于完整的虚拟化技术，通过在物理服务器上运行虚拟化层和多个独立的操作系统实例来实现隔离。每个虚拟机都有自己的操作系统内核，独立的硬件资源（如 CPU、内存）和虚拟硬件（如磁盘、网络接口），它们之间的隔离性较高。

容器（Container）则是基于操作系统级虚拟化技术，通过在同一操作系统内核上运行多个隔离的用户空间实例来实现隔离。容器共享主机操作系统的内核和硬件资源，但通过使用命名空间、控制组和文件系统隔离等机制，实现容器之间的相对隔离。

虚拟机相对于容器的优势在于它们提供了更高级别的隔离，因为每个虚拟机都拥有独立的操作系统内核和资源。这使得虚拟机可以实现更强的隔离，适用于需要完全隔离的场景，如多租户环境、安全性要求高的应用等。

然而，容器也有其优势。容器启动和停止速度更快，占用更少的资源，并且更轻量级。容器可以在同一主机上运行更多的实例，提供更高的密度和资源利用率。容器还具有更好的可移植性和易于部署的特点，使得开发、测试和部署过程更加便捷。

因此，选择使用虚拟机还是容器取决于具体的需求和使用场景。如果需要高度隔离和完全独立的环境，虚拟机可能是更好的选择。如果注重轻量级、高效率和可移植性，容器是更合适的选择。实际应用中，通常会根据具体需求和权衡来选择使用虚拟机、容器或两者的组合来满足不同的需求。

## 虚拟机的缺点

虚拟机虽然在隔离性方面具有优势，但也存在一些缺点，包括以下几个方面：

1. 资源占用：每个虚拟机都需要独立的操作系统和资源，包括内存、存储和计算资源。这会导致较高的资源占用，特别是在需要同时运行多个虚拟机的情况下。相比之下，容器共享主机操作系统的内核和资源，因此在资源利用率方面更加高效。
2. 启动时间：虚拟机需要启动完整的操作系统，这需要较长的启动时间。相比之下，容器启动时间更快，因为它们只需要启动容器内的应用程序和进程，而无需启动整个操作系统。
3. 管理复杂性：虚拟机的管理相对较为复杂。每个虚拟机都需要独立的操作系统安装、配置和维护，包括安全补丁、软件更新等。此外，虚拟机的迁移和扩展也需要额外的管理操作。相比之下，容器的管理相对简单，容器镜像可以轻松部署和迁移，并且容器的管理工具和平台提供了更高级别的自动化和简化操作。
4. 性能开销：由于虚拟机需要模拟硬件层，因此在运行时存在一定的性能开销。虚拟机的运行通常需要更多的计算资源，而且在虚拟化层的传输和处理也会引入一定的延迟。相比之下，容器直接在主机操作系统上运行，无需虚拟化层的介入，因此具有更低的性能开销。

虚拟机和容器各有优势和劣势，根据具体需求和场景来选择合适的解决方案。虚拟机适用于需要完全隔离和独立操作系统的场景，而容器适用于轻量级、高效率和可移植性要求较高的场景。

#  知识点

## 特点

Docker 和传统虚拟化方式的不同*传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整操作系统，在该系统上再运行所需应用进程；*容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核且也没有进行硬件虚拟。因此容器要比传统虚拟机更为轻便。* 每个容器之间互相隔离，每个容器有自己的文件系统 ，容器之间进程不会相互影响，能区分计算资源。(1)docker有着比虚拟机更少的抽象层  由于docker不需要Hypervisor(虚拟机)实现硬件资源虚拟化,运行在docker容器上的程序直接使用的都是实际物理机的硬件资源。因此在CPU、内存利用率上docker将会在效率上有明显优势。(2)docker利用的是宿主机的内核,而不需要加载操作系统OS内核  当新建一个容器时,docker不需要和虚拟机一样重新加载一个操作系统内核。进而避免引寻、加载操作系统内核返回等比较费时费资源的过程,当新建一个虚拟机时,虚拟机软件需要加载OS,返回新建过程是分钟级别的。而docker由于直接利用宿主机的操作系统,则省略了返回过程,因此新建一个docker容器只需要几秒钟。

## 架构

Docker是一个C/S模式的架构，后端是一个松耦合架构，众多模块各司其职

Docker底层架构是基于C/S架构的，包括客户端和服务端。Docker daemon作为服务端接受来自客户端的请求，并处理这些请求，包括创建、运行、分发容器等。客户端和服务端既可以运行在一个机器上，也可以通过socket或者RESTful API来进行通信。

此外，Docker的底层核心技术包括Linux的命名空间（NameSpace）、控制组（control groups）、Union文件系统（Union file system）和容器格式（Container format）。这些技术共同实现了Docker容器的隔离性、资源限制、文件系统分层和可移植性等特点。

具体来说，Linux的命名空间用于隔离系统资源，让每个容器都拥有独立的网络、进程、文件系统等资源视图；控制组用于限制容器的资源使用，如CPU、内存等；Union文件系统则实现了文件系统的分层和共享，使得容器可以共享底层文件系统，同时又可以拥有自己独立的文件系统层；容器格式则是Docker定义的一种容器镜像和容器运行时的标准格式，保证了容器的可移植性和一致性。

总的来说，Docker的底层架构是基于C/S架构和一系列Linux内核技术实现的，通过这些技术实现了容器的隔离、资源限制、文件系统分层和可移植性等特点，使得Docker成为了一种非常流行的容器化技术。

## 三要素

* 镜像

image是一种轻量级，可执行的独立软件包，它包含运行某个软件所需的所有内容，我们把应用程序和配置依赖打包好形成一个可交付的运行环境（包括代码、运行时需要的库、环境变量和配置文件等），这个打包好的运行环境就是image镜像文件。只有通过这个镜像文件才能生成Docker容器实例

* 容器

containerDocker 利用容器（Container）独立运行的一个或一组应用，应用程序或服务运行在容器里面，容器就类似于一个虚拟化的运行环境。可以把容器看做是一个简易版的linux环境（包括root用户权限、进程空间、用户空间和网络空间等）和运行其中应用程序。镜像是静态的定义，容器是镜像运行时的实体。容器为镜像提供了一个标准的和隔离的运行环境，它可以被启动、开始、停止删除。每个容器都是相互隔离的、保证安全的平台

* 仓库

repository 集中存放镜像文件的场所 公开仓库 私有仓库
## 数据挂载

![image-20240216145253843](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20240216145253843.png)

## 网络模式

* 介绍：概述负责docker与宿主/容器之间的网络通信、端口映射.容器ip变动时, 可通过容器名通信而不受影响. (docker内部容器ip是可能变动的)
* 基本命令：docker network --help

![image-20240216150015185](D:\typora\Golang_Engineer\typora-user-images\image-20240216150015185.png)

* 创建网络：docker network create --driver <DriverType> <DriverName>  默认创建的驱动类型是 bridge

* 指定网络：--network <NetName> ；对于指定container ： --network container:<containerName>

* 网络类型

  1. bridge：**默认**，Docker 服务默认会创建一个 docker0 网桥（其上有一个 docker0 内部接口），该桥接网络的名称为docker0，它在内核层连通了其他的物理或虚拟网卡，这就将所有容器和本地主机都放到同一个物理网络。Docker 默认指定了 docker0 接口 的 IP 地址和子网掩码，让主机和容器之间可以通过网桥相互通信。两两对应原则

     ![image-20240216150526691](D:\typora\Golang_Engineer\typora-user-images\image-20240216150526691.png)

  2. host：直接使用宿主机的 IP 地址与外界进行通信，不再需要额外进行网络地址转换

  ![image-20240216150635671](D:\typora\Golang_Engineer\typora-user-images\image-20240216150635671.png)

  3. none：禁止网络功能，只有lo标识（127.0.0.1，表示本地回环）

  4. container：新建的容器使用另一个容器的网络ip配置, 不和宿主机直接通信

  ![image-20240216150759204](D:\typora\Golang_Engineer\typora-user-images\image-20240216150759204.png)

  5. 自定义网络：同一个Docker服务下, 默认桥接时, 容器内部可以通过ip内网互通. 但是ip是可变动的, 使用服务名(容器名)ping不通. 自定义网络(桥接即可)默认维护了服务名和ip的关系, 多个容器使用同一个自定义网络即可实现稳定的通过服务名的通信
  6. ![image-20240216150837044](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20240216150837044.png)

## 镜像构建与发布

* 原理：镜像实际上由一层一层的文件系统组成，这种层级的文件系统UnionFS。分层最大的一个好处就是共享资源，方便复制迁移，就是为了复用。当容器启动时，一个新的可写层被加载到镜像的顶部。这一层通常被称作“容器层”，“容器层”之下的都叫“镜像层”。所有对容器的改动 - 无论添加、删除、还是修改文件都只会发生在容器层中。只有容器层是可写的，容器层下面的所有镜像层都是只读的。

* 构建镜像

  1. 依靠容器：docker commit -m="提交的描述信息" -a="作者" <containerId> <imgName>:<tag>

  2. Dockerfile

     * 是什么：Dockerfile是用来构建Docker镜像的文本文件，是由一条条构建镜像所需的指令和参数构成的脚本。
     * 构建镜像步骤：1.编写Dockerfile文件 2.创建镜像 docker build -f <目标Dockerfile文件名> -t <imgName:tag> .
     * 生成容器（注意：末尾有空格+"."）

  3. demo

     ```go
     基于centos7, 增强 ifconfig, vim, jdk#基于centos, 增强 vim, jdk, ipconfig# 基于centosFROM centos:7# 作者信息maintainer ryze<test@test.com># 环境变量ENV WORKPATH /usr/local# 工作默认路径(引用环境变量)WORKDIR $WORKPATH# RUN: 执行命令(build时)# 安装vim RUN yum -y install vim# 安装 ipconfigRUN yum -y install net-tools# 安装jdkRUN yum -y install glibc.i686RUN mkdir /usr/local/java# 宿主机文件添加到镜像中ADD jdk-8u212-linux-x64.tar.gz /usr/local/java/# jdk环境变量ENV JAVA_HOME /usr/local/java/jdk1.8.0_212ENV JRE_HOME $JAVA_HOME/jreENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib:$CLASSPATHENV PATH $JAVA_HOME/bin:$PATH# 暴露端口EXPOSE 10000CMD eoho $WORKPATHCMD echo "======镜像构建成功======"CMD /bin/bash
     ```

  4. 问题 ：创建img过程中可能出现各种问题导致出现虚悬镜像 1.删除虚悬镜像 2.docker image prune

## 镜像发布

![image-20240216153840081](D:\typora\Golang_Engineer\typora-user-images\image-20240216153840081.png)

## compose 容器编排

* 概述
  1. Docker-Compose是Docker官方的开源项目，负责实现对Docker容器集群的快速编排。
  2. 定义一个 YAML 格式的配置文件docker-compose.yml，写好多个容器之间的调用关系。然后，只要一个命令，就能同时启动/关闭这些容器
  3. Compose允许用户通过一个单独的docker-compose.yml模板文件（YAML 格式）来定义一组相关联的应用容器为一个项目（project）。可以很容易地用一个配置文件定义一个多容器的应用，然后使用一条指令安装这个应用的所有依赖，完成构建。其中的容器 可通过服务名互相访问, Docker-Compose 解决了容器与容器之间如何管理编排的问题。
* 安装、修改权限、版本查看、卸载

![image-20240216155029093](D:\typora\Golang_Engineer\typora-user-images\image-20240216155029093.png)

* 编排步骤
  1. 准备好docker镜像（基础镜像/本地dockerfile构建）
  2. 编写docker-compose.yaml
  3. 检查配置docker-compose config
  4. 后台启动 docker-compose up -d
  5. 关停docker-compose stop
* demo 

1. 构建一个集成 mysql/redis 的服务镜像

其中配置文件依赖的同Docker下的服务可用服务名替代

```
# 基于基础镜像java:8FROM java:8
# 作者MAINTAINER raozheng
# VOLUME 指定临时文件目录为/tmp，在主机/var/lib/docker目录下创建了一个临时文件并链接到容器的/tmpVOLUME /tmp
# 将jar包添加到容器中并更名为zzyy_docker.jarADD Demo-Docker.jar Demo-Docker.jar
# 运行jar包RUN bash -c 'touch /Demo-Docker.jar'ENTRYPOINT ["java","-jar","/Demo-Docker.jar"]
# 暴露端口作为微服务EXPOSE 8888
```

2. 编写docker-compose.yaml

   ```yaml
   
   编写docker-compose.yaml
   version: "3"
   services:  microService:    image: raozheng:2.0    container_name: democompose    ports:      - "8888:8888"    volumes:      - /ryze/demodockercompose/microService:/data    networks:      - compose_net    depends_on:      - redis      - mysql  redis:    image: redis:6.0.8    container_name: redis    ports:      - "6380:6379"    volumes:      - /ryze/demodockercompose/redis/redis.conf:/etc/redis/redis.conf      - /ryze/demodockercompose/redis/data:/data    networks:      - compose_net    command: redis-server /etc/redis/redis.conf  mysql:    image: mysql:5.7    container_name: mysql    environment:      MYSQL_ROOT_PASSWORD: '0000'      MYSQL_ALLOW_EMPTY_PASSWORD: 'no'      MYSQL_DATABASE: 'test'    ports:       - "3307:3306"    volumes:       - /ryze/demodockercompose/mysql/db:/var/lib/mysql       - /ryze/demodockercompose/mysql/conf/my.cnf:/etc/my.cnf       - /ryze/demodockercompose/mysql/init:/docker-entrypoint-initdb.d    networks:      - compose_net    command: --default-authentication-plugin=mysql_native_password #解决外部无法访问networks:   compose_net:     driver:       bridge
   ```

3. 注意：容器之间通过容器名进行网络通信, 需要在compose手动指定容器名 container_name

## 容器原理

1. Docker容器只是一种特殊的进程, 是一个“单进程”模型
2. 使用Linux的特性进行"虚拟机的效果" 1. 访问隔离: namespace 2. 资源限制: CGroups
3. 由于一个容器的本质就是一个进程，用户的应用进程实际上就是容器里 PID=1 的进程，也是其他后续创建的所有进程的父进程。这就意味着，在一个容器中，你没办法同时运行两个不同的应用，除非你能事先找到一个公共的 PID=1 的程序来充当两个不同应用的父进程

## 容器可视化监控

- Portainer

1. Portainer 是一款轻量级的应用，它提供了图形化界面，用于方便地管理Docker环境，包括单机环境和集群环境。

2. ```bash
   docker run -d -p 7000:8000 -p 9000:9000 --name portainer     --restart=always     -v /var/run/docker.sock:/var/run/docker.sock     -v portainer_data:/data     portainer/portainer
   ```

- 重量级监控

1. CAdvisor + InfluxDB + Granfana
2. ![image-20240216172315019](D:\typora\Golang_Engineer\typora-user-images\image-20240216172315019.png)

3. 安装

   ```yaml
   Dockerfileversion: '3.1' volumes:  grafana_data: {} services: influxdb:  image: tutum/influxdb:0.9  restart: always  environment:    - PRE_CREATE_DB=cadvisor  ports:    - "8083:8083"    - "8086:8086"  volumes:    - ./data/influxdb:/data  cadvisor:  image: google/cadvisor  links:    - influxdb:influxsrv  command: -storage_driver=influxdb -storage_driver_db=cadvisor -storage_driver_host=influxsrv:8086  restart: always  ports:    - "8080:8080"  volumes:    - /:/rootfs:ro    - /var/run:/var/run:rw    - /sys:/sys:ro    - /var/lib/docker/:/var/lib/docker:ro  grafana:  user: "104"  image: grafana/grafana  user: "104"  restart: always  links:    - influxdb:influxsrv  ports:    - "3000:3000"  volumes:    - grafana_data:/var/lib/grafana  environment:    - HTTP_USER=admin    - HTTP_PASS=admin    - INFLUXDB_HOST=influxsrv    - INFLUXDB_PORT=8086    - INFLUXDB_NAME=cadvisor    - INFLUXDB_USER=root    - INFLUXDB_PASS=root
   ```

   4. 测试：8080/8083/3000端口

* ![image-20240216172436059](D:\typora\Golang_Engineer\typora-user-images\image-20240216172436059.png)
