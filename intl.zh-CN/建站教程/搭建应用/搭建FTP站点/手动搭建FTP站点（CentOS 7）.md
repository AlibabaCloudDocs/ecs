---
keyword: [搭建FTP, CentOS 7.2搭建FTP, CentOS 7搭建FTP]
---

# 手动搭建FTP站点（CentOS 7）

vsftpd（very secure FTP daemon）是Linux下的一款小巧轻快、安全易用的FTP服务器软件。本教程介绍如何在Linux实例上安装并配置vsftpd。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.alibabacloud.com/register/intl_register.htm)。
-   已创建ECS实例并为实例分配了公网IP地址。若尚未创建，请参见[创建方式导航](/intl.zh-CN/实例/创建实例/创建方式导航.md)。

FTP（File Transfer Protocol）是一种文件传输协议，基于客户端/服务器架构，支持以下两种工作模式：

-   主动模式：客户端向FTP服务器发送端口信息，由服务器主动连接该端口。
-   被动模式：FTP服务器开启并发送端口信息给客户端，由客户端连接该端口，服务器被动接受连接。

**说明：** 大多数FTP客户端都在局域网中，没有独立的公网IP地址，且有防火墙阻拦，主动模式下FTP服务器成功连接到客户端比较困难。因此，如无特殊需求，建议您将FTP服务器配置为被动模式。

FTP支持以下三种认证模式：

-   匿名用户模式：任何人无需密码验证就可以直接登录到FTP服务器。这种模式最不安全，一般只用来保存不重要的公开文件，不推荐在生产环境中使用。
-   本地用户模式：通过Linux系统本地账号进行验证的模式，相较于匿名用户模式更安全。
-   虚拟用户模式：FTP服务器的专有用户。虚拟用户只能访问Linux系统为其提供的FTP服务，而不能访问Linux系统的其它资源，进一步增强了FTP服务器的安全性。

本教程中介绍的FTP服务器配置方法如下表所示。

|工作模式|匿名用户|本地用户|
|----|----|----|
|主动模式|主动模式下，开通匿名用户向FTP服务器上传文件权限的配置方法。|主动模式下，使用本地用户访问FTP服务器的配置方法。|
|被动模式|无。|被动模式下，使用本地用户访问FTP服务器的配置方法。|

本教程示例步骤使用以下资源版本：

-   实例规格：ecs.c6.large
-   操作系统：CentOS 7.2 64位
-   vsftpd：3.0.2
-   浏览器：Internet Explorer 11

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

本示例提供两种方式配置vsftpd：匿名用户模式或本地用户模式。请根据您的需求选择其中一种方式进行配置。

方式一：配置主动模式下匿名用户上传文件权限。

1.  修改配置文件/etc/vsftpd/vsftpd.conf。

    **说明：** 如果您在安装vsftpd时，使用的是`apt install vsftpd`安装命令，则配置文件路径为/etc/vsftpd.conf。

    1.  运行vim /etc/vsftpd/vsftpd.conf命令打开配置文件。

    2.  按i进入编辑模式。

    3.  将匿名上传权限的注释去掉，修改为`anon_upload_enable=YES`。

    4.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。

    修改后的配置文件，如下图所示。

    ![vsftpd配置文件](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0118773061/p102865.png)

2.  运行以下命令更改/var/ftp/pub目录的权限，为FTP用户添加写权限。

    ```
    chmod o+w /var/ftp/pub/
    ```

3.  运行以下命令重新加载配置文件。

    ```
    systemctl restart vsftpd.service
    ```

    ![匿名权限2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2419459951/p12603.png)


方式二：配置本地用户访问FTP服务器。

1.  运行以下命令为FTP服务创建一个Linux用户。本示例中，该用户名为ftptest。

    ```
    adduser ftptest
    ```

2.  运行以下命令修改ftptest用户的密码。

    ```
    passwd ftptest
    ```

3.  运行以下命令创建一个供FTP服务使用的文件目录。

    ```
    mkdir /var/ftp/test
    ```

4.  运行以下命令更改/var/ftp/test目录的拥有者为ftptest。

    ```
    chown -R ftptest:ftptest /var/ftp/test
    ```

