# 部署svnserve访问SVN

本教程介绍如何通过svnserve访问模式来部署SVN。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。
-   已创建实例规格为ecs.g6.large的CentOS操作系统实例，具体操作请参见[创建方式导航](/cn.zh-CN/实例/创建实例/创建方式导航.md)。
-   已在实例安全组的入方向添加规则并放行SVN服务的默认端口3690，具体操作请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

本教程手动部署SVN的示例步骤中使用了以下版本软件。操作时，请您以实际软件版本为准。

-   操作系统：公共镜像CentOS 7.2 64位
-   SVN：1.7.14

## 操作步骤

-   [步骤一：安装SVN](#section_h54_dqf_pyz)
-   [步骤二：配置SVN](#section_qui_xbb_dke)
-   [步骤三：使用Windows客户端测试](#section_frq_nei_7ay)

## 步骤一：安装SVN

1.  [通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。

2.  运行以下命令安装SVN。

    ```
    yum install subversion
    ```

3.  运行以下命令查看SVN版本。

    ```
    svnserve --version
    ```

    ![查看SVN版本](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3912649951/p12528.png)


## 步骤二：配置SVN

1.  运行以下命令创建版本库根目录。

    ```
    mkdir /var/svn
    ```

2.  依次运行以下命令创建版本库。

    ```
    cd /var/svn
    ```

    ```
    svnadmin create /var/svn/svnrepos
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

4.  设置SVN版本库的账号和密码。

    1.  运行`cd conf/`命令。

    2.  运行`vi passwd`命令，打开用户配置文件。

    3.  按`i`键进入编辑模式。

    4.  移动光标至`[users]`下，添加用户账号和密码。

        **说明：** 添加账号和密码的格式为：账号 = 密码。例如，userTest（账号） = passWDTest（密码），如下图所示（注意等号两端要有一个空格）。

        ![svn-3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3912649951/p101210.png)

    5.  按`Esc`键退出编辑模式，并输入`:wq`保存并退出。

5.  设置账号的读写权限。

    1.  运行`vi authz`命令，打开权限控制文件。

    2.  按`i`键进入编辑模式。

    3.  移动光标至文件末尾，并添加如下代码（其中，userTest表示账号，r表示读权限，w表示写权限）：

        ```
        [/]
        userTest=rw
        ```

        ![svn-4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6912649951/p101211.png)

    4.  按`Esc`键退出编辑模式，并输入`:wq`保存并退出。

6.  修改SVN服务配置。

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

7.  运行以下命令启动SVN版本库。

    本文示例中，启动命令直接指定到版本库。

    ```
    svnserve -d -r /var/svn/svnrepos/
    ```

    **说明：** 运行`killall svnserve`命令可停止SVN服务。

8.  运行命令`ps -ef |grep svn`查看SVN服务是否开启。

    如果返回结果如下图所示，表示SVN服务已经开启。

    ![查看SVN服务状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0884677161/p12533.png)


## 步骤三：使用Windows客户端测试

1.  在本地下载并安装[TortoiseSVN客户端](http://tortoisesvn.net/downloads.html)。

2.  在本地项目文件夹内的空白区域单击鼠标右键。

    本示例中，项目文件夹为C:\\Test。

3.  在弹出菜单中，选择**SVN检出**。

    ![snv-1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4912649951/p101195.png)

4.  填写如下信息后，单击**确定**。

    -   指定**版本库URL**，本文示例中直接指定到版本库启动的SVN，svnserve只为`svnrepos`这一个版本库工作，因此版本库URL格式为svn://实例公网IP地址/。
    -   指定**检出至目录**。本文示例中，目录为C:\\Test。
    ![svn-2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0884677161/p101197.png)

    **说明：** 第一次登录需要输入账号和密码，即您在passwd文件中设置的用户名和密码。

    检出完成示例如下。

    ![svn-5](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0884677161/p101213.png)


