---
keyword: [Docker, 容器, Linux, ECS, 云服务器, 阿里云, Alibaba Cloud Linux 3]
---

# 部署并使用Docker（Alibaba Cloud Linux 3）

本文介绍如何在Alibaba Cloud Linux 3.2104 64位操作系统的ECS实例上部署并使用Docker，适用于熟悉Linux操作系统、刚开始使用阿里云ECS的开发者。

已创建了至少一台Alibaba Cloud Linux 3.2104 64位操作系统的ECS实例。具体操作，请参见[使用向导创建实例](/intl.zh-CN/实例/创建实例/使用向导创建实例.md)。

本教程示例步骤适用于以下ECS实例配置：

-   实例规格：ecs.g6.large
-   操作系统：公共镜像Alibaba Cloud Linux 3.2104 64位
-   网络类型：专有网络VPC
-   IP地址：公网IP

本教程主要介绍以下内容：

-   部署Docker，具体操作，请参见[部署Docker](#section_m0l_g22_ska)。
-   使用Docker。
    -   Docker的基本用法介绍，请参见[使用Docker](#section_pcr_9i8_qtw)。
    -   制作镜像的示例操作，请参见[制作Docker镜像](#section_ozu_fww_6qa)。

## 部署Docker

1.  远程连接ECS实例。连接方式请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

2.  安装Docker。

    您可以通过以下任一方式安装Docker：

    -   安装dnf源中默认的Docker（podman-docker）。
        1.  运行以下命令，安装podman-docker。

            ```
            dnf -y install docker
            ```

        2.  运行以下命令，查看Docker是否安装成功。

            ```
            docker images
            ```

            回显信息如下图所示，表示Docker安装成功。

            **说明：** 该方式安装的podman-docker没有守护进程（systemd），因此您在后续的操作中无需关注podman-docker的运行状态（无需进行systemctl命令的相关操作），直接使用Docker即可。

            ![podman-docker](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5724064261/p288785.png)

    -   安装社区版Docker（docker-ce）。
        1.  运行以下命令，添加docker-ce的dnf源。

            ```
            dnf config-manager --add-repo=https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
            ```

        2.  运行以下命令，安装Alibaba Cloud Linux 3专用的dnf源兼容插件。

            ```
            dnf -y install dnf-plugin-releasever-adapter --repo alinux3-plus
            ```

        3.  运行以下命令，安装docker-ce。

            ```
            dnf -y install docker-ce --nobest
            ```

        4.  运行以下命令，查看docker-ce是否成功安装。

            ```
            dnf list docker-ce
            ```

            回显信息如下图所示，表示docker-ce成功安装。

            ![docker-ce](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6724064261/p289259.png)

3.  运行以下命令，启动Docker服务。

    ```
    systemctl start docker
    ```

4.  运行以下命令，查看Docker服务的运行状态。

    ```
    systemctl status docker
    ```

    回显信息如下图所示，表示Docker服务处于运行中的状态。

    ![docker-active](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6724064261/p289262.png)


## 使用Docker

Docker有以下基本用法：

-   管理Docker守护进程。

    ```
    systemctl start docker     #运行Docker守护进程
    systemctl stop docker      #停止Docker守护进程
    systemctl restart docker   #重启Docker守护进程
    systemctl enable docker    #设置Docker开机自启动
    systemctl status docker    #查看Docker的运行状态
    ```

-   管理镜像。本文使用的是来自阿里云仓库的Apache镜像。

    ```
    docker pull registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5
    ```

    -   修改标签。由于阿里云仓库镜像的镜像名称较长，您可以修改镜像标签以便记忆区分。

        ```
        docker tag registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5:latest aliweb:v1
        ```

    -   查看已有镜像。

        ```
        docker images
        ```

    -   强制删除镜像。

        ```
        docker rmi -f registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5
        ```

-   管理容器。
    -   进入容器。e1abc\*\*\*\*是执行`docker images`命令查询到的ImageId，使用`docker run`命令进入容器。

        ```
        docker run -it e1abc**** /bin/bash
        ```

    -   退出容器。使用`exit`命令退出当前容器。
    -   `run`命令加上`–d`参数可以在后台运行容器，`--name`指定容器命名为apache。

        ```
        docker run -d --name apache e1abc****
        ```

    -   进入后台运行的容器。

        ```
        docker exec -it apache /bin/bash
        ```

    -   查看容器ID。

        ```
        docker ps
        ```

    -   将容器做成镜像，命令的参数说明：`docker commit <容器ID或容器名> [<仓库名>[:<标签>]]`。

        ```
        docker commit containerID/containerName repository:tag
        ```

    -   为了方便测试和恢复，将源镜像运行起来后，再做一个命名简单的镜像做测试。

        ```
        docker commit 4c8066cd8**** apachephp:v1
        ```

    -   运行容器并将宿主机的8080端口映射到容器里去。

        ```
        docker run -d -p 8080:80 apachephp:v1
        ```

        在浏览器输入ECS实例IP地址加8080端口访问测试，出现以下内容则说明运行成功。

        **说明：** ECS实例的安全组入方向规则需要放行8080端口。具体操作，请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

        ![映射结果](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4712649951/p12348.png)


## 制作Docker镜像

1.  准备Dockerfile内容。

    1.  新建并编辑Dockerfile文件。

        ```
        vim Dockerfile
        ```

    2.  按i进入编辑模式，添加以下内容。

        ```
        #声明基础镜像来源。
        FROM apachephp:v1
        #声明镜像拥有者。
        MAINTAINER DTSTACK
        #RUN后面接容器运行前需要执行的命令，由于Dockerfile文件不能超过127行，因此当命令较多时建议写到脚本中执行。
        RUN mkdir /dtstact
        #开机启动命令，此处最后一个命令需要是可在前台持续执行的命令，否则容器后台运行时会因为命令执行完而退出。
        ENTRYPOINT ping www.aliyun.com
        ```

    3.  按下键盘esc键，输入`:wq`并按下enter键，保存并退出Dockerfile文件。

2.  创建镜像。

    ```
    docker build -t webalinux3:v1 .          #使用Dockerfile创建镜像。命令末尾的`.`是Dockerfile文件的路径，不能忽略。
    docker images                            #查看是否创建成功。
    ```

3.  运行容器并查看容器信息。

    ```
    docker run -d webalinux3:v1           #后台运行容器。
    docker ps                             #查看当前运行中的容器。
    docker ps -a                          #查看所有容器，包括未运行的容器。
    docker logs CONTAINER ID/IMAGE        #如未查看到刚才运行的容器，则用容器id或者名称查看启动日志排错。
    ```

4.  制作镜像。

    ```
    docker commit fb2844b6**** dtstackweb:v1     #commit参数后添加容器ID和构建新镜像的名称和版本号。
    docker images                                #列出本地（已下载的和本地创建的）镜像。
    ```

5.  将镜像推送至远程仓库。

    默认推送到Docker Hub。您需要先登录Docker，为镜像绑定标签，将镜像命名为`Docker用户名/镜像名:标签`的格式。最终完成推送。

    ```
    docker login --username=dtstack_plus registry.cn-shanghai.aliyuncs.com    #执行后输入镜像仓库密码。
    docker tag \[ImageId\] registry.cn-shanghai.aliyuncs.com/dtstack123/test:\[标签\]
    docker push registry.cn-shanghai.aliyuncs.com/dtstack123/test:\[标签\]
    ```


