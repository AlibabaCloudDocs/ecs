# Use the RTL design on an f3 instance

This topic describes how to implement the Register Transfer Level \(RTL\) design on an f3 instance.

-   An f3 instance is created and is able to access the Internet. For more information, see [Create an f3 instance](/intl.en-US/Instance/Instance type families/Compute optimized type family with FPGA/Create an f3 instance.md).
-   A rule is added to the security group to which the f3 instance belongs to allow access over SSH port 22. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).
-   The ID of the f3 instance is obtained on the Instances page of the [Elastic Compute Service \(ECS\) console](https://ecs.console.aliyun.com/#/home).
-   An Object Storage Service \(OSS\) bucket dedicated to FPGA as a Service \(FaaS\) is created in the China \(Shanghai\) region. For more information, see [Create buckets](/intl.en-US/Quick Start/OSS console/Create buckets.md).

    **Note:** The FaaS administrator account has read and write permissions on the bucket. We recommend that you only store information that is related to FaaS.

-   You must complete the following operations before you can manage FPGA-accelerated instances as a RAM user:
    -   Create a RAM user and grant permissions to the RAM user. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Basic operations/Create a RAM user.md) and [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Authorization management/Grant permissions to a RAM user.md).

        The permissions you must grant to the RAM user include AliyunECSReadOnlyAccess, AliyunOSSFullAccess, and AliyunRAMFullAccess.

    -   Go to the [Cloud Resource Access Authorization](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunFAASDefaultRole%22%2C%20%22TemplateId%22%3A%20%22DefaultRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//ecs.console.aliyun.com/%23/home%22%2C%20%22Service%22%3A%20%22FAAS%22%7D) page to authorize FaaS to access your resources.
    -   Obtain the AccessKey ID and AccessKey secret of the RAM user.

Before you perform the operations, take note of the following items:

-   All operations described in this topic must be performed by a single account within the same region.
-   We recommend that you perform operations on an f3 instance as a Resource Access Management \(RAM\) user. We recommend that you grant the RAM user necessary permissions based on the principle of least privilege, such as permissions to access DCP/xclbin files in OSS buckets, upload the Vivado compilation log, and manage specified ECS instances. You must also specify the RAM role AliyunFAASDefaultRole. By default, the role is used by FaaS to access resources hosted in other cloud services. The AliyunFAASRolePolicy policy of the role includes permissions on Key Management Service \(KMS\) for you to encrypt IP addresses.

## Procedure

1.  [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).

    **Note:** The compilation process may take 2 to 3 hours to complete. We recommend that you use nohup or Virtual Network Computing \(VNC\) to connect to the instance to avoid unexpected disconnection.

2.  Download and decompress the [RTL design](https://faas-ref-design.oss-cn-hangzhou.aliyuncs.com/FaaS_F3/f3_hdk.tar.gz).

3.  Set up the environment.

    -   If the driver is `xdma`, run the following command to set up the environment:

        ```
        source /root/xbinst_oem/F3_env_setup.sh xdma #Run the command each time you open a new terminal window.  
        ```

    -   If the driver is `xocl`, run the following command to set up the environment:

        ```
        source /root/xbinst_oem/F3_env_setup.sh xocl #Run the command each time you open a new terminal window.
        ```

    **Note:** The environment set-up process involves installing the xdma or xocl driver, setting the vivado environment variable, checking the vivado license, checking the aliyun-f3 sdaccel platform, configuring 2018.2 runtime, and checking the faascmd version.

4.  Specify an OSS bucket.

    ```
    faascmd config --id=<hereIsYourSecretId> --key=<hereIsYourSecretKey> #Replace <hereIsYourSecretId> with the AccessKey ID of the RAM user, and replace <hereIsYourSecretKey> with the AccessKey secret of the RAM user.
    faascmd auth --bucket=hereIsYourBucket # Replace <hereIsYourBucket> with the name of the OSS bucket that you created.                        
    ```

5.  Run the following command to compile the RTL project:

    ```
    cd <Directory where the decompressed RTL design resides>/hw/ # Access the hw directory where the decompressed RTL design resides.
    sh compiling.sh               
    ```

    **Note:** The compilation process takes about 2 to 3 hours to complete.

6.  Upload the netlist files and download the FPGA image.

    You can use faascmd to upload the netlist files and download the FPGA image. For more information about how to use the faascmd command, see [Use faascmd](/intl.en-US/Best Practices/FaaS instances best practices/faascmd tool/Use faascmd.md).

    1.  Run the following commands in sequence to upload the package to your OSS bucket, and then upload the GBS file from your OSS bucket to the OSS bucket in the FaaS administrative unit:

        ```
        faascmd upload_object --object=bit.tar.gz --file=bit.tar.gz
        faascmd create_image --object=bit.tar.gz --fpgatype=xilinx --name=<hereIsFPGAImageName> --tags=<hereIsFPGAImageTag> --encrypted=false --shell=<hereIsShellVersionOfFPGA>                      
        ```

        ![upload_object](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2614488951/p12112.png)

        ![create_image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2614488951/p12113.png)

    2.  Run the following command to check whether the FPGA image can be downloaded:

        ```
        faascmd list_images
        ```

        The command output is returned:

        -   If "State":"compiling" is displayed, the FPGA image is being compiled.
        -   If "State":"success" is displayed, the FPGA image can be downloaded. You must find and record the FpgaImageUUID value.
        ![list_images](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2614488951/p12115.png)

    3.  Run the following command. Find and record the FpgaUUID value in the command output.

        ```
        faascmd list_instances --instanceId=<hereIsYourInstanceId> # Replace <hereIsYourInstanceId> with the ID of the f3 instance.
        ```

    4.  Run the following command to download the FPGA image:

        ```
        #Replace <hereIsYourInstanceId> with the ID the f3 instance. Replace <hereIsFpgaUUID> with the FpgaUUID value that you recorded. Replace <hereIsImageUUID> with the FpgaImageUUID value that you recorded.
        faascmd download_image --instanceId=<hereIsYourInstanceId> --fpgauuid=<hereIsFpgaUUID> --fpgatype=xilinx --imageuuid=<hereIsImageUUID> --imagetype=afu --shell=<hereIsShellVersionOfFpga>
        ```

        ![download_image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2614488951/p12116.png)

    5.  Run the following command to check whether the image is downloaded:

        ```
        # Replace <hereIsFpgaUUID> with the FpgaUUID value that you recorded. Replace <hereIsYourInstanceId> with the ID of the f3 instance. 
        faascmd fpga_status --fpgauuid=<hereIsFpgaUUID> --instanceId=<hereIsYourInstanceId> 
        ```

        The following figure shows the command output. If the FpgaImageUUID value in the command output is the same as the FpgaImageUUID value that you recorded, and if "TaskStatus":"valid" is displayed, the image is downloaded.

        ![fpga_status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3614488951/p12117.png)


## FAQ

Question 1: How do I view the details of errors that occur during the image upload process?

If your project reports errors during the image upload process, such as compilation errors, you can use the following method to view the details of errors: Run the `sh /root/xbinst_oem/tool/faas_checklog.sh <Name of the uploaded package>` command to view the log file.

Question 2: How do I reload an image?

You can perform the following operations to reload an image:

1.  Uninstall the driver.

    -   If you installed the `xdma` driver, run the `sudo rmmod xdma` command in the instance to uninstall the driver.
    -   If you installed the `xocl` driver, run the `sudo rmmod xocl` command in the instance to uninstall the driver.
2.  Download the image.

    You can use faascmd to download the image:

    ```
    faascmd download_image --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=hereIsShellVersionOfFpga
    ```

3.  Install the driver.

    -   Run the following commands to install the `xdma` driver:

        ```
        sudo depmod
        sudo modprobe xdma
        ```

    -   Run the following commands to install the `xocl` driver:

        ```
        sudo depmod 
        sudo modprobe xocl
        ```


