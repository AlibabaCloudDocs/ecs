---
keyword: [搭建FTP, CentOS 7.2搭建FTP, CentOS 7搭建FTP]
---

# 手动搭建FTP站点（CentOS 7）

vsftpd（very secure FTP daemon）是Linux下的一款小巧轻快、安全易用的FTP服务器软件。本教程介绍如何在Linux实例上安装并配置vsftpd。

已创建ECS实例并为实例分配了公网IP地址。若尚未创建，请参见[创建方式导航](/intl.zh-CN/实例/创建实例/创建方式导航.md)。

FTP（File Transfer Protocol）是一种文件传输协议，基于客户端/服务器架构，支持以下两种工作模式：

-   主动模式：客户端向FTP服务器发送端口信息，由服务器主动连接该端口。
-   被动模式：FTP服务器开启并发送端口信息给客户端，由客户端连接该端口，服务器被动接受连接。

**说明：** 大多数FTP客户端都在局域网中，没有独立的公网IP地址，且有防火墙阻拦，主动模式下FTP服务器成功连接到客户端比较困难。因此，如无特殊需求，建议您将FTP服务器配置为被动模式。

FTP支持以下三种认证模式：

-   匿名用户模式：任何人无需密码验证就可以直接登录到FTP服务器。这种模式最不安全，一般只用来保存不重要的公开文件，不推荐在生产环境中使用。
-   本地用户模式：通过Linux系统本地账号进行验证的模式，相较于匿名用户模式更安全。
-   虚拟用户模式：FTP服务器的专有用户。虚拟用户只能访问Linux系统为其提供的FTP服务，而不能访问Linux系统的其它资源，进一步增强了FTP服务器的安全性。

