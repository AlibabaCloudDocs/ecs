# 安装和配置Terraform

在使用Terraform的简单模板语言定义、预览和部署云基础结构前，您需要安装预配置Terraform。

1.  前往[Terraform官网](https://www.terraform.io/downloads.html)下载适用于您的操作系统的程序包。

2.  将程序包解压到/usr/local/bin。

    如果将可执行文件解压到其他目录，按照以下方法为其设置环境变量：

    -   Linux：请参见[在Linux系统设置环境变量](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix)。
    -   Windows：请参见[在Windows系统设置环境变量](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows)。
    -   macOS：请参见[在macOS系统设置环境变量](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix)。
3.  运行`terraform`验证路径配置。

    将显示可用的Terraform选项的列表，类似如下所示，表示安装完成。

    ```
    username:~$ terraform
    Usage: terraform [-version] [-help] <command> [args]
    ```

4.  为提高权限管理的灵活性和安全性，建议您创建RAM用户，并为其授权。

    1.  登录[RAM控制台](https://ram.console.aliyun.com/#/overview)。
    2.  创建名为Terraform的RAM用户，并为该用户创建AccessKey。具体步骤请参见[创建RAM用户](/intl.zh-CN/用户管理/创建RAM用户.md)。
    3.  为RAM用户授权。在本示例中，给用户Terraform授予`AliyunECSFullAccess`和`AliyunVPCFullAccess`权限，具体步骤请参见[为RAM用户授权](/intl.zh-CN/用户管理/为RAM用户授权.md)。
5.  创建环境变量，用于存放身份认证信息。

    ```
    export ALICLOUD_ACCESS_KEY="LTAIUrZCw3********"
    export ALICLOUD_SECRET_KEY="zfwwWAMWIAiooj14GQ2*************"
    export ALICLOUD_REGION="cn-beijing"
    ```


