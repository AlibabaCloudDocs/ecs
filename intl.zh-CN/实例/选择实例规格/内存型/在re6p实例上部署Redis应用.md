# 在re6p实例上部署Redis应用

Redis应用运行在持久内存型实例上可以降低单GiB内存的成本，但为了保证性能，您需要对Redis应用做适当的改造。为了最大程度降低您的应用改造成本，re6p专门提供了针对Redis应用的规格，通过几行命令即可快速部署Redis应用。本文以Alibaba Cloud Linux 2和CentOS为例介绍如何在re6p实例上快速部署Redis应用。

本文中快速部署Redis应用的步骤仅适用于以下实例规格：

-   ecs.re6p-redis.large
-   ecs.re6p-redis.xlarge
-   ecs.re6p-redis.2xlarge
-   ecs.re6p-redis.13xlarge

**说明：** ecs.re6p-redis.<nx\>large是为Redis应用推出的专用实例规格，只支持将持久内存作为内存使用。

如果您使用其他系统部署Redis应用，请保证镜像的版本满足以下要求：

-   Alibaba Cloud Linux 2
-   CentOS 7.6及更高版本
-   Ubuntu 18.10及更高版本
-   SUSE Linux 12 SP4及更高版本

## 在使用Alibaba Cloud Linux 2操作系统的re6p实例上部署Redis应用

Alibaba Cloud Linux 2操作系统对Redis应用进行了专项调优，相比社区版操作系统，Redis应用整体性能提升20%以上。

