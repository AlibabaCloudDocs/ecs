---
keyword: [Docker, 容器, Linux, ECS, 云服务器, 阿里云, Alibaba Cloud Linux 2]
---

# 部署并使用Docker（Alibaba Cloud Linux 2）

本文介绍如何在Alibaba Cloud Linux 2.1903 LTS 64位操作系统的ECS实例上部署并使用Docker，适用于熟悉Linux操作系统，刚开始使用阿里云ECS的开发者。

已创建了至少一台ECS实例。具体操作，请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。

本教程示例步骤适用于以下ECS实例配置：

-   实例规格：ecs.g6.large
-   操作系统：公共镜像Alibaba Cloud Linux 2.1903 LTS 64位

    **说明：** 本示例操作命令同样适用于CentOS 7系统。

-   网络类型：专有网络VPC
-   IP地址：公网IP

本教程主要介绍以下内容：

-   部署Docker，具体操作，请参见[部署Docker](#section_gtl_cjs_ls2)。
-   使用Docker。
    -   Docker的基本用法介绍，请参见[使用Docker](#section_x1c_w5u_5wb)。
    -   制作镜像的示例操作，请参见[制作Docker镜像](#section_i4r_m92_6ev)。

## 部署Docker

本节主要介绍手动安装Docker的操作步骤，您也可以在[云市场](https://market.aliyun.com/software)购买相应镜像，一键部署云服务器。

1.  远程连接ECS实例。连接方式请参见[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  安装Docker。

    您可以通过以下任一方式安装Docker：

    -   安装yum源中默认的Docker。

        ```
        yum -y install docker
        ```

    -   安装社区版Docker（docker-ce）。
        1.  运行以下命令，下载docker-ce的yum源。

            ```
            wget -O /etc/yum.repos.d/docker-ce.repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
            ```

        2.  运行以下命令，安装Alibaba Cloud Linux 2专用的yum源兼容插件。

            **说明：** 仅当您的实例为Alibaba Cloud Linux 2操作系统时，需要运行该命令。

            ```
            yum install yum-plugin-releasever-adapter --disablerepo=* --enablerepo=plus
            ```

        3.  运行以下命令，安装docker-ce。

            ```
            yum -y install docker-ce
            ```

3.  运行以下命令，启动Docker服务。

    ```
    systemctl start docker
    ```

4.  运行以下命令，查看Docker服务的运行状态。

    ```
    systemctl status docker
    ```

    回显结果如下图所示，表示Docker已成功部署并处于运行状态。

    ![docker active](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4200954261/p287883.png)

    **说明：** 如果您需要查看Docker的版本，请运行docker -v命令。


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

        **说明：** ECS实例的安全组入方向规则需要放行8080端口。具体操作，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

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

2.  构建镜像。

    ```
    docker build -t webalibabacloudlinux:v1 .    #命令末尾的`.`是Dockerfile文件的路径，不能忽略。
    docker images                                #查看是否创建成功。
    ```

3.  运行容器并查看。

    ```
    docker run -d webalibabacloudlinux:v1    #后台运行容器。
    docker ps                                #查看当前运行中的容器。
    docker ps -a                             #查看所有容器，包括未运行中的。
    docker logs CONTAINER ID/IMAGE           #如未查看到刚才运行的容器，则用容器id或者名字查看启动日志排错。
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


