# Manage the user data of Windows instances

This topic describes how to prepare user-data scripts for Windows instances and how to pass in user data and verify the result of running the user data.

If you want to modify the user data of an instance, the instance is in the **Stopped** state.

The user data feature enables Windows instances to run initialization scripts. When an instance starts, the system uses the administrator permissions to run the user data of the instance.

The following limits apply to user data:

-   The user data feature is supported only for instances that reside in virtual private clouds \(VPCs\).
-   The instances must be created from the following public images or custom images derived from public images:
    -   Alibaba Cloud Linux, CentOS, Ubuntu, SUSE Linux Enterprise, OpenSUSE, and Debian
    -   Windows Server 2008 R2 and later
-   The user data feature is supported for all available instance types. For retired instance types, the user data feature is supported only for I/O-optimized instances. For more information, see [Retired instance types](/intl.en-US/Instance/Instance type families/Retired instance types.md).
-   The user data that you want to run must be encoded in Base64. The size of the user data cannot exceed 16 KB before it is encoded.

    **Note:** You can enter the user data that has not been encoded in Base64 in the console. The console automatically encodes the user data in Base64. If you do not want to enter the user data in the console, you must encode it in Base64 on your own.


## Procedure

1.  Prepare user data.

    You can run batch and PowerShell scripts to prepare user data of Windows instances. For more information about the characteristics of different scripts and their examples, see the following sections:

    -   [Bat](#section_5lb_6c5_sdf)
    -   [PowerShell](#section_p81_sdk_rnb)
2.  Pass the user data into the instance.

    -   Pass in the user data when you create the instance: In the **System Configurations \(Optional\)** step, click **Advanced** to show the parameters and enter the user data in the **User Data** section. If the user data is encoded in Base64, select **Enter Base64 Encoded Information**.

        The following figure shows an example of content written to a specified file.

        ![createinstance-powershellsample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5276941261/p272285.png)

    -   Modify the user data of an existing instance: On the **Instances** page, find the instance for which you want to modify the user data and choose **More** \> **Instance Settings** \> **Set User Data**. In the Set User Data dialog box, enter new user data in the **User Data** section.

        **Note:** If you want to start a pay-as-you-go instance immediately after you modify the user data of the instance, we recommend that you set the stop mode of the instance to **Keep Instances and Continue Billing**.

        The following figure shows an example of the content written to a specified file.

        ![modifyinstance-powershellsample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5276941261/p272289.png)

        **Note:** After the user data is modified for a Windows instance, the new user data is not run when the instance is started.

3.  View the content passed into the instance and the script results.

    1.  Connect to the instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

    2.  View the content by using the metadata of the instance.

        ```
        Invoke-RestMethod http://100.100.100.200/latest/user-data
        ```

        In this example, the user data that is passed in in [Step 2](#step_v0x_9gc_u16) is used as an example. If the user data is included in the output, the user data is passed in, as shown in the following figure.

        ![view-userdata](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5276941261/p272292.png)

    3.  View the running results.

        The result of running a script is related to its content. The following figure shows an example of the result of writing content to the specified file.

        ![powershell-sample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0296851261/p272280.png)


## Bat

Batch scripts have the following characteristics:

-   The first line starts with `[bat]`, and the header cannot have spaces.
-   Only half-width letters can be entered, and no additional characters are allowed.

Example:

```
[bat]
echo "bat test" > C:\userdata_test.txt
```

The example batch script can be run to write `"bat test"` to the userdata\_test.txt file when the instance starts for the first time, as shown in the following figure.

![bat-sample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0296851261/p272279.png)

## PowerShell

PowerShell scripts have the following characteristics:

-   The first line starts with `[powershell]`, and the header cannot have spaces.
-   Only half-width letters can be entered, and no additional characters are allowed.

Example:

```
[powershell]
write-output "powershell test" | Out-File C:\userdata_test.txt
```

The example PowerShell script can be run to write `powershell test` to the userdata\_test.txt file when the instance starts for the first time, as shown in the following figure.

![powershell-sample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0296851261/p272280.png)