5.  修改vsftpd.conf配置文件。

    1.  运行vim /etc/vsftpd/vsftpd.conf命令打开配置文件。

    2.  按i进入编辑模式。

    3.  根据实际需要，配置FTP服务器为主动模式或被动模式。

        **说明：** 修改和添加配置文件内的信息时，请注意格式问题。例如，添加多余的空格会造成无法重启服务的结果。

        -   配置FTP为主动模式的参数如下：

            ```
            #除下面提及的参数外，其他参数保持默认值即可。
            
            #修改下列参数的值
            anonymous_enable=NO      #禁止匿名登录FTP服务器
            local_enable=YES         #允许本地用户登录FTP服务器
            listen=YES               #监听IPv4 sockets
            
            #在行首添加#注释掉以下参数
            #listen_ipv6=YES          #关闭监听IPv6 sockets
            
            #添加下列参数
            chroot_local_user=YES    #全部用户被限制在主目录
            chroot_list_enable=YES   #启用例外用户名单
            chroot_list_file=/etc/vsftpd/chroot_list  #指定例外用户列表文件，列表中的用户不被锁定在主目录
            allow_writeable_chroot=YES  
            local_root=/var/ftp/test #设置本地用户登录后所在的目录
            ```

        -   配置FTP为被动模式的参数如下：

            ```
            #除下面提及的参数外，其他参数保持默认值即可。
            
            #修改下列参数的值
            anonymous_enable=NO          #禁止匿名登录FTP服务器
            local_enable=YES             #允许本地用户登录FTP服务器
            listen=YES                   #监听IPv4 sockets
            #在行首添加#注释掉以下参数
            #listen_ipv6=YES             #关闭监听IPv6 sockets
            
            #添加下列参数
            local_root=/var/ftp/test     #设置本地用户登录后所在目录
            chroot_local_user=YES        #全部用户被限制在主目录
            chroot_list_enable=YES       #启用例外用户名单
            chroot_list_file=/etc/vsftpd/chroot_list  #指定例外用户列表文件，列表中用户不被锁定在主目录
            allow_writeable_chroot=YES
            pasv_enable=YES                    #开启被动模式
            pasv_address=<FTP服务器公网IP地址>  #本教程中为Linux实例公网IP
            pasv_min_port=<port number>          #设置被动模式下，建立数据传输可使用的端口范围的最小值
            pasv_max_port=<port number>          #设置被动模式下，建立数据传输可使用的端口范围的最大值
            ```

            **说明：** 建议您把端口范围设置在一段比较高的范围内，例如50000~50010，有助于提高访问FTP服务器的安全性。

        更多参数的详细信息，请参见[vsftp配置文件及参数说明](#section_t9a_ors_44c)。

    4.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。

6.  创建chroot\_list文件，并在文件中写入例外用户名单。

    1.  运行vim /etc/vsftpd/chroot\_list命令创建chroot\_list文件。

    2.  按i进入编辑模式。

    3.  输入例外用户名单。此名单中的用户不会被锁定在主目录，可以访问其他目录。

    4.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。

    **说明：** 没有例外用户时，也必须创建chroot\_list文件，内容可为空。

7.  运行以下命令重启vsftpd服务。

    ```
    systemctl restart vsftpd.service
    ```


## 步骤三：设置安全组

搭建好FTP站点后，在实例安全组的入方向添加规则并放行下列FTP端口。具体操作，请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

**说明：** 大多数客户端位于局域网中，IP地址是经过转换的，因此ipconfig或ifconfig命令返回的IP不一定是客户端的真实公网IP地址。若后续客户端无法登录FTP服务器，请重新确认其公网IP地址。

-   FTP为主动模式时：端口21。配置详情如下表所示。

    |规则方向|授权策略|协议类型|端口范围|授权对象|
    |----|----|----|----|----|
    |入方向|允许|自定义TCP|21/21|所有要访问FTP服务器的客户端公网IP地址，多个地址之间用逗号隔开。 允许所有客户端访问时，授权对象为0.0.0.0/0。 |

-   FTP为被动模式时：端口21，以及配置文件/etc/vsftpd/vsftpd.conf中参数pasv\_min\_port和pasv\_max\_port之间的所有端口。配置详情如下表所示。

    |规则方向|授权策略|协议类型|端口范围|授权对象|
    |----|----|----|----|----|
    |入方向|允许|自定义TCP|21/21|所有要访问FTP服务器的客户端公网IP地址，多个地址之间用逗号隔开。 允许所有客户端访问时，授权对象为0.0.0.0/0。 |
    |入方向|允许|自定义TCP|pasv\_min\_port/pasv\_max\_port|所有要访问FTP服务器的客户端公网IP地址，多个地址之间用逗号隔开。 允许所有客户端访问时，授权对象为0.0.0.0/0。 |


## 步骤四：客户端测试

FTP客户端、Windows命令行工具或浏览器均可用来测试FTP服务器。本教程以Google Chrome浏览器为例，介绍FTP服务器的访问步骤。

**说明：** 使用浏览器访问FTP服务器出错时，建议您清除浏览器缓存后再尝试。

1.  打开客户端的Google Chrome浏览器。

2.  在地址栏中输入`ftp://<FTP服务器公网IP地址>:FTP端口`，本教程中为Linux实例的公网IP地址。例如：`ftp://39.0.**.**:21`

3.  在弹出的对话框中，输入用户名和密码，即可对FTP文件进行相应权限的操作。

    **说明：** 此步骤仅适用于本地用户，匿名用户无需输入用户名和密码即可登录FTP服务器。


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


对FTP服务进行安全加固。具体操作，请参见[安全加固方案](https://www.alibabacloud.com/help/zh/doc-detail/37452.htm)。

