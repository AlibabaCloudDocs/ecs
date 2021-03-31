# Build a confidential computing environment by using Enclave

This topic describes how to create a trusted isolation space by using the Enclave feature to protect your applications and data.

Typically, data is classified into three states: data at rest, data in transit, and data in use. Data at rest and data in transit can be protected through encryption, but it is very difficult to ensure security for data in use. Typically, confidential computing is used to secure data in use.

Alibaba Cloud provides the Enclave feature for security-enhanced instances. This feature provides a trusted isolation space inside ECS instances and encapsulates the security operations of legitimate software within an enclave to protect the confidentiality and integrity of your code and data against attacks by malware.

**Note:** The Enclave feature is in invitational preview. If you want to use this feature, go to the [product details page](https://www.aliyun.com/daily-act/ecs/aliyun-enclave).

The Enclave feature is applicable to businesses in industries such as finance, Internet, and healthcare that require strong protection for sensitive and confidential data.

## How Enclave works

Computing resources \(including vCPUs and memory\) are split within an ECS instance \(the primary VM\) and an Enclave VM \(EVM\) is created as a trusted execution environment. The security of the EVM is ensured in the following aspects:

-   The underlying virtualization technology provides security isolation. The EVM is isolated from the primary VM as well as other ECS instances.
-   The EVM runs an independent, customized, and trusted operating system. The EVM has no persistent storage, interactive connections, or external network channels, and allows communication with the primary VM only by using a local secure channel \(based on vsock\) to ensure a minimal attack surface. You can put applications that involve confidential data into the EVM for running, and make secure calls to interact with the applications that run within the primary VM.

The security provided by Alibaba Cloud Enclave is implemented in multiple aspects. At the underlying layer, the third-generation SHENLONG architecture that uses TPM or TCM chips provides vTPM or vTCM devices for the EVM to enhance security and trusted capabilities. At the upper layer, highly compatible SDKs are provided so that you can quickly build an Enclave environment for use. To verify the trusted capabilities, you can verify the code running in the confidential execution environment, such as by using SDKs. Confidential applications can generate attestation materials \(including the platform, application information, and signatures\) at runtime, and then verify the attestation materials by using the remote attestation server \(with reference to KMS\). When the primary VM splits resources to the EVM and the EVM starts to run, the underlying layer performs resource access isolation to ensure that the primary VM cannot access these split vCPU or memory resources. This ensures the normal operation and privacy of the EVM.

## Limits

-   You can create only one enclave for each security-enhanced ECS instance.
-   Before you use an enclave, you must reserve at least one processor core and a portion of the memory for the primary VM. The remaining processor and memory resources can be flexibly allocated to the enclave. If hyper-threading is enabled, two processor hyper-threads that belong to one physical core are reserved.

For other general limits, see [Limits](/intl.en-US/Product Introduction/Limits.md).

## Use an enclave by using a toolset

1.  Install the Enclave Runtime toolset.

    The Enclave Runtime toolset manages the lifecycle of enclaves on the primary VM, including the startup and termination of enclaves. You can use one of the following methods to install the Enclave Runtime toolset:

    -   When you are creating an ECS instance, select **Enclave**. The Enclave Runtime toolset is automatically installed.

        ![Install the Enclave Runtime toolset along with the instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8244334161/p240198.png)

    -   After an ECS instance is created, run the following commands to install the Enclave Runtime toolset on the primary VM:

        ```
        sudo rpmkeys --import http://mirrors.aliyun.com/epel/RPM-GPG-KEY-EPEL-7
        sudo yum install -y alinux-release-experimentals
        sudo yum install -y https://enclave.oss-cn-hangzhou.aliyuncs.com/de-platform-runtime-0.1.0-1.2.al7.x86_64.rpm
        ```

    After the Enclave Runtime toolset is installed, the local service attempts to automatically starts the enclave. By default, the enclave image is stored in /usr/local/share/dragonfly/image.bin. You can modify the /etc/enclave.conf configuration file to change the storage path. The configuration file also provides more configuration options, including the vCPU and memory resources allocated to the enclave.

2.  After the Enclave Runtime toolset is manually installed for the first time, run the following command to download the enclave image and save it to your local computer:

    ```
    wget -O /usr/local/share/dragonfly/image.bin \
      https://enclave-cn-shenzhen.oss-cn-shenzhen.aliyuncs.com/download/linux/enclave_image/x86_64/0.1.0/image-0.1.0.bin
    ```

3.  Run the systemctl commands to perform operations on the enclave:

    ```
    systemctl status de_platform_service # View the running status.
    systemctl start de_platform_service # Start the service.
    systemctl restart de_platform_service # Restart the service.
    systemctl stop de_platform_service # Stop the service.
    ```


## Use an enclave by using SDKs

Alibaba Cloud Enclave provides SDKs for you to develop your own applications on ECS instances that have Enclave enabled. Alibaba Cloud Enclave also provides a set of API definitions and code libraries that are compatible with SGX SDKs. If you already have an SGX application, you can run the application on a platform that has Enclave enabled only with a small amount of migration work.

1.  Prepare the following Dockerfile file in the development environment:

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

2.  Run the following command to use Docker to create an enclave image:

    ```
    docker build -t deenclave/sdk-builder .
    ```

    After the command is run, an image named deenclave/sdk-builder is generated. You can use this image to build DE Enclave applications. Alibaba Cloud provides the following [SDK examples](#section_gem_b9o_bg2) for your reference.


## SDK example 1: Start a container to build an application

Alibaba Cloud provides an SDK sample program in /opt/alibaba/teesdk/desdk/examples/SampleMath. This sample program receives two externally entered plane coordinate points, calculates the straight-line distance between the two points within the enclave, and sends the calculation results to the console. Perform the following operations.

1.  Run the following command to start a container by using the created deenclave/sdk-builder image:

    ```
    docker run -it \
      -v /opt/alibaba/teesdk/desdk/examples/SampleMath:/opt/app-root/src:z \
      deenclave/sdk-builder
    ```

2.  Run the cmake command to build the sample code within the started container:

    ```
    cmake3 -B build && \
    cmake3 --build build
    ```

    The application is located in /opt/app-root/src/build/SampleMath/App/app, and the enclave is located in /opt/app-root/src/build/SampleMath/Enclave/enclave.signed.so.

3.  Upload the application to the primary VM.

4.  Start the enclave on the primary VM, execute the sample code SampleMath, and then check the execution result.

    ```
    [root@AliYun ~]# ./app
    A(3,4) -> B(1,8) -> 4.47214
    A(6,9) -> B(6,2) -> 7
    A(3,3) -> B(7,5) -> 4.47214
    ```


## SDK example 2: Generate attestation materials through Attestation

Attestation is an authentication process that allows you to ensure that images, operating systems, and application code running in an enclave are not modified or tampered with. You can call API operations provided by the SDK in your Enclave application code to generate attestation materials and upload the attestation materials to the remote attestation server for verification. Then, the remote attestation server returns the verification results.

Alibaba Cloud provides the following sample programs. You can build and run these sample programs in the same way as you execute SampleMath in [SDK example 1](#section_gem_b9o_bg2).

-   The sample program for generating attestation materials is located in /opt/alibaba/teesdk/desdk/examples/QuoteGenerationSample.
-   The sample program for verifying attestation materials is located in /opt/alibaba/teesdk/desdk/examples/QuoteVerificationSample.

