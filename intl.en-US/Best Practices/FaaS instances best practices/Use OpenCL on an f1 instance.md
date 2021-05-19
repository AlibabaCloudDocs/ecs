# Use OpenCL on an f1 instance

This topic describes how to use Open Computing Language \(OpenCL\) on an f1 instance to create an image and download the image to a Field Programmable Gate Array \(FPGA\).

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   An f1 instance is created and can access the Internet.

    **Note:** Only FaaS F1 basic images from Alibaba Cloud Marketplace can be used in f1 instances. For more information, see [Create an f1 instance](/intl.en-US/Instance/Instance type families/Compute optimized type family with FPGA/Create an f1 instance.md).

-   The rule for allowing traffic on SSH port 22 is configured for the security groups where the f1 instance resides.
-   The ID of the f1 instance is obtained from the Instances page in the [ECS console](https://ecs.console.aliyun.com/#/home).
-   An OSS bucket for FaaS is created.

    The OSS bucket and the f1 instance must be in the same account and the same region. For more information, see [Create buckets](/intl.en-US/Quick Start/OSS console/Create buckets.md).

-   To encrypt files, activate Key Management Service \(KMS\) first.

    For more information, see [Activate KMS](/intl.en-US/Quick Start/Overview.md).

-   You must complete the following operations before you can manage FPGA-accelerated instances as a RAM user:
    -   Create a RAM user and grant permissions to the RAM user. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Basic operations/Create a RAM user.md) and [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Authorization management/Grant permissions to a RAM user.md).

        The permissions you must grant to the RAM user include AliyunECSReadOnlyAccess, AliyunOSSFullAccess, and AliyunRAMFullAccess.

    -   Go to the [Cloud Resource Access Authorization](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunFAASDefaultRole%22%2C%20%22TemplateId%22%3A%20%22DefaultRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//ecs.console.aliyun.com/%23/home%22%2C%20%22Service%22%3A%20%22FAAS%22%7D) page to authorize FaaS to access your resources.
    -   Obtain the AccessKey ID and AccessKey secret of the RAM user.

Before you perform the operations, take note of the following items:

-   All operations described in this topic must be performed by a single account within the same region.
-   We strongly recommend that you manage FPGA-accelerated instances as a RAM user. To avoid unwanted operations, you must only authorize the RAM user to perform required actions. You must create a role for the RAM user and grant temporary permissions to the role to access the specified OSS bucket. Then, you can download the original DCP project from the OSS bucket and manage the FPGA image. If you want to encrypt the IP address, you must authorize the RAM user to use KMS. If you want the RAM user to check permissions of Alibaba Cloud accounts, you must authorize the RAM user to view the resources of Alibaba Cloud accounts.

## Procedure

Perform the following operations to use the OpenCL example on an f1 instance to create an image and download the image to an FPGA:

1.  [Step 1: Connect to an f1 instance](#section_0xw_r1j_tak)
2.  [Step 2: Install the basic environment](#section_gob_p8r_eox)
3.  [Step 3: Copy the OpenCL example](#section_jrm_tz5_d4k)
4.  [Step 4: Upload the configuration file](#section_hbq_4vp_q7d)
5.  [Step 5: Download the image to the f1 instance](#section_nxl_txt_iep)
6.  [Step 6: Download the FPGA image to an FPGA](#section_bcs_ojs_uae)

## Step 1: Connect to an f1 instance

For more information, see [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).

## Step 2: Install the basic environment

Run the following script to install the basic environment:

```
source /opt/dcp1_1/script/f1_env_set.sh
```

## Step 3: Copy the OpenCL example

1.  Run the following commands in sequence to create and switch to the /opt/tmp directory:

    ```
    mkdir -p /opt/tmp         
    ```

    ```
    cd /opt/tmp            
    ```

    You are in the /opt/tmp directory.

    ![Enter the tmp directory](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6514488951/p11994.png)

2.  Run the following command to copy the OpenCL example to the current directory:

    ```
    cp /opt/dcp1_1/opencl/exm_opencl_vector_add_x64_linux.tgz ./
    ```

3.  Run the following commands in sequence to go to the vector\_add directory for compilation:

    ```
    cd vector_add             
    ```

    ```
    aoc -v -g -report ./device/vector_add.cl             
    ```

    The compilation process may take a few hours. You can start another session, and run the top command to monitor system resource usage and view the compilation status.


## Step 4: Upload the configuration file

1.  Run the following commands in sequence to initialize the faascmd tool:

    ```
    #Configure the environment variable.
    export PATH=$PATH:/opt/dcp1_1/script/
    ```

    ```
    #Grant execute permissions to the faascmd tool.
    chmod +x /opt/dcp1_1/script/faascmd
    ```

    ```
    #Replace <hereIsYourSecretId> in the command with your AccessKey ID. Replace <hereIsYourSecretKey> with your AccessKey secret.
    faascmd config --id=<hereIsYourSecretId> --key=<hereIsYourSecretKey>
    ```

    ```
    #Replace <hereIsYourBucket> in the command with your bucket name.
    faascmd auth --bucket=<hereIsYourBucket>
    ```

2.  Run the following commands in sequence to access the vector\_add/output\_files directory and upload the configuration file:

    ```
    cd vector_add/output_files         
    ```

    You are in the /opt/tmp/vector\_add/vector\_add/output\_files directory.

    ```
    faascmd upload_object --object=afu_fit.gbs --file=afu_fit.gbs           
    ```

3.  Run the following command to use the GBS file to create an FPGA image:

    ```
    #Replace <hereIsYourImageName> in the command with your image name. Replace <hereIsYourImageTag> with your image tag.
    faascmd create_image --object=dma_afu.gbs --fpgatype=intel --name=<hereIsYourImageName> --tags=<hereIsYourImageTag> --encrypted=false --shell=V1.1             
    ```

4.  Run the following command to check whether the image is created:

    ```
    faascmd list_images
    ```

    If "State":"success" is displayed in the command output, the image is created. Record the FpgaImageUUID value in the command output for later use.

    ![The image is created](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7514488951/p11996.png)


## Step 5: Download the image to the f1 instance

1.  Run the following command to obtain the ID of your FPGA instance:

    ```
    #Replace <hereIsYourInstanceId> in the command with the ID of your FPGA instance.
    faascmd list_instances --instanceId=<hereIsYourInstanceId>                 
    ```

    The following figure shows an example of the command output. Record the FpgaUUID value.

    ![fpgaUUID](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7514488951/p11997.png)

2.  Run the following command to download the image to the f1 instance.

    ```
    #Replace <hereIsYourInstanceID> in the command with the instance ID that you recorded. Replace <hereIsFpgaUUID> with the FpgaUUID value that you recorded. Replace <hereIsImageUUID> with the FpgaImageUUID value that you recorded.
    faascmd download_image  --instanceId=<hereIsYourInstanceID> --fpgauuid=<hereIsFpgaUUID> --fpgatype=intel --imageuuid=<hereIsImageUUID> --imagetype=afu --shell=V0.11                 
    ```

3.  Run the following command to check whether the image is downloaded:

    ```
    # Replace <hereIsYourInstanceID> in the command with the instance ID that you recorded. Replace <hereIsFpgaUUID> with the FpgaUUID value that you recorded.
    faascmd fpga_status --fpgauuid=<hereIsFpgaUUID> --instanceId=<hereIsYourInstanceID>            
    ```

    If "TaskStatus":"operating" is displayed in the command output, the image is downloaded.

    ![The image is downloaded](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7514488951/p11998.png)


## Step 6: Download the FPGA image to an FPGA

1.  Open the environment window in Step 2. If the window is closed, perform the operations in [Step 2](#section_gob_p8r_eox) again.

2.  Run the following command to configure the runtime environment for OpenCL:

    ```
    sh /opt/dcp1_1/opencl/opencl_bsp/linux64/libexec/setup_permissions.sh                 
    ```

3.  Run the following command to go back to the parent directory:

    ```
    cd ../..           
    ```

    You are in the /opt/tmp/vector\_add directory.

4.  Run the following commands for compilation:

    ```
    make
    # Show the environment configuration.
    export CL_CONTEXT_COMPILER_MODE_ALTERA=3
    cp vector_add.aocx ./bin/vector_add.aocx
    cd bin
    host vector_add.aocx               
    ```

    If the following output is displayed, the environment is configured. Note that the last line must be `Verification: PASS`.

    ```
    [root@iZbpXXXXXZ bin]# ./host vector_add.aocx
    Matrix sizes:
      A: 2048 x 1024
      B: 1024 x 1024
      C: 2048 x 1024
    Initializing OpenCL
    Platform: Intel(R) FPGA SDK for OpenCL(TM)
    Using 1 device(s)
      skx_fpga_dcp_ddr : SKX DCP FPGA OpenCL BSP (acl0)
    Using AOCX: vector_add.aocx
    Generating input matrices
    Launching for device 0 (global size: 1024, 2048)
    Time: 40.415 ms
    Kernel time (device 0): 40.355 ms
    Throughput: 106.27 GFLOPS
    Computing reference output
    Verifying
    Verification: PASS             
    ```