本文主要介绍被动模式下，使用本地用户访问FTP服务器的配置方法。关于匿名模式的配置方式、第三方FTP客户端工具使用方式等介绍，请参见[常见问题](#section_q6i_wdk_m96)。

本文示例步骤使用以下资源版本：

-   实例规格：ecs.c6.large
-   操作系统：CentOS 7.2 64位
-   vsftpd：3.0.2

当您使用不同软件版本时，可能需要根据实际情况调整命令和参数配置。

## 步骤一：安装vsftpd

1.  远程连接Linux实例。

    远程连接的具体操作，请参见[连接方式介绍](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

2.  运行以下命令安装vsftpd。

    ```
    yum install -y vsftpd
    ```

    出现如下图所示界面时，表示安装成功。

    ![install_vsftp_successfully](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2419459951/p12598.png)

3.  运行以下命令设置FTP服务开机自启动。

    ```
    systemctl enable vsftpd.service
    ```

4.  运行以下命令启动FTP服务。

    ```
    systemctl start vsftpd.service
    ```

    **说明：** 执行该命令时如果提示错误信息Job for vsftpd.service failed because the control process exited with error code，请排查是否存在下述问题。如果问题仍未解决，建议提交工单。

    -   网络环境不支持IPv6时，运行命令vim /etc/vsftpd/vsftpd.conf将内容`listen_ipv6=YES`修改为`listen_ipv6=NO`。
    -   MAC地址不匹配时，运行命令ifconfig查看MAC地址，并在/etc/sysconfig/network-scripts/ifcfg-xxx配置文件中新增或修改`HWADDR=<MAC地址>`。
5.  运行以下命令查看FTP服务监听的端口。

    ```
    netstat -antup | grep ftp
    ```

    出现如下图所示界面，表示FTP服务已启动，监听的端口号为21。此时，vsftpd默认已开启匿名访问功能，您无需输入用户名密码即可登录FTP服务器，但没有修改或上传文件的权限。

    ![install_vsftpd_3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2419459951/p12600.png)


## 步骤二：配置vsftpd

为保证数据安全，本文主要介绍被动模式下，使用本地用户访问FTP服务器的配置方法。

1.  运行以下命令为FTP服务创建一个Linux用户。本示例中，该用户名为ftptest。

    ```
    adduser ftptest
    ```

2.  运行以下命令修改ftptest用户的密码。

    ```
    passwd ftptest
    ```

    运行命令后，根据命令行提示完成FTP用户的密码修改。

3.  运行以下命令创建一个供FTP服务使用的文件目录。

    ```
    mkdir /var/ftp/test
    ```

4.  运行以下命令，创建测试文件。

    该测试文件用于FTP客户端访问FTP服务器时使用。

    ```
    touch /var/ftp/test/testfile.txt
    ```

5.  运行以下命令更改/var/ftp/test目录的拥有者为ftptest。

    ```
    chown -R ftptest:ftptest /var/ftp/test
    ```

6.  修改vsftpd.conf配置文件。

    1.  运行以下命令，打开vsftpd的配置文件。

        如果您在安装vsftpd时，使用的是`apt install vsftpd`安装命令，则配置文件路径为/etc/vsftpd.conf。

        ```
        vim /etc/vsftpd/vsftpd.conf
        ```

    2.  按i进入编辑模式。

    3.  配置FTP服务器为被动模式。

        具体的配置参数说明如下：

        **说明：** 修改和添加配置文件内的信息时，请注意格式问题。例如，添加多余的空格会造成无法重启服务的结果。

        ```
        #除下面提及的参数，其他参数保持默认值即可。
        
        #修改下列参数的值：
        #禁止匿名登录FTP服务器。
        anonymous_enable=NO
        #允许本地用户登录FTP服务器。
        local_enable=YES
        #监听IPv4 sockets。
        listen=YES
        
        #在行首添加#注释掉以下参数：
        #关闭监听IPv6 sockets。
        #listen_ipv6=YES
        
        #在配置文件的末尾添加下列参数：
        #设置本地用户登录后所在目录。
        local_root=/var/ftp/test
        #全部用户被限制在主目录。
        chroot_local_user=YES
        #启用例外用户名单。
        chroot_list_enable=YES
        #指定例外用户列表文件，列表中用户不被锁定在主目录。
        chroot_list_file=/etc/vsftpd/chroot_list
        #开启被动模式。
        pasv_enable=YES
        allow_writeable_chroot=YES
        #本教程中为Linux实例的公网IP。
        pasv_address=<FTP服务器公网IP地址>
        #设置被动模式下，建立数据传输可使用的端口范围的最小值。
        #建议您把端口范围设置在一段比较高的范围内，例如50000~50010，有助于提高访问FTP服务器的安全性。
        pasv_min_port=<port number>
        #设置被动模式下，建立数据传输可使用的端口范围的最大值。
        pasv_max_port=<port number>
        ```

        更多参数的详细信息，请参见[vsftp配置文件及参数说明](/intl.zh-CN/建站教程/搭建应用/搭建FTP站点/手动搭建FTP站点（CentOS 7）.md)。

    4.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。

7.  创建chroot\_list文件，并在文件中写入例外用户名单。

    1.  运行以下命令，创建chroot\_list文件。

        ```
        vim /etc/vsftpd/chroot_list
        ```

    2.  按i进入编辑模式。

    3.  输入例外用户名单。此名单中的用户不会被锁定在主目录，可以访问其他目录。

    4.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。

    **说明：** 没有例外用户时，也必须创建chroot\_list文件，内容可为空。

8.  运行以下命令重启vsftpd服务。

    ```
    systemctl restart vsftpd.service
    ```


## 步骤三：设置安全组

搭建好FTP站点后，在实例安全组的入方向添加规则并放行下列FTP端口。具体操作，请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

**说明：** 大多数客户端位于局域网中，IP地址是经过转换的，因此ipconfig或ifconfig命令返回的IP不一定是客户端的真实公网IP地址。若后续客户端无法登录FTP服务器，请重新确认其公网IP地址。

被动模式需开放21端口，以及配置文件/etc/vsftpd/vsftpd.conf中参数pasv\_min\_port和pasv\_max\_port之间的所有端口。配置详情如下表所示。

|规则方向|授权策略|协议类型|端口范围|授权对象|
|----|----|----|----|----|
|入方向|允许|自定义TCP|21/21|所有要访问FTP服务器的客户端公网IP地址，多个地址之间用逗号隔开。 允许所有客户端访问时，授权对象为0.0.0.0/0。 |
|入方向|允许|自定义TCP|pasv\_min\_port/pasv\_max\_port。例如：50000/50010|所有要访问FTP服务器的客户端公网IP地址，多个地址之间用逗号隔开。 允许所有客户端访问时，授权对象为0.0.0.0/0。 |

## 步骤四：客户端测试

FTP客户端、Windows命令行工具或浏览器均可用来测试FTP服务器。本文以Windows Server 2012 R2 64位系统的本地主机作为FTP客户端，介绍FTP服务器的访问步骤。

1.  在本地主机，打开**这台电脑**。

2.  在地址栏中输入`ftp://<FTP服务器公网IP地址>:FTP端口`，本文中为Linux实例的公网IP地址。例如：`ftp://121.43.XX.XX:21`

3.  在弹出的**登录身份**对话框中，输入已设置的FTP用户名和密码，然后单击**登录**。

    登录后，您可以查看到FTP服务器指定目录下的文件，例如：测试文件testfile.txt。


## vsftp配置文件及参数说明

/etc/vsftpd目录下文件说明如下：

-   /etc/vsftpd/vsftpd.conf是vsftpd的核心配置文件。
-   /etc/vsftpd/ftpusers是黑名单文件，此文件中的用户不允许访问FTP服务器。
-   /etc/vsftpd/user\_list是白名单文件，此文件中的用户允许访问FTP服务器。

配置文件vsftpd.conf参数说明如下：

-   用户登录控制参数说明如下表所示。

    |参数|说明|
    |:-|:-|
    |anonymous\_enable=YES|接受匿名用户|
    |no\_anon\_password=YES|匿名用户login时不询问口令|
    |anon\_root=（none）|匿名用户主目录|
    |local\_enable=YES|接受本地用户|
    |local\_root=（none）|本地用户主目录|

-   用户权限控制参数说明如下表所示。

    |参数|说明|
    |:-|:-|
    |write\_enable=YES|可以上传文件（全局控制）|
    |local\_umask=022|本地用户上传的文件权限|
    |file\_open\_mode=0666|上传文件的权限配合umask使用|
    |anon\_upload\_enable=NO|匿名用户可以上传文件|
    |anon\_mkdir\_write\_enable=NO|匿名用户可以建目录|
    |anon\_other\_write\_enable=NO|匿名用户修改删除|
    |chown\_username=lightwiter|匿名上传文件所属用户名|


## 常见问题

-   问题一：本地主机为Windows系统，为什么我无法下载FTP服务器中的文件？

    您需要根据以下操作步骤，开启IE浏览器的下载权限。

    1.  在本地主机中打开IE浏览器。
    2.  在浏览器的右上角单击![IE图标](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5531787161/p261673.png)图标，然后单击**Internet 选项**。
    3.  在**Internet 选项**对话框的顶部，单击**安全**页签。
    4.  在**选择一个区域以查看或更改安全设置**区域，单击**Internet**，然后在**该区域的安全级别**区域，单击**自定义级别**。
    5.  选择**下载** \> **文件下载** \> **启用**，然后单击**确定**。
    6.  单击**应用**，然后单击**确定**。
-   问题二：在Windows系统中，使用命令行工具、浏览器等方式连接FTP服务器报错如何处理？

    您可以根据FTP的报错信息手动排查问题。当您的报错难以排查解决时，建议您使用第三方FTP客户端连接工具。例如：FileZilla。下载地址为[FileZilla](https://filezilla-project.org/download.php)。本示例介绍使用FileZilla连接匿名模式的FTP服务器。

    **说明：** 如果连接FTP服务器时的报错始终无法解决，建议您[提交工单](https://workorder-intl.console.aliyun.com/console.htm)。

    1.  在Linux系统的FTP服务器中，安装vsftpd。

        具体操作，请参见[步骤一：安装vsftpd](#section_821_887_8np)。如果您已安装vsftpd，请跳过该步骤。

    2.  配置vsftpd为匿名模式。
        1.  运行以下命令，修改配置文件/etc/vsftpd/vsftpd.conf。

            如果您在安装vsftpd时，使用的是`apt install vsftpd`安装命令，则配置文件路径为/etc/vsftpd.conf。

            ```
            vim /etc/vsftpd/vsftpd.conf
            ```

        2.  按i进入编辑模式。
        3.  将匿名上传权限的注释去掉，修改为`anon_upload_enable=YES`。
        4.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。

            修改后的配置文件，如下图所示。

            ![vsftpd配置文件](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0118773061/p102865.png)

        5.  运行以下命令更改/var/ftp/pub目录的权限，为FTP用户添加写权限。

            /var/ftp/pub为FTP服务默认的文件目录。

            ```
            chmod o+w /var/ftp/pub/
            ```

        6.  运行以下命令重新加载配置文件。

            ```
            systemctl restart vsftpd.service
            ```

    3.  下载并安装FileZilla。
    4.  通过FileZilla连接匿名模式的FTP服务器。
        1.  打开FileZilla客户端。
        2.  在顶部菜单栏，选择**文件** \> **站点管理器**。
        3.  在**站点管理器**对话框的左下角，单击**新站点**。
        4.  输入新站点的名称，并完成站点配置。

            ![filezilla](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7690838161/p261708.png)

            具体的配置项说明如下：

            -   新站点名称：您自定义的站点名称。例如`test-01`。
            -   协议：FTP-文件传输协议。
            -   主机：FTP服务器公网IP地址。本文中为Linux实例的公网IP地址，例如`121.43.XX.XX`。
            -   端口：21。
            -   登录类型：匿名。

                本示例中使用FTP客户端连接匿名模式的FTP服务器。如果您需要使用FTP用户密码连接FTP服务器，则登录类型需要设置为正常，并需要配置用户和密码信息。

        5.  单击**连接**。

            连接成功后，您可以对文件进行上传、下载和删除等操作。FileZilla工具界面如下图所示。

            ![filezilla](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5531787161/p261717.png)

            图中各区域的信息说明如下表所示。

            |序号|说明|
            |--|--|
            |①|显示命令、FTP连接状态和任务执行结果。|
            |②|本地区域，显示本地主机的目录信息。|
            |③|远程区域，显示FTP服务器的目录信息。匿名模式下，默认目录为/pub。|
            |④|记录区域，可查看FTP任务的队列信息和日志信息。|


对FTP服务进行安全加固。具体操作，请参见[安全加固方案](https://www.alibabacloud.com/help/zh/doc-detail/37452.htm)。

