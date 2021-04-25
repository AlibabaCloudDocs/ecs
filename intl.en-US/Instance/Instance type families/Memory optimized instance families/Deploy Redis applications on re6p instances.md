# Deploy Redis applications on re6p instances

You can run Redis applications on persistent memory optimized instances to reduce memory costs per GiB. To ensure performance, you must modify your Redis applications. To reduce your modification costs, Alibaba Cloud provides re6p instance types for Redis applications. You can deploy Redis applications on re6p instances by running several commands. In this topic, Alibaba Cloud Linux 2 and CentOS are used to demonstrate how to deploy Redis applications on re6p instances.

The procedures described in this topic apply only to the following instance types:

-   ecs.re6p-redis.large
-   ecs.re6p-redis.xlarge
-   ecs.re6p-redis.2xlarge
-   ecs.re6p-redis.13xlarge

**Note:** ecs.re6p-redis.<nx\>large indicates instance types that are provided for Redis applications and support only persistent memory used as memory.

If you deploy Redis applications in other operating systems, make sure that you use one of the following image versions:

-   Alibaba Cloud Linux 2
-   CentOS 7.6 or later
-   Ubuntu 18.10 or later
-   SUSE Linux 12 SP4 or later

## Deploy Redis applications on an re6p instance that runs Alibaba Cloud Linux 2

Alibaba Cloud Linux 2 is tuned for Redis applications. Redis applications deployed on Alibaba Cloud Linux 2 outperform those deployed on community-supported Linux operating systems by more than 20%.

Alibaba Cloud Linux 2 has the built-in YUM repositories of Redis 6.0.5 and Redis 3.2.12. You can run the yum install command to deploy Redis 6.0.5 and Redis 3.2.12. You can also manually deploy Redis of other versions. For more information, see [Deploy Redis applications on an re6p instance that runs CentOS](#section_gx2_rzq_8rk).

The following configurations are used in this example:

-   Instance type: ecs.re6p-redis.2xlarge
-   Image: Alibaba Cloud Linux 2.1903 LTS 64-bit

1.  Purchase a persistent memory optimized instance.

    For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md). Take note of the following configurations:

    -   **Instance Type**: Set Architecture to **x86-Architecture**, set Category to **Memory Optimized**, and then select the ecs.re6p-redis.2xlarge instance type.
    -   **Image**: Select Alibaba Cloud Linux 2.1903 LTS 64-bit.
2.  Log on to the instance.

    For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

3.  Install the Alibaba Cloud experimentals repository.

    ```
    yum install -y alinux-release-experimentals
    ```

4.  Deploy Redis applications.

    -   Run the following commands to deploy Redis 6.0.5:

        ```
        yum install -y redis-6.0.5
        ```

    -   Run the following commands to deploy Redis 3.2.12:

        ```
        yum install -y redis-3.2.12
        ```

5.  Configure network interface controller \(NIC\) multi-queue.

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

    4.  Run the script.

        The command format varies with image versions. For example, Alibaba Cloud Linux 2.1903 images use `bash install.sh aliyun 2`.

        ```
        bash install.sh <Operating system name> <Major version number of the operating system>
        ```

    5.  Start the service.

        ```
        systemctl start ecs_mq
        ```

6.  Check the available amounts of regular memory and persistent memory.

    1.  Install numactl.

        ```
        yum install -y numactl
        ```

    2.  Check the available amounts of regular memory and persistent memory.

        ```
        numactl -H
        ```

        **Note:** `node 0 free` indicates the amount of regular memory available for use by applications. `node 1 free` indicates the amount of persistent memory available for use by applications.

        ![available-mem](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8668988161/p259154.png)

