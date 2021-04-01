# Build an SGX encrypted computing environment

This topic describes how to build an SGX encrypted computing environment in a g7t, c7t, or r7t instance \(vSGX instance\) and run sample code to verify SGX features.

A vSGX instance that uses the Alibaba Cloud Linux 2.1903 64-bit \(UEFI\) image is created, and you are logged on.

Intel® SGX secures data by providing hardware-based protections instead of firmware- or software-based protections, and can provide you with physical-level encrypted computing environment. Intel® SGX uses instruction set extensions and the access control mechanism to isolate the runtime environment of SGX programs. This can protect the confidentiality and integrity of key code and data against malware attacks. Compared with other security technologies, Intel® SGX uses the root of trust that contains only hardware. This can avoid defects caused by security vulnerabilities of software on which the root of trust is based, and improve system security.

The g7t, c7t, and r7t security-enhanced instance families provide encrypted memory based on Intel® SGX and support SGX technology applicable to virtual machines. You can develop and run SGX programs in vSGX instances.

## Build an SGX encrypted computing environment

Before you can develop SGX programs, you must install the runtime and SDK on the vSGX instance and configure the remote attestation service. We recommend that you use Alibaba Cloud Linux 2.1903 64-bit \(UEFI\) for a better user experience. Alibaba Cloud Linux 2.1903 64-bit \(UEFI\) is equipped with the SGX driver and provides TEE SDK that is completely compatible with Intel® SGX SDK.

1.  Install the Alibaba Cloud SGX runtime.

    **Note:** If you create a vSGX instance by using the ECS console, the Alibaba Cloud SGX runtime is automatically installed. You can skip this step and continue to install the Alibaba Cloud TEE SDK.

    1.  Install protobuf.

        ```
        yum install -y protobuf
        ```

    2.  Download the installation file of the Alibaba Cloud SGX runtime.

        -   Download URL over the Internet: `https://enclave-[Region-ID].oss-[Region-ID].aliyuncs.com/download/linux/x86_64/sgx_runtime/sgx_linux_x64_runtime_2.13.100.4.bin`.
        -   Download URL over the internal network in VPCs: `https://enclave-[Region-ID].oss-[Region-ID]-internal.aliyuncs.com/download/linux/x86_64/sgx_runtime/sgx_linux_x64_runtime_2.13.100.4.bin`.
        Replace \[Region-ID\] in the preceding URLs with the region ID of the vSGX instance. For example, you can download the installation file from the following URL over the internal network in a VPC for an instance in the China \(Beijing\) region:

        ```
        wget https://enclave-cn-beijing.oss-cn-beijing-internal.aliyuncs.com/download/linux/x86_64/sgx_runtime/sgx_linux_x64_runtime_2.13.100.4.bin
        ```

    3.  Install the Alibaba Cloud SGX runtime.

        ```
        sh sgx_linux_x64_runtime_2.13.100.4.bin
        ```

        **Note:** SGX Architectural Enclave Service Manager \(AESM\) is responsible for managing services such as enclave start, key configuration, and remote attestation. The default installation path of SGX AESM is /opt/intel/sgx-aesm-service.

