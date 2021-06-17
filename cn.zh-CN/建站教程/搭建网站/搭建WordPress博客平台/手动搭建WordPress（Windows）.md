# 手动搭建WordPress（Windows）

本教程介绍如何在Windows操作系统的ECS实例上搭建WordPress网站。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。
-   已创建网络类型为专有网络的安全组，并且安全组的入方向添加规则并放行80端口及3389端口。 添加规则的具体操作请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。
-   已创建Windows操作系统的ECS实例，并且已经部署Web环境，详情请参见[部署Web环境](/cn.zh-CN/建站教程/搭建环境/部署Web环境.md)。本教程使用的软件版本如下：
    -   操作系统：Windows Server 2012 R2 64位中文版
    -   IIS服务版本：7.5
    -   PHP版本：7.0.28
    -   MySQL版本：5.7
    -   WordPress版本：5.3.2

**说明：** 当您使用不同软件版本时，可能需要根据实际情况调整参数配置。

## 搭建WordPress网站

1.  通过ECS控制台，远程连接部署好Web环境的ECS实例，下载WordPress。

    1.  远程连接ECS实例。

        详情请参见[通过密码或密钥认证登录Windows实例](/cn.zh-CN/实例/连接实例/使用Workbench连接实例/通过密码或密钥认证登录Windows实例.md)。

    2.  前往WordPress官网下载[WordPress安装包](https://wordpress.org/download/)。

        本教程下载的版本为5.3.2。

        **说明：** 阿里云中国内地地域的节点服务器，下载WordPress会出现报错`429 Too Many Requests`。建议您多次尝试，或者通过第三方下载WordPress。

    3.  解压WordPress安装包。

        本教程将安装包解压至`C:\wordpress`目录下。

2.  为WordPress网站创建MySQL数据库。

    1.  进入MySQL安装目录下的bin文件夹，按下`shift`键的同时，单击鼠标右键，然后选择**在此处打开命令窗口**。

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4212649951/p81913.png)

    2.  打开MySQL数据库。

        ```
        mysql -u root -p
        ```

    3.  创建数据库。

        本教程为WordPress网站创建数据库wordpress。

        ```
        create database wordpress;
        ```

3.  配置WordPress。

    1.  在WordPress解压路径`C:\wordpress`下，找到`wp-config-sample.php`文件，复制该文件，并将副本文件重命名为`wp-config.php`。

    2.  使用文本编辑器打开`wp-config.php`文件，修改与创建好的MySQL数据库wordpress有关的信息。

        如下图所示：

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3212649951/p81914.png)

    3.  保存`wp-config.php`文件。

4.  在服务器管理器中添加wordpress网站。

    1.  在Windows任务栏找到服务器管理器图标并打开。

        ![服务器管理器](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3212649951/p110645.png)

    2.  在服务器管理器顶部菜单栏，单击**工具** \> **Internet Information Services \(IIS\)管理器**。

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3212649951/p81920.png)

    3.  在**连接**列表，单击**服务器名称** \> **网站**。

    4.  将已绑定80端口的网站删除，或者修改80端口为其他未被占用的端口号，例如：8080端口。

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3212649951/p81925.png)

    5.  在右侧**操作**区域，单击**添加网站**，添加wordpress网站。

        添加信息如下图所示：

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3212649951/p81927.png)

        配置说明：

        -   网站名称：自定义网站名称，本教程使用wordpress作为网站名称。
        -   应用程序池：DefaultAppPool。
        -   物理路径：您WordPress的解压目录，本教程的目录为`C:\wordpress`。
        -   端口：80。
5.  安装并登录WordPress。

    1.  在ECS实例内，使用浏览器访问`http://localhost/`，将自动跳转至WorPress安装页面。

    2.  填写网站基本信息，然后单击**安装WordPress**。

        填写信息参数说明：

        -   站点标题：WordPress网站的名称。例如：demowp。
        -   用户名：用户登录WordPress时使用的用户名，请注意安全性。例如：testwp。
        -   密码：建议用户设置安全性高的密码。例如：Wp.123456。
        -   您的电子邮件：用于接收通知的电子邮件。例如：1234567890@aliyun.com。
    3.  单击**登录**。

    4.  输入您在安装WordPress时设置的用户名和密码，然后单击**登录**。

        成功进入您个人的WordPress网站。


## 解析WordPress网站域名

通过实例公网IP地址直接访问您的WordPress网站会降低服务端的安全性。如果您已有域名或者想为WordPress网站注册一个域名，可以参考以下步骤。本示例注册域名为`www.WordPress.EcsQuickStart.com`。

1.  注册域名。

    详情请参见[注册通用域名](/cn.zh-CN/域名注册/注册通用域名.md)。

2.  备案。

    如果您的域名指向的网站托管在阿里云中国内地节点服务器，您需要进行备案。如果您是首次备案，请参见[首次备案流程]()，其他情况请参见[ICP备案流程概述]()。

3.  解析域名。将域名指向实例公网IP。

    域名解析是使用域名访问您的网站的必备环节。具体操作流程，请参见[设置域名解析](http://help.aliyun.com/document_detail/29716.html)。

4.  返回搭建WordPress网站的ECS实例，进入MySQL安装目录下的bin文件夹，按下`shift`键的同时，单击鼠标右键，然后选择**在此处打开命令窗口**。

    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4212649951/p81913.png)

5.  登录MySQL数据库。

    ```
    mysql -u root -p
    ```

6.  使用wordpress数据库。

    ```
    use wordpress;
    ```

7.  将`http://localhost/`替换为新域名。

    ```
    update wp_options set option_value = replace(option_value, 'http://localhost', 'http://www.WordPress.EcsQuickStart.com') where option_name = 'home' OR option_name = 'siteurl';
    ```

    成功为WordPress网站设置新域名。


