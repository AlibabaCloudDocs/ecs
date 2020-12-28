# 安装和使用GitLab

GitLab是Ruby开发的自托管的Git项目仓库，可通过Web界面访问公开的或者私人的项目。本教程介绍如何安装和使用GitLab。

使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。

您已创建部署GitLab的实例，要求如下：

-   部署GitLab的实例要求至少使用2个vCPU和4GiB的内存，本示例中使用的相关资源版本如下。
    -   实例规格：ecs.c6.large
    -   操作系统：CentOS 7.2 64位
-   已添加如下表所示的安全组规则。具体步骤，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

    |方向|协议/应用|端口/范围|源地址|
    |--|-----|-----|---|
    |入方向|HTTP\(80\)|80|0.0.0.0/0|




## 使用镜像部署GitLab环境

1.  进入[GitLab代码管理（Centos 64位 \| GitLab）](https://market.aliyun.com/products/55530001/jxsc000067.html?spm=5176.730005.0.0.LuTu)镜像详情页面，单击**立即购买**，然后按界面提示完成配置选型并购买ECS实例。实例配置详情，请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。

2.  远程连接ECS实例。连接方式请参见[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

3.  运行/alidata目录下的gitlab\_opennet.sh脚本，开启远程访问。

    **说明：** GitLab镜像部署成功后默认禁止远程访问。您需要开启远程访问，才能通过ECS服务器的公网IP地址访问GitLab的登录界面。更多详情，请参见[镜像帮助文档](http://zy-res.oss-cn-hangzhou.aliyuncs.com/aliyun_Market_files/gitlab%E4%BB%A3%E7%A0%81%E7%AE%A1%E7%90%86%EF%BC%88centos%2064%E4%BD%8D%20%20gitlab%EF%BC%89.pdf?spm=5176.730006-jxsc000067.102.9.J5BUL1&file=gitlab%E4%BB%A3%E7%A0%81%E7%AE%A1%E7%90%86%EF%BC%88centos%2064%E4%BD%8D%20%20gitlab%EF%BC%89.pdf)。

4.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

5.  在左侧导航栏，单击**实例与镜像** \> **实例**。

6.  在顶部菜单栏左上角处，选择地域。

7.  在实例列表页面，找到所购ECS实例，并在**IP 地址**列获取该实例的公网IP地址。

8.  在浏览器地址栏输入公网IP地址，访问GitLab主页。


## 手动部署GitLab环境

1.  安装依赖包。

    ```
    sudo yum install -y curl policycoreutils-python openssh-server
    ```

    **说明：** 本教程中示例场景的操作系统为CentOS 7.2 64位。如果您使用CentOS 8系统的ECS实例， 运行以上命令将出现找不到依赖包`policycoreutils-python`的问题，原因是CentOS 8的软件源中没有包含该依赖包。该依赖包不影响部署GitLab，您可以忽略该问题继续运行下文中的命令。

2.  设置SSH开机自启动并启动SSH服务。

    ```
    sudo systemctl enable sshd
    sudo systemctl start sshd
    ```

3.  安装Postfix来发送通知邮件。

    ```
    sudo yum install postfix
    ```

4.  设置Postfix开机自启动。

    ```
    sudo systemctl enable postfix
    ```

5.  启动Postfix服务。

    1.  运行命令`vim /etc/postfix/main.cf`打开main.cf文件，找到下图内容：

        ![set_inet](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9512649951/p38837.png)

    2.  按i进入编辑模式。

    3.  将这行代码改为`inet_interfaces = all`。

    4.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。

    5.  运行命令`sudo systemctl start postfix`启动Postfix服务。

6.  添加GitLab软件包仓库。

    ```
     curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
    ```

7.  安装GitLab。

    ```
    sudo EXTERNAL_URL="GitLab服务器的公网IP地址" yum install -y gitlab-ce
    ```

    **说明：** 您可从ECS管理控制台的实例列表页面找到GitLab服务器的公网IP地址。

8.  使用浏览器访问GitLab服务器的公网IP地址。

    返回页面如下图所示，表示环境搭建成功，并且您需要设置新密码。

    ![gitlab1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9512649951/p92789.png)


## 使用GitLab

1.  登录GitLab。

    在浏览器的地址栏中，输入ECS服务器的公网IP即可进入GitLab的登录界面，首次登录使用用户名`root`，密码为首次访问GitLab时设置的新密码。

    ![gl2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9512649951/p92794.png)

    登录成功后界面如下。

    ![gl3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9512649951/p92797.png)

2.  创建Project。

    1.  使用Linux自带的软件源安装Git工具。

        ```
        yum install git
        ```

        ![install_git](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9512649951/p12262.png)

    2.  生成密钥文件。

        使用如下命令生成密钥文件.ssh/id\_rsa。

        ```
        ssh-keygen
        ```

        ![密钥](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9512649951/p12263.png)

        使用如下命令查看公钥文件id\_rsa.pub中的内容。在下一步操作中，您需要粘贴该内容到GitLab服务器的SSH-key的配置文件中。

        ```
        cat .ssh/id_rsa.pub
        ```

        ![公钥](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9512649951/p12264.png)

    3.  在GitLab的主页中新建一个Project。

        ![new_project](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0612649951/p12265.png)

        ![new_project_2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0612649951/p12274.png)

    4.  添加ssh key，导入步骤2中生成的密钥文件内容。

        ![import-sshkey-1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0612649951/p12266.png)

        ![import-sshkey-2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0612649951/p12275.png)

        ssh key添加完成后，如下图所示。

        ![import-ssh-key-complete](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0612649951/p12267.png)

    5.  保存项目地址，该地址在进行克隆操作时需要用到。

        ![项目地址](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0612649951/p12268.png)

3.  简单配置。

    1.  配置使用Git仓库的人员姓名。

        ```
        git config --global user.name "testname" 
        ```

    2.  配置使用Git仓库的人员email，填写自己的公司邮箱。

        ```
        git config --global user.email "abc@example.com" 
        ```

    3.  克隆项目，在本地生成同名目录，并且目录中会有所有的项目文件。

        ```
        git clone git@iZxxxxxxxxxxxxxxxxx3Z:root/test.git
        ```

        ![简单配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0612649951/p12269.png)

4.  上传文件。

    1.  进入到项目目录。

        ```
        cd test/ 
        ```

    2.  创建需要上传到GitLab中的目标文件。

        ```
        echo "test" > /root/test.sh
        ```

    3.  将目标文件或者目录复制到项目目录下。

        ```
        cp /root/test.sh ./ 
        ```

        ![上传文件](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0612649951/p12270.png)

    4.  将test.sh文件加入到索引中。

        ```
        git add test.sh
        ```

    5.  将test.sh提交到本地仓库。

        ```
        git commit -m "test.sh"
        ```

    6.  将文件同步到GitLab服务器上。

        ```
        git push -u origin master
        ```

        ![文件同步命令](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0612649951/p12271.png)

        在网页中查看上传的test.sh文件已经同步到GitLab中。

        ![文件同步结果](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0612649951/p12272.png)


