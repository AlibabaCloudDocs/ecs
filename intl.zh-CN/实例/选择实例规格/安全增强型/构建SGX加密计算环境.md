# 构建SGX加密计算环境

本文介绍如何在g7t、c7t或r7t实例（下文简称为vSGX实例）中构建SGX加密计算环境，并演示如何运行示例代码以验证SGX功能。

已创建使用Alibaba Cloud Linux 2.1903 64位UEFI版镜像的vSGX实例，并登录vSGX实例。

Intel® SGX以硬件安全保障信息安全，不依赖固件和软件的安全状态，为用户提供物理级的加密计算环境。Intel® SGX通过新的指令集扩展与访问控制机制实现SGX程序的隔离运行，保障关键代码和数据的机密性与完整性不受恶意软件的破坏。不同于其他安全技术，Intel®SGX的可信根仅包括硬件，避免了基于软件的可信根可能自身存在安全漏洞的缺陷，极大地提升了系统安全保障。

阿里云安全增强型实例规格族g7t、c7t、r7t基于Intel®SGX技术提供加密内存，并支持虚拟机形态的SGX技术，您可以在vSGX实例中开发并运行SGX程序。

**说明：** 如果您在Intel SGX Enclave中使用了与硬件相绑定的密钥加密数据（例如基于SGX Sealing），实例所在的宿主机发生变化后将导致无法解密对应数据。建议您在应用层做好数据冗余和备份，以保证应用的可靠性。

## 构建SGX加密计算环境

为开发SGX程序，您需要在vSGX实例上安装运行时（runtime）、SDK，并配置远程证明服务。建议您使用Alibaba Cloud Linux 2.1903 64位UEFI版镜像获得更好的使用体验。Alibaba Cloud Linux 2.1903 64位UEFI版镜像已搭载SGX驱动，并提供完全兼容Intel® SGX SDK的阿里云TEE SDK。

1.  安装阿里云SGX运行时。

    **说明：** 如果您通过ECS管理控制台创建vSGX实例，会自动安装阿里云SGX运行时。您可以跳过本步骤，直接开始安装阿里云TEE SDK。

    1.  导入阿里云加密计算yum软件源。

        -   公网地址格式：`https://enclave-[Region-ID].oss-[Region-ID].aliyuncs.com/repo/alinux/enclave-expr.repo`。
        -   VPC内网地址格式：`https://enclave-[Region-ID].oss-[Region-ID]-internal.aliyuncs.com/repo/alinux/enclave-expr.repo`。
        请将上述地址中的\[Region-ID\]替换为vSGX实例所在地域的ID。例如，华北2（北京）地域中的VPC内网导入示例：

        ```
        sudo yum install -y yum-utils && \
            sudo yum-config-manager --add-repo \
            https://enclave-cn-beijing.oss-cn-beijing-internal.aliyuncs.com/repo/alinux/enclave-expr.repo
        ```

    2.  安装阿里云SGX运行时。

        ```
        yum install -y \
            libsgx-ae-le libsgx-ae-pce libsgx-ae-qe3 libsgx-ae-qve \
            libsgx-aesm-ecdsa-plugin libsgx-aesm-launch-plugin libsgx-aesm-pce-plugin libsgx-aesm-quote-ex-plugin \
            libsgx-dcap-default-qpl libsgx-dcap-ql libsgx-dcap-quote-verify \
            libsgx-enclave-common libsgx-launch libsgx-pce-logic libsgx-qe3-logic libsgx-quote-ex \
            libsgx-ra-network libsgx-ra-uefi libsgx-uae-service libsgx-urts sgx-ra-service \
            sgx-aesm-service
        ```

        **说明：** SGX AESM（Architectural Enclave Service Manager）负责管理启动Enclave、密钥配置、远程认证等服务，默认安装路径为/opt/intel/sgx-aesm-service。

