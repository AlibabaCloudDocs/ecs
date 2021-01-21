# Deploy Redis applications on re6p instances

You can run Redis applications on persistent memory optimized instances to reduce memory costs per GiB. To ensure performance, you must modify your Redis applications. To reduce your modification costs, Alibaba Cloud provides re6p instance types specially for Redis applications. You can deploy Redis applications on re6p instances by running several commands. In this topic, Alibaba Cloud Linux and CentOS are used to demonstrate how to deploy Redis applications on re6p instances.

The procedures described in this topic apply only to the following instance types:

-   ecs.re6p-redis.large
-   ecs.re6p-redis.xlarge
-   ecs.re6p-redis.2xlarge
-   ecs.re6p-redis.13xlarge

**Note:** ecs.re6p-redis.<nx\>large are instance types that are specially provided for Redis applications and support only persistent memory used as memory.

If you use other operating systems to deploy Redis applications, make sure that you use one of the following image versions:

-   Alibaba Cloud Linux 2
-   CentOS 7.6 or later
-   Ubuntu 18.10 or later
-   SUSE Linux 12 SP4 or later

**Note:** The reliability of data stored in persistent memory depends on the reliability of persistent memory devices and the physical servers to which these devices are attached. This increases risks of single points of failure. To ensure the reliability of application data, we recommend that you implement data redundancy at the application layer and use cloud disks for long-term data storage.

## Deploy Redis applications on an re6p instance that runs Alibaba Cloud Linux

Alibaba Cloud Linux is specially tuned for Redis applications. Redis applications deployed on community operating systems outperform those deployed on Alibaba Cloud Linux by more than 20%.

Alibaba Cloud Linux integrates Redis 6.0.5 and Redis 3.2.12. You can also manually deploy Redis of other versions. In this way, the overall performance of Redis applications can also be improved by more than 20%.

The following configurations are used in this example:

-   Instance type: ecs.re6p-redis.2xlarge
-   Image: Alibaba Cloud Linux 2.1903 LTS 64-bit

1.  Purchase a persistent memory optimized instance.

    For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md). Take note of the following configurations:

    -   **Instance Type**: Set Architecture to **x86-Architecture**, set Category to **Memory Optimized**, and then select the ecs.re6p-redis.2xlarge instance type.
    -   **Image**: Select Alibaba Cloud Linux 2.1903 LTS 64-bit.
2.  Log on to the instance.

    For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

3.  Deploy Redis applications.

    -   Run the following commands to deploy Redis 6.0.5:

        ```
        yum install -y alinux-release-experimentals
        yum install -y redis-6.0.5
        ```

    -   Run the following commands to deploy Redis 3.2.12:

        ```
        yum install -y alinux-release-experimentals
        yum install –y redis-3.2.12
        ```

4.  Configure network interface controller \(NIC\) multi-queue.

    NIC multi-queue helps improve the performance of Redis applications.

    1.  Download the ecs\_mq automatic configuration script package.

        ```
        wget https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/ecs_mq/ecs_mq_latest.tgz
        ```

    2.  Decompress the script package.

        ```
        tar -xzf ecs_mq_latest.tgz
        ```

    3.  Change the working path.

        ```
        cd ecs_mq/
        ```

    4.  Run the extracted script file.

        The command format varies with image versions. For example, Alibaba Cloud Linux 2.1903 images use the `bash install.sh aliyun 2` format.

        ```
        bash install.sh <Operating system name> <Major version number of the operating system>
        ```

    5.  Start the service.

        ```
        systemctl start ecs_mq
        ```

5.  Configure the default sizes of DRAM and persistent memory for the Redis service.

    **Note:** If applications such as NGINX that are not optimized are assigned memory addresses of persistent memory, performance problems may arise. To prevent the performance problems, we recommend that you allocate all persistent memory to Redis applications when you start the Redis applications.

    Sample commands:

    -   To set the port number to 6379, the DRAM to 4 GiB, and the persistent memory to 32 GiB, run the following command:

        ```
        export MEMKIND_DAX_KMEM_NODES=1
        redis-server /etc/redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 8 --maxmemory 36G
        ```

    -   To set the port number to 6379, the DRAM to 2 GiB, and the persistent memory to 32 GiB, run the following command:

        ```
        export MEMKIND_DAX_KMEM_NODES=1
        redis-server /etc/redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 16 --maxmemory 34G
        ```

    -   To set the port number to 6379, the DRAM to 0 GiB, and the persistent memory to 32 GiB, run the following command:

        ```
        export MEMKIND_DAX_KMEM_NODES=1
        redis-server /etc/redis.conf --port 6379 --memory-alloc-policy only-pmem --maxmemory 32G
        ```


## Deploy Redis applications on an re6p instance that runs CentOS

The following configurations are used in this example:

-   Instance type: ecs.re6p-redis.2xlarge
-   Image: CentOS 7.6

    **Note:** Make sure that CentOS 7.6 or later is used.

-   Redis: Redis 4.0.14
-   memkind: memkind 1.10.1

1.  Purchase a persistent memory optimized instance.

    For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md). Take note of the following configurations:

    -   **Instance Type**: Set Architecture to **x86-Architecture**, set Category to **Memory Optimized**, and then select the ecs.re6p-redis.2xlarge instance type.
    -   **Image**: Select CentOS 7.6 64-bit.
2.  Log on to the instance.

    For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

3.  Prepare the compiling environment.

    ```
    export MEMKIND_DAX_KMEM_NODES=1
    yum -y install numactl-devel.x86_64
    yum -y groupinstall 'Development Tools'
    ```

    **Note:** Development tools include the GCC compiler.

4.  Download the Redis installation package.

    ```
    wget https://github.com/redis-io/redis/archive/4.0.14.tar.gz
    tar xzvf 4.0.14.tar.gz
    ```

5.  Download and install patches that enable Redis applications to use persistent memory.

    For more information, see [Download patches that enable Redis applications to use persistent memory](#section_7l0_0ys_dm0).

    ```
    wget https://github.com/redis/redis/compare/4.0.14...memKeyDB:4.0.14-devel.diff -O redis_4.0.14_eca56e845aa19d2e79e7c70207e860f8385541f9.patch
    cd redis-4.0.14
    git apply --ignore-whitespace ../redis_4.0.14_eca56e845aa19d2e79e7c70207e860f8385541f9.patch
    ```

6.  Install memkind.

    memkind is a memory management tool used to allocate and manage persistent memory.

    ```
    wget https://github.com/memkind/memkind/archive/v1.10.1-rc2.tar.gz
    tar xzvf v1.10.1-rc2.tar.gz
    mv memkind-1.10.1-rc2/* ./deps/memkind/
    ```

7.  Adjust Makefile if the version of glibc is earlier than 2.17.

    ```
    cd ./deps/memkind/
    wget https://github.com/memKeyDB/memKeyDB/wiki/files/0001-Use-secure_getenv-when-possible.patch
    git apply --ignore-whitespace 0001-Use-secure_getenv-when-possible.patch
    ```

8.  Perform compilation in the redis-4.0.14 directory.

    **Note:** If you do not need to switch to the ./deps/memkind/ directory to adjust Makefile, you are still in the redis-4.0.14 directory. In this case, you do not need to run the `cd .. /..` command to switch the directory.

    ```
    cd .. /..
    make clean;make distclean;make MALLOC=memkind -j 4
    make install
    ```

9.  Configure NIC multi-queue.

    NIC multi-queue helps improve the performance of Redis applications.

    1.  Download the ecs\_mq automatic configuration script package.

        ```
        wget https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/ecs_mq/ecs_mq_latest.tgz
        ```

    2.  Decompress the script package.

        ```
        tar -xzf ecs_mq_latest.tgz
        ```

    3.  Change the working path.

        ```
        cd ecs_mq/
        ```

    4.  Run the extracted script file.

        The command format varies with image versions. For example, CentOS 7.6 images use the `bash install.sh centos 7` format.

        ```
        bash install.sh <Operating system name> <Major version number of the operating system>
        ```

    5.  Start the service.

        ```
        systemctl start ecs_mq
        ```

10. Configure the default sizes of DRAM and persistent memory for the Redis service.

    **Note:** If applications such as NGINX that are not optimized are assigned memory addresses of persistent memory, performance problems may arise. To prevent the performance problems, we recommend that you allocate all persistent memory to Redis applications when you start the Redis applications.

    Sample commands:

    -   To set the port number to 6379, the DRAM to 4 GiB, and the persistent memory to 32 GiB, run the following command:

        ```
        redis-server redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 8 --maxmemory 36G
        ```

    -   To set the port number to 6379, the DRAM to 2 GiB, and the persistent memory to 32 GiB, run the following command:

        ```
        redis-server redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 16 --maxmemory 34G
        ```

    -   To set the port number to 6379, the DRAM to 0 GiB, and the persistent memory to 32 GiB, run the following command:

        ```
        redis-server redis.conf --port 6379 --memory-alloc-policy only-pmem --maxmemory 32G
        ```


## Download patches that enable Redis applications to use persistent memory

Replace the download URL and the version number of the file name in the sample command. For example, run the following command to download patches suitable for Redis 6.0.5:

```
wget https://github.com/redis/redis/compare/6.0.5...memKeyDB:6.0.5-devel.diff -O redis_6.0.5_eca56e845aa19d2e79e7c70207e860f8385541f9.patch
```

The following section shows the download URLs for supported patches:

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

**Note:** If you want to use other versions of Redis, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