7.  Start the Redis service.

    1.  Set environment variables.

        ```
        export MEMKIND_DAX_KMEM_NODES=1
        ```

    2.  Start Redis and configure the default amounts of regular memory and persistent memory allocated to Redis.

        **Note:** If unoptimized applications such as NGINX are assigned memory addresses of persistent memory, performance problems may arise. To prevent the problems, we recommend that you allocate all persistent memory to Redis applications when you start the applications.

        Sample commands:

        -   Run the following command to set the port number to 6379, the allocated amount of regular memory to 4 GiB, and the allocated amount of persistent memory to 32 GiB:

            ```
            redis-server /etc/redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 8 --maxmemory 36G
            ```

        -   Run the following command to set the port number to 6379, the allocated amount of regular memory to 2 GiB, and the allocated amount of persistent memory to 32 GiB:

            ```
            redis-server /etc/redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 16 --maxmemory 34G
            ```

        -   Run the following command to set the port number to 6379, the allocated amount of regular memory to 0 GiB, and the allocated amount of persistent memory to 32 GiB:

            ```
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

    1.  Set environment variables.

        ```
        export MEMKIND_DAX_KMEM_NODES=1
        ```

    2.  Download the dependency.

        ```
        yum -y install numactl-devel.x86_64
        ```

    3.  Download the toolkit.

        ```
        yum -y groupinstall 'Development Tools'
        ```

        **Note:** The toolkit includes the GCC compiler.

4.  Prepare the Redis 4.0.14 installation package.

    1.  Download the installation package.

        ```
        wget https://github.com/redis-io/redis/archive/4.0.14.tar.gz
        ```

    2.  Decompress the package.

        ```
        tar xzvf 4.0.14.tar.gz
        ```

5.  Download and install the patch that enables Redis applications to use persistent memory.

    1.  Download the patch.

        ```
        wget https://github.com/redis/redis/compare/4.0.14...memKeyDB:4.0.14-devel.diff -O redis_4.0.14_eca56e845aa19d2e79e7c70207e860f8385541f9.patch
        ```

        **Note:** For information about how to download patches for more Redis versions, see [Download patches that enable Redis applications to use persistent memory](#section_7l0_0ys_dm0).

    2.  Switch to the directory where Redis 4.0.14 is installed.

        ```
        cd redis-4.0.14
        ```

    3.  Install the patch.

        ```
        git apply --ignore-whitespace ../redis_4.0.14_eca56e845aa19d2e79e7c70207e860f8385541f9.patch
        ```

6.  Prepare the memkind installation package.

    memkind is a memory management tool used to allocate and manage persistent memory.

    1.  Download the memkind installation package.

        ```
        wget https://github.com/memkind/memkind/archive/v1.10.1-rc2.tar.gz
        ```

    2.  Decompress the memkind installation package.

        ```
        tar xzvf v1.10.1-rc2.tar.gz
        ```

    3.  Move the memkind installation package to the ./deps/memkind/ path.

        ```
        mv memkind-1.10.1-rc2/* ./deps/memkind/
        ```

7.  Run the `ldd --version` command to view the version of glibc and determine whether to adjust Makefile.

    **Note:** If the version of glibc is earlier than 2.17, perform the following operations to adjust Makefile. If the version of glibc is not earlier than 2.17, skip the following operations and compile Redis 4.0.14.

    1.  Switch to the ./deps/memkind/ path.

        ```
        cd ./deps/memkind/
        ```

    2.  Download the patch.

        ```
        wget https://github.com/memKeyDB/memKeyDB/wiki/files/0001-Use-secure_getenv-when-possible.patch
        ```

    3.  Install the patch.

        ```
        git apply --ignore-whitespace 0001-Use-secure_getenv-when-possible.patch
        ```

    4.  Go back to the redis-4.0.14 directory.

        ```
        cd /root/redis-4.0.14
        ```

8.  Compile and install Redis 4.0.14 in the redis-4.0.14 directory.

    1.  Compile Redis 4.0.14.

        ```
        make clean;make distclean;make MALLOC=memkind -j 4
        ```

    2.  Install Redis 4.0.14.

        ```
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

    4.  Run the script.

        The command format varies with image versions. For example, CentOS 7.6 images use `bash install.sh centos 7`.

        ```
        bash install.sh <Operating system name> <Major version number of the operating system>
        ```

    5.  Start the service.

        ```
        systemctl start ecs_mq
        ```

    6.  Go back to the redis-4.0.14 directory.

        ```
        cd /root/redis-4.0.14
        ```

10. Check the available amounts of regular memory and persistent memory.

    1.  Install numactl.

        ```
        yum install -y numactl
        ```

    2.  Check the available amounts of regular memory and persistent memory.

        ```
        numactl -H
        ```

        **Note:** `node 0 free` indicates the amount of regular memory available for use by applications. `node 1 free` indicates the amount of persistent memory available for use by applications.

        ![available-mem](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8668988161/p259154.png)

11. Start Redis and configure the default amounts of regular memory and persistent memory allocated to Redis.

    **Note:** If unoptimized applications such as NGINX are assigned memory addresses of persistent memory, performance problems may arise. To prevent the problems, we recommend that you allocate all persistent memory to Redis applications when you start the applications.

    Sample commands:

    -   Run the following command to set the port number to 6379, the allocated amount of regular memory to 4 GiB, and the allocated amount of persistent memory to 32 GiB:

        ```
        redis-server redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 8 --maxmemory 36G
        ```

    -   Run the following command to set the port number to 6379, the allocated amount of regular memory to 2 GiB, and the allocated amount of persistent memory to 32 GiB:

        ```
        redis-server redis.conf --port 6379 --memory-alloc-policy ratio --dram-pmem-ratio 1 16 --maxmemory 34G
        ```

    -   Run the following command to set the port number to 6379, the allocated amount of regular memory to 0 GiB, and the allocated amount of persistent memory to 32 GiB:

        ```
        redis-server redis.conf --port 6379 --memory-alloc-policy only-pmem --maxmemory 32G
        ```


## Download patches that enable Redis applications to use persistent memory

In the sample command, replace the download URL and the version number of the file name. For example, run the following command to download patches suitable for Redis 6.0.5:

```
wget https://github.com/redis/redis/compare/6.0.5...memKeyDB:6.0.5-devel.diff -O redis_6.0.5_eca56e845aa19d2e79e7c70207e860f8385541f9.patch
```

The following section lists the download URLs for supported patches:

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