2.  安装阿里云TEE SDK。

    ```
    yum install -y teesdk
    ```

    阿里云TEE SDK完全兼容Intel® SGX SDK，安装阿里云TEE SDK后，您可以参见[Intel® SGX Developer Reference](https://download.01.org/intel-sgx/sgx-linux/2.13/docs/Intel_SGX_Developer_Reference_Linux_2.13_Open_Source.pdf)开发SGX程序。

    **说明：** 阿里云TEE SDK中包含的Intel® SGX SDK的默认安装目录为/opt/alibaba/teesdk/intel/sgxsdk/。

3.  安装补丁。

    Alibaba Cloud Linux 2.1903 64位UEFI版镜像搭载的SGX驱动在特定情况下存在内存泄露问题，该问题将在下个版本修复。如果您调用API创建了vSGX实例，建议安装补丁规避该问题。如果您通过控制台创建了vSGX实例，请跳过本步骤。

    ```
    yum install -y alinux-release-experimentals && \
        yum install -y kernel-hotfix-5577959-23.al7.x86_64
    ```

4.  配置阿里云SGX远程证明服务。

    阿里云SGX远程证明服务完全兼容[Intel® SGX ECDSA远程证明服务](https://software.intel.com/content/www/us/en/develop/topics/software-guard-extensions/attestation-services.html)和Intel® SGX SDK，因此阿里云vSGX实例能够通过远程证明来获得远程提供商或生产者的信任。阿里云SGX远程证明服务为SGX SDK提供下列信息：

    -   SGX certificates：SGX证书。
    -   Revocation lists：已被撤销的SGX证书列表。
    -   Trusted computing base information：可信根信息。
    阿里云SGX远程证明服务采用区域化部署，您可以访问vSGX实例所在地域的阿里云SGX远程证明服务来获得最佳的稳定性。安装阿里云TEE SDK后会自动生成远程证明服务的默认配置文件/etc/sgx\_default\_qcnl.conf，您需要手动修改该文件以适配vSGX实例所在地域的阿里云SGX远程证明服务。

    **说明：** 目前仅中国内地地域支持阿里云SGX远程证明服务，详细信息，请参见[地域和可用区]()。

    -   如果vSGX实例已分配公网IP，/etc/sgx\_default\_qcnl.conf的内容修改如下：

        ```
        # PCCS server address
        PCCS_URL=https://sgx-dcap-server.[Region-ID].aliyuncs.com/sgx/certification/v3/
        # To accept insecure HTTPS cert, set this option to FALSE
        USE_SECURE_CERT=TRUE
        ```

        请将上述内容中的\[Region-ID\]替换为vSGX实例所在地域的ID。例如华北2（北京）地域的修改示例如下：

        ```
        # PCCS server address
        PCCS_URL=https://sgx-dcap-server.cn-beijing.aliyuncs.com/sgx/certification/v3/
        # To accept insecure HTTPS cert, set this option to FALSE
        USE_SECURE_CERT=TRUE
        ```

    -   如果vSGX实例只有VPC内网IP，/etc/sgx\_default\_qcnl.conf的内容修改如下：

        ```
        # PCCS server address
        PCCS_URL=https://sgx-dcap-server-vpc.[Region-ID].aliyuncs.com/sgx/certification/v3/
        # To accept insecure HTTPS cert, set this option to FALSE
        USE_SECURE_CERT=TRUE
        ```

        请将上述内容中的\[Region-ID\]替换为vSGX实例所在地域的ID。例如华北2（北京）地域的修改示例如下：

        ```
        # PCCS server address
        PCCS_URL=https://sgx-dcap-server-vpc.cn-beijing.aliyuncs.com/sgx/certification/v3/
        # To accept insecure HTTPS cert, set this option to FALSE
        USE_SECURE_CERT=TRUE
        ```


## 验证SGX功能示例一：启动Enclave

阿里云TEE SDK中提供了SGX示例代码用于验证SGX功能，默认位于/opt/alibaba/teesdk/intel/sgxsdk/SampleCode目录下。

本节演示其中的启动Enclave示例（SampleEnclave），效果为启动一个Enclave，以验证是否可以正常使用安装的SGX SDK。

1.  安装devtoolset。

    1.  打开阿里云exp源。

        ```
        rpmkeys --import http://mirrors.cloud.aliyuncs.com/epel/RPM-GPG-KEY-EPEL-7 && \
            yum install -y alinux-release-experimentals
        ```

    2.  安装devtoolset。

        ```
        yum install -y devtoolset-9
        ```

    3.  设置devtoolset相关的环境变量。

        ```
        source /opt/rh/devtoolset-9/enable
        ```

2.  设置SGX SDK相关的环境变量。

    ```
    source /opt/alibaba/teesdk/intel/sgxsdk/environment
    ```

3.  编译示例代码SampleEnclave。

    1.  进入SampleEnclave目录。

        ```
        cd /opt/alibaba/teesdk/intel/sgxsdk/SampleCode/SampleEnclave
        ```

    2.  编译SampleEnclave。

        ```
        make
        ```

4.  运行编译出的可执行文件。

    ```
    ./app
    ```


## 验证SGX功能示例二：SGX远程证明示例

阿里云TEE SDK中提供了SGX示例代码用于验证SGX功能，默认位于/opt/alibaba/teesdk/intel/sgxsdk/SampleCode目录下。

本节演示其中的SGX远程证明示例（QuoteGenerationSample、QuoteVerificationSample），效果为生成和验证Quote。该示例涉及被挑战方（在vSGX实例中运行的SGX程序）和挑战方（希望验证SGX程序是否可信的一方），其中QuoteGenerationSample为被挑战方生成Quote的示例代码，QuoteVerificationSample为挑战方验证Quote的示例代码。

1.  安装devtoolset。

    1.  打开阿里云exp源。

        ```
        rpmkeys --import http://mirrors.cloud.aliyuncs.com/epel/RPM-GPG-KEY-EPEL-7 && \
            yum install -y alinux-release-experimentals
        ```

    2.  安装devtoolset。

        ```
        yum install -y devtoolset-9
        ```

    3.  设置devtoolset相关的环境变量。

        ```
        source /opt/rh/devtoolset-9/enable
        ```

2.  设置SGX SDK相关的环境变量。

    ```
    source /opt/alibaba/teesdk/intel/sgxsdk/environment
    ```

3.  编译被挑战方示例代码QuoteGenerationSample。

    1.  进入QuoteGenerationSample目录。

        ```
        cd /opt/alibaba/teesdk/intel/sgxsdk/SampleCode/QuoteGenerationSample
        ```

    2.  编译QuoteGenerationSample。

        ```
        make
        ```

4.  运行编译出的可执行文件生成Quote。

    ```
    ./app
    ```

5.  编译挑战方示例代码QuoteVerificationSample。

    1.  进入QuoteVerificationSample目录。

        ```
        cd /opt/alibaba/teesdk/intel/sgxsdk/SampleCode/QuoteVerificationSample
        ```

    2.  编译QuoteVerificationSample。

        ```
        make
        ```

6.  对QuoteVerificationSample Enclave进行签名。

    发布对外的正式版Enclave时，您需要提供签名密钥进行签名操作。

    ```
    sgx_sign sign -key Enclave/Enclave_private_sample.pem -enclave enclave.so -out enclave.signed.so -config Enclave/Enclave.config.xml
    ```

7.  运行编译出的可执行文件验证Quote。

    ```
    ./app
    ```


