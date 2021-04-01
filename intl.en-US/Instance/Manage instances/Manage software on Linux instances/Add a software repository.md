# Add a software repository

In most cases, software packages for Linux are stored in software repositories. After you add a software repository, you can use the package management tool provided by Linux to search for, install, and update software applications in the repository. This topic describes how to add software repositories to different Linux distributions. Alibaba Cloud software repositories are used in the following examples.

All users have free access to Alibaba Cloud software repositories, regardless of whether the users have Alibaba Cloud accounts. You can go to the [Alibaba Open Source Image Site](https://opsx.alibaba.com) to obtain the software repository of your Linux distribution.

## Add a software repository to a CentOS instance

A CentOS 7 instance is used in this example. Operations may vary based on the version of your operating system.

1.  Connect to a CentOS 7 instance. For more information, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to back up the original Alibaba Cloud software repository:

    ```
    sudo mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
    ```

3.  Run one of the following commands to add the original software repository to the CentOS 7 instance:

    -   ```
sudo wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

    -   ```
sudo curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

    **Note:**

    -   To view the instructions on how to add an Alibaba Cloud software repository to an instance that runs another version of CentOS, go to the [Alibaba Open Source Image Site](https://opsx.alibaba.com) and click `centos`.
    -   To add a software repository that is not from Alibaba Cloud, replace `http://mirrors.aliyun.com/repo/Centos-7.repo` in the preceding commands with the URL of the software repository that you want to add.
4.  Run the following command to generate a local cache for fast search and installation of software:

    ```
    sudo yum clean all && sudo yum makecache
    ```

5.  Run the `sudo yum repolist` command to check whether the software repository is added.

    If the output shown in the following figure appears, the software repository is added to the CentOS 7 instance.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3013909951/p48248.png)


## Add a software repository to an Ubuntu instance

An Ubuntu 18.04 instance is used in this example. Operations may vary based on the version of your operating system.

1.  Connect to an Ubuntu 18.04 instance. For more information, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to back up the original Alibaba Cloud software repository:

    ```
    sudo cp /etc/apt/sources.list /etc/apt/sources.list.bakup
    ```

3.  Run the `sudo vim /etc/apt/sources.list` command to open the source.list file and add the following information to the file. For more information, see [Use the Vim editor](/intl.en-US/Tutorials/Use the Vim editor.md).

    ```
    deb http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic main restricted universe multiverse
    deb-src http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic main restricted universe multiverse
    deb http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-security main restricted universe multiverse
    deb-src http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-security main restricted universe multiverse
    deb http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-updates main restricted universe multiverse
    deb-src http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-updates main restricted universe multiverse
    deb http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-proposed main restricted universe multiverse
    deb-src http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-proposed main restricted universe multiverse
    deb http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-backports main restricted universe multiverse
    deb-src http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-backports main restricted universe multiverse
    ```

    **Note:**

    -   To view the instructions on how to add an Alibaba Cloud software repository to an instance that runs another version of Ubuntu, go to the [Alibaba Open Source Image Site](https://opsx.alibaba.com) and click `ubuntu`. To add an Alibaba Cloud software repository to an ECS instance, replace `http://mirrors.aliyun.com/ubuntu/` on the Help page with `http://mirrors.cloud.aliyuncs.com/ubuntu`. This helps reduce data transfer costs.
    -   To add a software repository that is not from Alibaba Cloud, replace the URL on the Help page with the URL of the software repository that you want to add.
4.  Run the `sudo apt-get update` command to update the information about the software packages in the software repository.


## Add a software repository to a Debian instance

A Debian 8.9 instance is used in this example. Operations may vary based on the version of your operating system.

1.  Connect to a Debian 8.9 instance. For more information, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to back up the original Alibaba Cloud software repository:

    ```
    sudo cp /etc/apt/sources.list /etc/apt/sources.list.bakup
    ```

3.  Run the `sudo vim/etc/apt/sources.list` command to open the source.list file and add the following information to the file. For more information, see [Use the Vim editor](/intl.en-US/Tutorials/Use the Vim editor.md).

    ```
    deb http://mirrors.cloud.aliyuncs.com/debian/ jessie main non-free contrib
    deb http://mirrors.cloud.aliyuncs.com/debian/ jessie-proposed-updates main non-free contrib
    deb-src http://mirrors.cloud.aliyuncs.com/debian/ jessie main non-free contrib
    deb-src http://mirrors.cloud.aliyuncs.com/debian/ jessie-proposed-updates main non-free contrib
    ```

    **Note:**

    -   To view the instructions on how to add an Alibaba Cloud software repository to an instance that runs another version of Debian, go to the [Alibaba Open Source Image Site](https://opsx.alibaba.com) and click `debian`. To add an Alibaba Cloud software repository to an ECS instance, replace `http://mirrors.aliyun.com/debian/` on the Help page with `http://mirrors.cloud.aliyuncs.com/debian/`. This helps reduce data transfer costs.
    -   To add a software repository that is not from Alibaba Cloud, replace the URL on the Help page with the URL of the software repository that you want to add.
4.  Run the `sudo apt-get update` command to update the information about the software packages in the software repository.


## Add a software repository to a Fedora instance

1.  Connect to a Fedora instance. For more information, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to back up the original Alibaba Cloud software repository:

    ```
    sudo mv /etc/yum.repos.d/fedora.repo /etc/yum.repos.d/fedora.repo.backup
    sudo mv /etc/yum.repos.d/fedora-updates.repo /etc/yum.repos.d/fedora-updates.repo.backup
    ```

3.  Run one of the following commands to add the original Fedora software repository of Alibaba Cloud to the Fedora instance:

    -   ```
sudo wget -O /etc/yum.repos.d/fedora.repo http://mirrors.aliyun.com/repo/fedora.repo
```

    -   ```
sudo curl -o /etc/yum.repos.d/fedora.repo http://mirrors.aliyun.com/repo/fedora.repo
```

    **Note:** To add a Fedora software repository that is not from Alibaba Cloud, replace `http://mirrors.aliyun.com/repo/fedora.repo` in the preceding commands with the URL of the software repository that you want to add.

4.  Run one of the following commands to add the Fedora-updates software repository of Alibaba Cloud to the Fedora instance:

    -   ```
sudo wget -O /etc/yum.repos.d/fedora-updates.repo http://mirrors.aliyun.com/repo/fedora-updates.repo
```

    -   ```
sudo curl -o /etc/yum.repos.d/fedora-updates.repo http://mirrors.aliyun.com/repo/fedora-updates.repo
```

        **Note:** To add a Fedora-updates software repository that is not from Alibaba Cloud, replace `http://mirrors.aliyun.com/repo/fedora-updates.repo` in the preceding commands with the URL of the repository that you want to add.

5.  Run the following command to generate a local cache:

    ```
    sudo yum clean all && sudo yum makecache
    ```


After you add a software repository, you can install software packages. For more information, see [Install software packages](/intl.en-US/Instance/Manage instances/Manage software on Linux instances/Install software packages.md).

