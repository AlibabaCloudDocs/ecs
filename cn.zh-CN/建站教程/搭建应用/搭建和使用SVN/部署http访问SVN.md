# 部署http访问SVN

本教程介绍如何通过http访问模式来部署SVN。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。
-   已创建CentOS操作系统实例，具体操作请参见[创建方式导航](/cn.zh-CN/实例/创建实例/创建方式导航.md)。
-   已在实例安全组的入方向添加规则并放行SVN服务的默认端口3690，具体操作请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

本教程手动部署SVN的示例步骤中ECS实例配置和版本软件信息如下。操作时，请您以实际配置为准。

-   实例规格：ecs.c6.large
-   操作系统：公共镜像CentOS 7.2 64位
-   SVN：1.7.14
-   Apache：2.4.6

您也可以通过云市场镜像快速部署SVN。例如云市场镜像提供的[SVN版本控制（Centos 64位 \| SVN）](https://market.aliyun.com/products/55530001/jxsc000061.html)，您可以选购镜像，并根据镜像选购页的使用指南，快速完成部署。

## 步骤一：安装SVN

1.  [远程连接Linux实例](/cn.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/使用用户名密码验证连接Linux实例.md)。

2.  运行以下命令安装SVN。

    ```
    yum install subversion -y
    ```

3.  运行以下命令查看SVN版本。

    ```
    svnserve --version
    ```


## 步骤二：安装Apache

1.  运行以下命令安装httpd。

    ```
    yum install httpd -y
    ```

2.  运行以下命令查看httpd版本。

    ```
    httpd -version
    ```


## 步骤三：安装mod\_dav\_svn

运行以下命令安装mod\_dav\_svn。

```
yum install mod_dav_svn -y
```

## 步骤四：配置SVN

1.  依次运行以下命令创建SVN版本库。

    ```
    mkdir /var/svn
    ```

    ```
    cd /var/svn
    svnadmin create /var/svn/svnrepos
    ```

2.  运行以下命令修改SVN仓库的用户组为apache。

    ```
    chown -R apache:apache /var/svn/svnrepos
    ```

3.  依次运行以下命令查看自动生成的版本库文件。

    ```
    cd svnrepos
    ```

    ```
    ls
    ```

    ![查看版本库文件](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6912649951/p12529.png)

    Subversion目录说明如下表：

    |目录|说明|
    |--|--|
    |db|存放所有的版本控制数据文件。|
    |hooks|放置hook脚本文件。|
    |locks|用来追踪存取文件库的客户端。|
    |format|一个文本文件，文件中只包含一个整数，表示当前文件库配置的版本号。|
    |conf|SVN版本库的配置文件（版本库的访问账号、权限等）。|

4.  运行以下命令增加SVN版本库的用户和密码。

    SVN默认使用明文密码，而http并不支持明文密码，所以需要单独生成passwd文件。本示例中，增加用户`userTest`，密码设置为`passWDTest`。 请根据实际情况选择并运行以下命令：

    -   如果您第一次增加用户，运行命令时需要带上参数`-c`生成文件。

        ```
        htpasswd -c /var/svn/svnrepos/conf/passwd userTest
        ```

    -   如果您已经增加过用户，当后续还需要增加用户时，请运行以下命令。

        ```
        htpasswd /var/svn/svnrepos/conf/passwd userTest
        ```

    根据提示设置用户的密码。

5.  运行以下命令进入conf目录下。

    ```
    cd /var/svn/svnrepos/conf/
    ```

6.  设置账号的读写权限。

    1.  运行`vi authz`命令，打开权限控制文件。

    2.  按`i`键进入编辑模式。

    3.  移动光标至文件末尾，并添加如下代码（其中，userTest表示账号，r表示读权限，w表示写权限）：

        ```
        [/]
        userTest=rw
        ```

        ![svn-4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6912649951/p101211.png)

    4.  按`Esc`键退出编辑模式，并输入`:wq`保存并退出。

7.  修改SVN服务配置。

    1.  运行`vi svnserve.conf`打开SVN服务配置文件。

    2.  按`i`键进入编辑模式。

    3.  移动光标找到如下配置行，删除行前面的注释符\#和空格：

        **说明：** 每行不能以空格开始，且等号两端要有一个空格。

        ```
        anon-access = read #匿名用户可读，您也可以设置 anon-access = none，不允许匿名用户访问。设置为 none，可以使日志日期正常显示
        auth-access = write #授权用户可写
        password-db = passwd #使用哪个文件作为账号文件
        authz-db = authz #使用哪个文件作为权限文件
        realm = /var/svn/svnrepos #认证空间名，版本库所在目录
        ```

        ![修改svn服务配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6912649951/p12532.png)

    4.  按`Esc`键退出编辑模式，并输入`:wq`保存并退出。

8.  运行以下命令启动SVN版本库。

    ```
    svnserve -d -r /var/svn/
    ```

    **说明：** 运行`killall svnserve`命令可停止SVN服务。

9.  运行命令`ps -ef |grep svn`查看SVN服务是否开启。

    如果返回结果如下图所示，表示SVN服务已经开启。

    ![查看SVN服务状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6912649951/p12533.png)


## 步骤五：配置Apache

1.  运行以下命令新增并编辑httpd配置文件。

    ```
    vim /etc/httpd/conf.d/subversion.conf
    ```

2.  按`i`键进入编辑模式。

3.  输入以下配置信息：

    ```
    <Location /svn>
    DAV svn
    SVNParentPath /var/svn
    AuthType Basic
    AuthName "Authorization SVN"
    AuthzSVNAccessFile /var/svn/svnrepos/conf/authz
    AuthUserFile /var/svn/svnrepos/conf/passwd
    Require valid-user
    </Location>
    ```

4.  按`Esc`键后，输入`:wq`保存并关闭文件。

5.  运行以下命令启动Apache服务。

    ```
    systemctl start httpd.service
    ```


## 步骤六：浏览器测试访问

1.  在本地主机上打开浏览器。

2.  输入网址`http://<ECS实例公网IP\>/svn/<SVN版本库名\>`并按回车键。本示例中，SVN版本库名为svnrepos。

3.  输入账号和密码，即您在passwd文件中设置的账号和密码。本示例中，账号为userTest，密码为passWDTest。

    返回结果如下图所示，表示成功访问之前新建的SVN仓库。

    ![result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6912649951/p101777.png)