2.  Install Alibaba Cloud TEE SDK.

    Alibaba Cloud TEE SDK is fully compatible with Intel® SGX SDK. After Alibaba Cloud TEE SDK is installed, you can visit [Intel® SGX Developer Reference](https://download.01.org/intel-sgx/sgx-linux/2.13/docs/Intel_SGX_Developer_Reference_Linux_2.13_Open_Source.pdf) to develop SGX programs.

    -   Download URL over the Internet: `https://enclave-[Region-ID].oss-[Region-ID].aliyuncs.com/sdk/installer/teesdk-0.1.0-1.1.al7.x86_64.rpm`.
    -   Download URL over the internal network in VPCs: `https://enclave-[Region-ID].oss-[Region-ID]-internal.aliyuncs.com/sdk/installer/teesdk-0.1.0-1.1.al7.x86_64.rpm`.
    Replace \[Region-ID\] in the preceding URLs with the region ID of the vSGX instance. For example, you can install Alibaba Cloud TEE SDK from the following URL over the internal network in a VPC for an instance in the China \(Beijing\) region:

    ```
    yum install -y https://enclave-cn-beijing.oss-cn-beijing-internal.aliyuncs.com/sdk/installer/teesdk-0.1.0-1.1.al7.x86_64.rpm
    ```

    **Note:** The default installation directory of Intel® SGX SDK in Alibaba Cloud TEE SDK is /opt/alibaba/teesdk/intel/sgxsdk/.

3.  Configure Alibaba Cloud SGX remote attestation service.

    Alibaba Cloud SGX remote attestation service is fully compatible with Intel® SGX Elliptic Curve Digital Signature Algorithm \(ECDSA\)-based remote attestation service and Intel® SGX SDK. Therefore, vSGX instances provided by Alibaba Cloud can gain trust from remote providers and producers by using remote attestation. For more information, visit [Intel® ECDSA remote attestation service](https://software.intel.com/content/www/us/en/develop/topics/software-guard-extensions/attestation-services.html). The Alibaba Cloud SGX remote attestation service provides the following information for SGX SDK:

    -   SGX certificates
    -   Revocation list: the list of revoked SGX certificates
    -   Trusted computing base information: the information of the root of trust
    The Alibaba Cloud SGX remote attestation service is regionally deployed. You can access this service deployed in the region where the vSGX instance is located for optimal stability. After Alibaba Cloud TEE SDK is installed, the default configuration file /etc/sgx\_default\_qcnl.conf is automatically generated for the remote attestation service. You must manually adapt the file to the Alibaba Cloud SGX remote attestation service in the region where the vSGX instance is located.

    **Note:** Alibaba Cloud SGX remote attestation service is supported only in regions within mainland China. For more information, see [Regions and zones]().

    -   If the vSGX instance is assigned a public IP address, modify /etc/sgx\_default\_qcnl.conf to the following content:

        ```
        # PCCS server address
        PCCS_URL=https://sgx-dcap-server.[Region-ID].aliyuncs.com/sgx/certification/v3/
        # To accept insecure HTTPS cert, set this option to FALSE
        USE_SECURE_CERT=TRUE
        ```

        Replace \[Region-ID\] in the preceding file with the region ID of the vSGX instance. Example for a vSGX instance in the China \(Beijing\) region:

        ```
        # PCCS server address
        PCCS_URL=https://sgx-dcap-server.cn-beijing.aliyuncs.com/sgx/certification/v3/
        # To accept insecure HTTPS cert, set this option to FALSE
        USE_SECURE_CERT=TRUE
        ```

    -   If the vSGX instance is in a VPC and has only internal IP addresses, modify /etc/sgx\_default\_qcnl.conf to the following content:

        ```
        # PCCS server address
        PCCS_URL=https://sgx-dcap-server-vpc.[Region-ID].aliyuncs.com/sgx/certification/v3/
        # To accept insecure HTTPS cert, set this option to FALSE
        USE_SECURE_CERT=TRUE
        ```

        Replace \[Region-ID\] in the preceding file with the region ID of the vSGX instance. Example for a vSGX instance in the China \(Beijing\) region:

        ```
        # PCCS server address
        PCCS_URL=https://sgx-dcap-server-vpc.cn-beijing.aliyuncs.com/sgx/certification/v3/
        # To accept insecure HTTPS cert, set this option to FALSE
        USE_SECURE_CERT=TRUE
        ```


## Example 1 of verifying SGX features: Start an enclave

Alibaba Cloud TEE SDK provides SGX sample code to verify SGX features. By default, the code is stored in the /opt/alibaba/teesdk/intel/sgxsdk/SampleCode directory.

This section describes the example of how to verify whether the installed SGX SDK works normally by starting an enclave. If the enclave is started, the SDK works normally.

1.  Install devtoolset.

    1.  Open Alibaba Cloud software repositories.

        ```
        rpmkeys --import http://mirrors.cloud.aliyuncs.com/epel/RPM-GPG-KEY-EPEL-7
        yum install -y alinux-release-experimentals
        ```

    2.  Install devtoolset.

        ```
        yum install -y devtoolset-9
        ```

    3.  Set the environment variable related to devtoolset.

        ```
        source /opt/rh/devtoolset-9/enable
        ```

2.  Set the environment variable related to SGX SDK.

    ```
    source /opt/alibaba/teesdk/intel/sgxsdk/environment
    ```

3.  Compile the sample code SampleEnclave.

    1.  Go to the SampleEnclave directory.

        ```
        cd /opt/alibaba/teesdk/intel/sgxsdk/SampleCode/SampleEnclave
        ```

    2.  Compile SampleEnclave.

        ```
        make
        ```

        ![make-enclave](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9605017161/p256785.png)

4.  Run the compiled executable file.

    ```
    ./app
    ```

    ![run-enclave](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9605017161/p256812.png)


## Example 2 of verifying SGX features: SGX remote attestation

Alibaba Cloud TEE SDK provides SGX sample code to verify SGX features. By default, the code is stored in the /opt/alibaba/teesdk/intel/sgxsdk/SampleCode directory.

This section describes the example of the SGX remote attestation service \(QuoteGenerationSample and QuoteVerificationSample\). The expected result is that Quote is generated and verified. The example involves the challenged party \(SGX programs that run in the vSGX instance\) and the challenging party \(the party that wants to verify whether the SGX programs are trusted\). QuoteGenerationSample is the sample code used by the challenged party to generate Quote, and QuoteVerificationSample is the sample code used by the challenging party to verify Quote.

1.  Install devtoolset.

    1.  Open Alibaba Cloud software repositories.

        ```
        rpmkeys --import http://mirrors.cloud.aliyuncs.com/epel/RPM-GPG-KEY-EPEL-7
        yum install -y alinux-release-experimentals
        ```

    2.  Install devtoolset.

        ```
        yum install -y devtoolset-9
        ```

    3.  Set the environment variable related to devtoolset.

        ```
        source /opt/rh/devtoolset-9/enable
        ```

2.  Set the environment variable related to SGX SDK.

    ```
    source /opt/alibaba/teesdk/intel/sgxsdk/environment
    ```

3.  Compile the sample code QuoteGenerationSample used by the challenged party.

    1.  Go to the QuoteGenerationSample directory.

        ```
        cd /opt/alibaba/teesdk/intel/sgxsdk/SampleCode/QuoteGenerationSample
        ```

    2.  Compile QuoteGenerationSample.

        ```
        make
        ```

        ![make-quote-generation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9605017161/p256814.png)

4.  Run the compiled executable file to generate Quote.

    ```
    ./app
    ```

    ![run-quote-generation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9605017161/p256819.png)

5.  Compile the sample code QuoteVerificationSample used by the challenging party.

    1.  Go to the QuoteVerificationSample directory.

        ```
        cd /opt/alibaba/teesdk/intel/sgxsdk/SampleCode/QuoteVerificationSample
        ```

    2.  Compile QuoteVerificationSample.

        ```
        make
        ```

        ![make-quote-verification](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9605017161/p256822.png)

6.  Sign the QuoteVerificationSample enclave.

    To release an official version of an enclave, you must provide the signature key to sign the enclave.

    ```
    /opt/alibaba/teesdk/intel/sgxsdk/bin/x64/sgx_sign sign -key Enclave/Enclave_private_sample.pem -enclave enclave.so -out enclave.signed.so -config Enclave/Enclave.config.xml
    ```

    ![sign-enclave](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0705017161/p256827.png)

7.  Run the compiled executable file to verify Quote.

    ```
    ./app
    ```

    ![run-quote-verification](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0705017161/p256828.png)


