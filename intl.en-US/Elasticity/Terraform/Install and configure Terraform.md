# Install and configure Terraform

You must install and configure Terraform before you can use its simple template language to define, preview, and deploy cloud infrastructure.

1.  Download the appropriate software package for your operating system from the official website of [Terraform](https://www.terraform.io/downloads.html).

2.  Decompress the package to /usr/local/bin.

    If you decompress the executable file to another directory, you must set an environment variable for the file by using one of the following methods:

    -   For Linux operating systems, use the method as described in [How to permanently set $PATH on Linux/Unix?](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix)
    -   For Windows operating systems, use the method as described in [Where can I set path to make.exe on Windows?](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows)
    -   For macOS operating systems, use the method as described in [How to permanently set $PATH on Linux/Unix?](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix)
3.  Run the `terraform` command to verify the path.

    If the following similar list of available Terraform options is displayed, the installation is complete:

    ```
    username:~$ terraform
    Usage: terraform [-version] [-help] <command> [args]
    ```

4.  For higher flexibility and security in permission management, we recommend that you create a RAM user and grant permissions to the user.

    1.  Log on to the [RAM console](https://ram.console.aliyun.com/#/overview).
    2.  Create a RAM user named Terraform and create an AccessKey pair for the user. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md).
    3.  Grant permissions to the RAM user. In this example, the `AliyunECSFullAccess` and `AliyunVPCFullAccess` permissions are granted to the Terraform user. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md).
5.  Create an environment variable to store authentication information.

    ```
    export ALICLOUD_ACCESS_KEY="LTAIUrZCw3********"
    export ALICLOUD_SECRET_KEY="zfwwWAMWIAiooj14GQ2*************"
    export ALICLOUD_REGION="cn-beijing"
    ```


