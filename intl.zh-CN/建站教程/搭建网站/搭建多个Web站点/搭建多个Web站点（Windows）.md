# 搭建多个Web站点（Windows）

本文介绍如何在Windows Server 2012 R2 64位系统的ECS实例上使用IIS服务器搭建多个Web站点。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.alibabacloud.com/register/intl_register.htm)。
-   已创建ECS实例，并部署了IIS+PHP+MySQL环境，您可以通过[云市场](https://marketplace.alibabacloud.com/)查找Windows系统的Web环境镜像，进行快速部署。

本教程适用于熟悉Windows操作系统，希望合理利用资源、统一管理站点以提高运维效率的用户。比如，您可以在一台云服务器上配置多个不同分类的博客平台或者搭建多个Web站点实现复杂业务的网站系统。

教程中，将通过Windows操作系统的IIS服务器，搭建两个测试站点`windows-testpage-1`和`windows-testpage-2`，并配置相同端口下不同域名来实现站点访问。

本教程示例步骤中使用的实例配置信息如下：

-   实例规格：ecs.c6.large
-   操作系统：Windows Server 2012 R2 64位

## 创建测试站点

1.  远程连接已部署Web环境的ECS实例。

    远程连接方式请参见[通过密码认证登录Windows实例](/intl.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Windows实例.md)。

2.  在桌面上单击**这台电脑**，并进入默认网站根目录下C:\\wwwroot。

3.  分别创建`windows-testpage-1`和`windows-testpage-2`两个文件夹。

    ![wwwroot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312649951/p128806.png)

4.  进入`windows-testpage-1`文件夹，创建测试文件test1.php，并在文件中输入以下测试内容。

    ```
    <?php
    echo "<title>Test-1</title>";
    echo "windows-test-1";
    ?>
    ```

5.  进入`windows-testpage-2`文件夹，创建测试文件test2.php，并在文件中输入以下测试内容。

    ```
    <?php
    echo "<title>Test-2</title>";
    echo "windows-test-2";
    ?>
    ```


## 配置IIS服务器

1.  在桌面底部任务栏，单击**服务器管理器**图标![server](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312649951/p128809.png)。

2.  在顶部菜单栏，单击**工具** \> **Internet Information Services \(IIS\)管理器**。

3.  在IIS管理器的左侧导航栏，单击服务器名称，并单击**网站**。

4.  在右侧操作区域，单击**添加网站...**。添加`windows-testpage-1`测试站点，然后单击**确定**。

    添加网站配置信息如下所示：

    ![netsite1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312649951/p128817.png)

    配置说明：

    -   网站名称：测试名称`windows-testpage-1`
    -   应用程序池：DefaultAppPool
    -   物理路径：测试站点`windows-testpage-1`的物理路径
    -   主机名：测试域名`test1.com`
5.  在右侧操作区域，单击**添加网站...**。添加`windows-testpage-2`测试站点，然后单击**确定**。

    添加网站配置信息如下所示：

    ![netsite2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312649951/p128819.png)

    配置说明：

    -   网站名称：测试名称`windows-testpage-2`
    -   应用程序池：DefaultAppPool
    -   物理路径：测试站点`windows-testpage-2`的物理路径
    -   主机名：测试域名`test2.com`
    网站添加完成后如下图所示。

    ![result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312649951/p128823.png)


## （可选）本地配置hosts

由于本教程中全部使用的测试信息，因此需要在本地的hosts文件中配置IP映射。如果您在配置多个站点信息时使用的是真实的域名，请忽略该步骤。教程中本地物理机使用Windows操作系统。

1.  访问C:\\Windows\\System32\\drivers\\etc目录。

2.  复制hosts文件进行备份。

    保留hosts - 副本文件，在测试完成后使用该文件恢复hosts文件的初始状态。

3.  修改hosts文件。

    在文件末尾追加以下内容，然后保存文件并退出。

    ```
    <ECS实例公网IP> test1.com
    <ECS实例公网IP> test2.com
    ```

4.  返回Windows桌面，并按下Win + R组合键。

5.  在**运行**对话框中输入cmd，并单击**确定**。

6.  在命令行中运行以下命令，使hosts配置立即生效。

    ```
    ipconfig /flushdns
    ```


在本地主机打开浏览器，成功访问到两个测试站点。

-   访问`test1.com/test1.php`，查看`windows-testpage-1`站点内容如下所示。

    ![test1.php](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312649951/p128826.png)

-   访问`test2.com/test2.php`，查看`windows-testpage-2`站点内容如下所示。

    ![test2.php](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2312649951/p128827.png)


至此多个Web站点已搭建成功。在实际搭建站点场景中，您只需要将主机名与项目的物理路径配置正确，即可实现多站点的访问。如果您需要安装SSL证书，请参见[在IIS服务器上安装SSL证书](/intl.zh-CN/证书安装/安装证书到服务器/在IIS服务器上安装SSL证书.md)。