Alibaba Cloud Linux 2操作系统内置Redis 6.0.5和Redis 3.2.12的yum源，您可以通过yum install命令直接部署Redis 6.0.5和Redis 3.2.12。您也可以手动部署其他Redis版本，具体操作，请参见[在使用CentOS系统的re6p实例上部署Redis应用](#section_gx2_rzq_8rk)。

本示例中使用的配置如下：

-   实例规格：ecs.re6p-redis.2xlarge
-   镜像：Alibaba Cloud Linux 2.1903 LTS 64位

1.  购买持久内存实例。

    具体操作，请参见[使用向导创建实例](/intl.zh-CN/实例/创建实例/使用向导创建实例.md)。请注意以下配置：

    -   **实例**：单击**x86计算**架构下的**内存型**分类，并选中名称为ecs.re6p-redis.2xlarge的实例规格。
    -   **镜像**：选择Alibaba Cloud Linux 2.1903 LTS 64位。
2.  登录实例。

    具体操作，请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

3.  安装阿里云exp源。

    ```
    yum install -y alinux-release-experimentals
    ```

4.  部署Redis应用。

    -   部署Redis 6.0.5：

        ```
        yum install -y redis-6.0.5
        ```

    -   部署Redis 3.2.12：

        ```
        yum install -y redis-3.2.12
        ```

5.  配置网卡多队列。

    网卡多队列可以帮助Redis应用获得更好的性能。

    1.  下载自动配置脚本ecs\_mq。

        ```
        wget https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/ecs_mq/ecs_mq_latest.tgz
        ```

    2.  解压脚本。

        ```
        tar -xzf ecs_mq_latest.tgz
        ```

    3.  更换工作路径。

        ```
        cd ecs_mq/
        ```

    4.  运行脚本。

        不同的镜像版本的命令格式不同，例如Alibaba Cloud Linux 2.1903镜像运行`bash install.sh aliyun 2`。

        ```
        bash install.sh <系统名称> <系统主版本号>
        ```

    5.  启动服务。

        ```
        systemctl start ecs_mq
        ```

6.  查看普通内存和持久内存的容量大小。

    1.  安装numactl。

        ```
        yum install -y numactl
        ```

    2.  查看普通内存和持久内存的容量大小。

        ```
        numactl -H
        ```

        **说明：** `node 0 free`为可分配给应用程序的普通内存容量，`node 1 free`为可分配给应用程序的持久内存容量。

        ![available-mem](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7756517161/p259154.png)

7.  启动Redis服务。

    1.  设置环境变量。

        ```
        export MEMKIND_DAX_KMEM_NODES=1
        ```

    2.  启动Redis（配置默认使用的普通内存和持久内存容量）。

        **说明：** 为防止其他未经优化的应用（例如Nginx）分配到持久内存的空间地址，引起性能问题，建议您在启动Redis应用时将所有持久内存分配给Redis应用。

        示例命令如下：

        -   端口号6379、内存36 GiB（其中普通内存4 GiB、持久内存32 GiB）

            ```
            redis-server /etc/redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 8 --maxmemory 36G
            ```

        -   端口号6379、内存34 GiB（其中普通内存2 GiB、持久内存32 GiB）

            ```
            redis-server /etc/redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 16 --maxmemory 34G
            ```

        -   端口号6379、内存32 GiB（其中普通内存0 GiB、持久内存32 GiB）

            ```
            redis-server /etc/redis.conf --port 6379 --memory-alloc-policy only-pmem --maxmemory 32G
            ```


## 在使用CentOS系统的re6p实例上部署Redis应用

本示例中使用的配置如下：

-   实例规格：ecs.re6p-redis.2xlarge
-   镜像：CentOS 7.6

    **说明：** 请确保使用CentOS 7.6或更高版本。

-   Redis：Redis 4.0.14
-   memkind：memkind 1.10.1

1.  购买持久内存实例。

    具体操作，请参见[使用向导创建实例](/intl.zh-CN/实例/创建实例/使用向导创建实例.md)。请注意以下配置：

    -   **实例**：单击**x86计算**架构下的**内存型**分类，并选中名称为ecs.re6p-redis.2xlarge的实例规格。
    -   **镜像**：选择CentOS 7.6 64位。
2.  登录实例。

    具体操作，请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

3.  准备编译环境。

    1.  设置环境变量。

        ```
        export MEMKIND_DAX_KMEM_NODES=1
        ```

    2.  下载依赖包。

        ```
        yum -y install numactl-devel.x86_64
        ```

    3.  下载工具包。

        ```
        yum -y groupinstall 'Development Tools'
        ```

        **说明：** Development Tools包括gcc编译器等工具。

4.  准备Redis 4.0.14安装包。

    1.  下载安装包。

        ```
        wget https://github.com/redis-io/redis/archive/4.0.14.tar.gz
        ```

    2.  解压安装包。

        ```
        tar xzvf 4.0.14.tar.gz
        ```

5.  下载并安装为Redis应用使能持久内存的patch。

    1.  下载patch。

        ```
        wget https://github.com/redis/redis/compare/4.0.14...memKeyDB:4.0.14-devel.diff -O redis_4.0.14_eca56e845aa19d2e79e7c70207e860f8385541f9.patch
        ```

        **说明：** 关于如何下载更多Redis版本对应的patch，请参见[下载使能持久内存的patch](#section_7l0_0ys_dm0)。

    2.  切换到Redis 4.0.14安装目录。

        ```
        cd redis-4.0.14
        ```

    3.  安装patch。

        ```
        git apply --ignore-whitespace ../redis_4.0.14_eca56e845aa19d2e79e7c70207e860f8385541f9.patch
        ```

6.  准备memkind安装包。

    memkind是内存管理工具，用于分配管理持久内存。

    1.  下载memkind安装包。

        ```
        wget https://github.com/memkind/memkind/archive/v1.10.1-rc2.tar.gz
        ```

    2.  解压memkind安装包。

        ```
        tar xzvf v1.10.1-rc2.tar.gz
        ```

    3.  将memkind安装包移动到./deps/memkind/目录中。

        ```
        mv memkind-1.10.1-rc2/* ./deps/memkind/
        ```

7.  运行`ldd --version`查看glibc版本，并判断是否需要调整makefile。

    **说明：** 如果glibc版本低于2.17，请执行以下操作调整makefile。如果glibc版本等于或高于2.17，请跳过以下操作直接开始编译Redis 4.0.14。

    1.  切换到./deps/memkind/目录。

        ```
        cd ./deps/memkind/
        ```

    2.  下载patch。

        ```
        wget https://github.com/memKeyDB/memKeyDB/wiki/files/0001-Use-secure_getenv-when-possible.patch
        ```

    3.  安装patch。

        ```
        git apply --ignore-whitespace 0001-Use-secure_getenv-when-possible.patch
        ```

    4.  返回redis-4.0.14目录。

        ```
        cd /root/redis-4.0.14
        ```

8.  在redis-4.0.14目录中编译并安装Redis 4.0.14。

    1.  编译Redis 4.0.14。

        ```
        make clean;make distclean;make MALLOC=memkind -j 4
        ```

    2.  安装Redis 4.0.14。

        ```
        make install
        ```

9.  配置网卡多队列。

    网卡多队列可以帮助Redis应用获得更好的性能。

    1.  下载自动配置脚本ecs\_mq。

        ```
        wget https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/ecs_mq/ecs_mq_latest.tgz
        ```

    2.  解压脚本。

        ```
        tar -xzf ecs_mq_latest.tgz
        ```

    3.  更换工作路径。

        ```
        cd ecs_mq/
        ```

    4.  运行脚本。

        不同的镜像版本的命令格式不同，例如CentOS 7.6镜像运行`bash install.sh centos 7`。

        ```
        bash install.sh <系统名称> <系统主版本号>
        ```

    5.  启动服务。

        ```
        systemctl start ecs_mq
        ```

    6.  返回redis-4.0.14目录。

        ```
        cd /root/redis-4.0.14
        ```

10. 查看普通内存和持久内存的容量大小。

    1.  安装numactl。

        ```
        yum install -y numactl
        ```

    2.  查看普通内存和持久内存的容量大小。

        ```
        numactl -H
        ```

        **说明：** `node 0 free`为可分配给应用程序的普通内存容量，`node 1 free`为可分配给应用程序的持久内存容量。

        ![available-mem](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7756517161/p259154.png)

11. 启动Redis（配置默认使用的普通内存和持久内存容量）。

    **说明：** 为防止其他未经优化的应用（例如Nginx）分配到持久内存的空间地址，引起性能问题，建议您在启动Redis应用时将所有持久内存分配给Redis应用。

    示例命令如下：

    -   端口号6379、内存36 GiB（其中普通内存4 GiB、持久内存32 GiB）

        ```
        redis-server redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 8 --maxmemory 36G
        ```

    -   端口号6379、内存34 GiB（其中普通内存2 GiB、持久内存32 GiB）

        ```
        redis-server redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 16 --maxmemory 34G
        ```

    -   端口号6379、内存32 GiB（其中普通内存0 GiB、持久内存32 GiB）

        ```
        redis-server redis.conf --port 6379 --memory-alloc-policy only-pmem --maxmemory 32G
        ```


## 下载使能持久内存的patch

替换示例命令中的下载地址以及文件名中对应的版本号即可，例如下载Redis 6.0.5适用的patch的命令如下：

```
wget https://github.com/redis/redis/compare/6.0.5...memKeyDB:6.0.5-devel.diff -O redis_6.0.5_eca56e845aa19d2e79e7c70207e860f8385541f9.patch
```

目前支持的patch的下载地址如下所示：

-   Redis 6.0
    -   [https://github.com/redis/redis/compare/6.0.9...memKeyDB:6.0.9-devel.diff](https://github.com/redis/redis/compare/6.0.9...memKeyDB:6.0.9-devel.diff)
    -   [https://github.com/redis/redis/compare/6.0.5...memKeyDB:6.0.5-devel.diff](https://github.com/redis/redis/compare/6.0.5...memKeyDB:6.0.5-devel.diff)
    -   [https://github.com/redis/redis/compare/6.0.3...memKeyDB:6.0.3-devel.diff](https://github.com/redis/redis/compare/6.0.3...memKeyDB:6.0.3-devel.diff)
    -   [https://github.com/redis/redis/compare/6.0.0...memKeyDB:6.0.0-devel.diff](https://github.com/redis/redis/compare/6.0.0...memKeyDB:6.0.0-devel.diff)
-   Redis 5.0
    -   [https://github.com/redis/redis/compare/5.0.9...memKeyDB:5.0.9-devel.diff](https://github.com/redis/redis/compare/5.0.9...memKeyDB:5.0.9-devel.diff)
    -   [https://github.com/redis/redis/compare/5.0.2...memKeyDB:5.0.2-devel.diff](https://github.com/redis/redis/compare/5.0.2...memKeyDB:5.0.2-devel.diff)
    -   [https://github.com/redis/redis/compare/5.0.0...memKeyDB:5.0.0-devel.diff](https://github.com/redis/redis/compare/5.0.0...memKeyDB:5.0.0-devel.diff)
-   Redis 4.0
    -   [https://github.com/redis/redis/compare/4.0.14...memKeyDB:4.0.14-devel.diff](https://github.com/redis/redis/compare/4.0.14...memKeyDB:4.0.14-devel.diff)
    -   [https://github.com/redis/redis/compare/4.0.9...memKeyDB:4.0.9-devel.diff](https://github.com/redis/redis/compare/4.0.9...memKeyDB:4.0.9-devel.diff)
    -   [https://github.com/redis/redis/compare/4.0.2...memKeyDB:4.0.2-devel.diff](https://github.com/redis/redis/compare/4.0.2...memKeyDB:4.0.2-devel.diff)
    -   [https://github.com/redis/redis/compare/4.0.0...memKeyDB:4.0.0-devel.diff](https://github.com/redis/redis/compare/4.0.0...memKeyDB:4.0.0-devel.diff)
-   Redis 3.0
    -   [https://github.com/redis/redis/compare/3.2.12...memKeyDB:3.2.diff](https://github.com/redis/redis/compare/3.2.12...memKeyDB:3.2.diff)

**说明：** 如果您有其他版本的支持需求，请[提交工单](https://workorder-intl.console.aliyun.com/console.htm)。

