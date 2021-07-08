# 使用Enclave构建机密计算环境

本文介绍如何使用阿里云虚拟化Enclave创建一个可信的隔离空间，从而保护您的应用程序和数据的安全。

数据一般分为三种形态：静态数据、传输中的数据以及使用中的数据。前两者可以通过加密等方式来保障数据安全；而使用中的数据的安全性保障十分困难，目前一般使用机密计算（Confidential Computing）来保护使用中的数据的安全性。

阿里云虚拟化Enclave在ECS实例内部提供一个可信的隔离空间，将合法软件的安全操作封装在一个Enclave中，保障您的代码和数据的机密性与完整性，不受恶意软件的攻击。

**说明：** 阿里云虚拟化Enclave正在邀测中。您可以前往[产品详情页](https://www.aliyun.com/daily-act/ecs/aliyun-enclave)申请使用。

阿里云虚拟化Enclave适用于对敏感和机密数据有强保护需求的业务，例如金融服务、互联网、医疗等。

## Enclave的工作原理

使用阿里云虚拟化Enclave构建机密计算环境的工作原理，是在ECS实例（即主VM）内切分计算资源（包括vCPU和内存），创建一个Enclave VM（简称EVM）作为可信执行环境。EVM的安全性保障体现在以下几方面：

-   由底层虚拟化技术提供安全隔离，EVM和主VM之间隔离，并且和其他ECS实例也隔离。
-   EVM运行独立的、定制化的可信操作系统，没有持久化存储、交互式连接或外部网络通路，仅允许通过本地安全信道（基于vsock）与主VM进行通信，最大程度缩小攻击面。您可以将涉及机密数据的应用放入EVM中运行，通过安全调用的形式与运行在主VM上的应用进行交互。

阿里云虚拟化Enclave的工作原理图如下所示。

![enclave原理图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3916902161/p237059.png)

阿里云虚拟化Enclave提供的安全性由多个方面结合实现。底层基于带有TPM/TCM芯片的第三代神龙架构，且为EVM提供vTPM/vTCM设备来增强其安全性和可信能力；上层提供高兼容性的SDK，方便您快速搭建Enclave环境并使用。在可信证明能力方面，您可以对运行在机密执行环境中的代码进行验证，例如借助SDK，机密应用可在运行时生成证明材料（包括平台、应用信息、签名等），再通过远程证明服务端（可结合KMS）验证证明材料的有效性。当主VM切分资源给EVM，并且EVM开始运行时，底层会执行资源访问隔离，确保主VM无法访问这些已经切分出去的vCPU或内存资源，保障EVM的正常运行和私密性。

阿里云虚拟化Enclave功能的架构图如下所示。

![enclave架构图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9345962161/p237060.png)

## 使用限制

-   仅g7、c7、r7支持阿里云虚拟化Enclave。
-   每台ECS实例只允许创建一个Enclave。
-   使用Enclave前您必须至少保留一个处理器物理核以及部分内存给主VM使用，剩余的处理器和内存资源可以灵活地分配给Enclave。如果您开启了超线程，则代表保留了属于一个物理核的两个处理器超线程，因此启用Enlave特性的ECS实例至少需要具备4 vCPU。

其他通用限制，请参见[使用限制](/cn.zh-CN/产品简介/使用限制.md)。

## 通过工具集使用Enclave

1.  安装Enclave Runtime工具集。

    Enclave Runtime工具集负责在主VM上管理Enclave的生命周期，包括Enclave的启动和终止。您可以通过以下任一方式安装：

    -   在创建ECS实例时勾选**Enclave**，自动安装Enclave Runtime工具集。

        ![随实例安装](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9345962161/p240198.png)

    -   在创建ECS实例后，运行以下命令，在主VM中安装Enclave Runtime工具集。

        ```
        sudo rpmkeys --import http://mirrors.aliyun.com/epel/RPM-GPG-KEY-EPEL-7
        sudo yum install -y alinux-release-experimentals
        sudo yum install -y https://enclave.oss-cn-hangzhou.aliyuncs.com/de-platform-runtime-0.1.0-1.2.al7.x86_64.rpm
        ```

    安装Enclave Runtime后，本地服务会尝试自动拉起Enclave，默认的Enclave镜像存储于/usr/local/share/dragonfly/image.bin，您可以修改配置文件/etc/enclave.conf来变更镜像存储所在路径。配置文件还提供了更多的配置选项，包括分配给Enclave的vCPU和内存资源等。

2.  初次手动安装后，运行以下命令将Enclave镜像下载保存到本地。

    ```
    wget -O /usr/local/share/dragonfly/image.bin \
      https://enclave-cn-shenzhen.oss-cn-shenzhen.aliyuncs.com/download/linux/enclave_image/x86_64/0.1.0/image-0.1.0.bin
    ```

3.  运行systemctl命令，对Enclave进行操作。

    ```
    systemctl status de_platform_service # 查看运行状态
    systemctl start de_platform_service # 启动服务
    systemctl restart de_platform_service # 重启服务
    systemctl stop de_platform_service # 关闭服务
    ```


## 通过SDK使用Enclave

阿里云虚拟化Enclave提供了SDK，让您在启用了Enclave的ECS实例上开发自己的应用。阿里云虚拟化Enclave还提供了一组与SGX-SDK兼容的API接口定义和代码库，如果您已经有SGX应用，则只需经过少量迁移工作即可将应用运行在Enclave平台上。

1.  在开发环境中准备以下Dockerfile文件。

    ```
    FROM registry.cn-hangzhou.aliyuncs.com/alinux/aliyunlinux
    RUN rpmkeys --import http://mirrors.aliyun.com/epel/RPM-GPG-KEY-EPEL-7 \
        && yum install -y alinux-release-experimentals \
        && yum install -y devtoolset-9 wget openssl-devel zlib-devel patch git cmake3 \
          https://enclave.oss-cn-hangzhou.aliyuncs.com/de-platform-runtime-0.1.0-1.2.al7.x86_64.rpm \
          https://enclave.oss-cn-hangzhou.aliyuncs.com/teesdk-0.1.0-1.1.al7.x86_64.rpm \
        && yum clean all -y \
        && wget -O /devtoolset9_enable.sh \
          https://enclave.oss-cn-hangzhou.aliyuncs.com/devtoolset9_enable.sh \
        && chmod +x /devtoolset9_enable.sh
    WORKDIR /opt/app-root/src
    ENTRYPOINT ["/devtoolset9_enable.sh"]
    ```

2.  运行以下命令，利用docker创建Enclave镜像。

    ```
    docker build -t deenclave/sdk-builder .
    ```

    执行成功后，自动生成名为deenclave/sdk-builder的镜像。您只需使用该镜像，即可进行DE Enclave的应用构建。阿里云提供了[SDK示例](#section_gem_b9o_bg2)供您参考。


## SDK示例一：启动容器构建应用

阿里云提供了SDK示例程序，位于/opt/alibaba/teesdk/desdk/examples/SampleMath。该示例程序接收外部输入的两个平面坐标点，并在Enclave内计算两点之间的直线距离，最后将计算结果输出至控制台。您可以按照以下步骤完成示例操作。

1.  运行以下命令，通过构建的docker镜像deenclave/sdk-builder启动容器。

    ```
    docker run -it \
      -v /opt/alibaba/teesdk/desdk/examples/SampleMath:/opt/app-root/src:z \
      deenclave/sdk-builder
    ```

2.  在启动后的容器实例内，运行以下命令配置环境变量。

    ```
    source /opt/alibaba/teesdk/desdk/environment
    ```

3.  在启动后的容器实例内，运行cmake命令对示例代码执行构建。

    ```
    cmake3 -B build && \
    cmake3 --build build
    ```

    构建成功后，应用和Enclave所在路径分别为/opt/app-root/src/build/SampleMath/App/app和/opt/app-root/src/build/SampleMath/Enclave/enclave.signed.so。

4.  将应用上传至主实例。

5.  在ECS主VM上启动Enclave，并执行示例代码SampleMath，然后查看执行结果。

    ```
    [root@AliYun ~]# ./app
    A(3,4) -> B(1,8) -> 4.47214
    A(6,9) -> B(6,2) -> 7
    A(3,3) -> B(7,5) -> 4.47214
    ```


## SDK示例二：通过Attestation生成证明材料

Attestation是一个认证的过程，您可以通过它来确保运行在Enclave中的镜像、操作系统和应用程序代码没有被修改或篡改。您可以在自己的Enclave应用代码内调用SDK提供的API接口生成证明材料，并将证明材料上传至远程证明服务进行验证，远程证明服务会将验证结果返回给调用者。

阿里云提供了以下示例，您可以使用与[SDK示例一](#section_gem_b9o_bg2)中SampleMath相同的方式构建并运行这些示例。

-   生成证明材料的示例程序，位置在/opt/alibaba/teesdk/desdk/examples/QuoteGenerationSample。
-   验证证明材料的示例程序，位置在/opt/alibaba/teesdk/desdk/examples/QuoteVerificationSample。

