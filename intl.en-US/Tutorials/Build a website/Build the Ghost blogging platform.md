# Build the Ghost blogging platform

Ghost is a free open source blogging platform developed based on Node.js. The platform is used to simplify the online publishing process for individual blogs and online publications. This topic describes how to deploy the Ghost blogging platform on an ECS instance that runs CentOS 7.

An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).

You can use Alibaba Cloud services to scale up or scale out your service capacity. For example, you can optimize your business by using the following ways:

-   Scale up the vCPUs and memory of a single ECS instance to enhance the processing performance.
-   Add multiple ECS instances and implement load balancing among these instances.
-   Use Auto Scaling to automatically increase or decrease the number of ECS instances.
-   Use Object Storage Service \(OSS\) to store large volumes of data such as static web pages, pictures, and videos.

An ecs.c6.large ECS instance is used in the examples of this topic to build the Ghost blogging platform. The procedure described in this topic is applicable to individual users that are new to website construction with ECS instances.

**Note:** You can build the Ghost blogging platform in development or production mode. If you are building the Ghost blogging platform for the first time, we recommend that you use the development mode for ease of debugging.

## Procedure

To build the Ghost blogging platform on an ECS instance, perform the following operations:

-   [Step 1: Create a Linux ECS instance](#section_lll_v4o_d8l)
-   [Step 2: Deploy the web environment](#section_3as_stl_g30)
-   [Step 3: Install Ghost](#section_ab9_fr6_oj6)
-   [Step 4: Purchase a domain name](#section_vhr_y2k_pga)
-   [Step 5: Apply for an ICP filing](#section_6ph_sb6_rb4)
-   [Step 6: Resolve the domain name to the IP address of the instance](#section_b35_s43_byu)

## Step 1: Create a Linux ECS instance

This section describes how to create an ECS instance. To build an individual website, you need only one ECS instance.

-   Create a Linux ECS instance. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).
-   If you have a custom image, you can create an instance from this image. For more information, see [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md).

When you configure parameters, take note of the following items:

-   **Instance Type**: For an individual website, you can select an instance type with **1 vCPU and 2 GiB** or **2 vCPUs and 4 GiB**. For more information about instance types, see [Instance families](/intl.en-US/Instance/Instance families.md).
-   **Network Type**: Select **VPC**.
-   **Bandwidth pricing**: **Assign Public IP Address** is selected in this topic. If you do not select Assign Public IP Address, the instance is not assigned a public IP address. In this case, if you want to enable the ECS instance to access the Internet, you must create an elastic IP address \(EIP\) and associate the EIP with the ECS instance. The actual configuration depends on your requirements.
-   **Image**: A Linux image such as CentOS 7.2 64-bit in the public image list is used in this topic.

After the instance is created, the system sends you a text message and email to notify you of the information about the instance, such as the instance name, public IP address, and internal IP address. You can use the information to log on to the ECS console and manage the instance.

The system notifies you of important information by sending text messages. To authenticate some important operations such as restarting or stopping the instance, you must use your mobile phone to receive verification codes. Therefore, keep your mobile phone reachable after you bind your mobile number to your Alibaba Cloud account.

## Step 2: Deploy the web environment

This section describes how to deploy the web environment by installing NGINX.

Prerequisites:

-   Your instance is able to connect to the Internet.
-   A tool for connecting to the Linux ECS instance is installed, such as SecureCRT.

1.  Open the SecureCRT client and specify the information of the ECS instance to which you want to log on.

    1.  Specify the name of the session for connecting to the ECS instance.

    2.  Select **SSH** from the Protocol drop-down list.

    3.  Enter the host IP address in the Hostname field and specify the username.

    4.  Click **Connect**.

    ![Configure logon information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0529919951/p12471.png)

2.  Enter the root username and password.

    ![Enter the username and password](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0529919951/p12472.png)

3.  Add the NGINX repository.

    ```
    rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
    ```

    The software package provides NGINX 1.10.2.

    **Note:** The actual version may vary depending on the package that you downloaded.

4.  Install NGINX.

    ```
    yum -y install nginx
    ```

5.  Enable NGINX to run upon system startup.

    ```
    systemctl enable nginx.service
    ```

6.  Start NGINX and check the NGINX service status.

    ```
    systemctl start nginx.service
    systemctl status nginx.service
    ```

7.  Enter the public IP address of the ECS instance in the address bar of your browser to view the default NGINX web page.

    ![NGINX web page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0529919951/p12474.png)


## Step 3: Install Ghost

1.  Run the following command to update system software to the latest version:

    ```
    yum -y update
    ```

2.  Install Node.js.

    1.  Install Extra Packages for Enterprise Linux \(EPEL\).

        ```
        yum install epel-release -y
        ```

    2.  Install Node.js and npm.

        ```
        yum install nodejs npm --enablerepo=epel
        ```

    3.  Install the package manager for Node.js.

        ```
        npm install -g n
        ```

    4.  Install Node.js of a stable version.

        Node.js `12.16.3` is used in this example.

        ```
        n 12.16.3
        ```

    5.  Run the n command to select Node.js 12.16.3.

    6.  Edit the environment configuration file.

        ```
        vim ~/.bash_profile
        ```

    7.  Enter i to switch to the edit mode and add the following information to the end of the file:

        ```
        export N_PREFIX=/usr/local/bin/node
        export PATH=$N_PREFIX/bin:$PATH
        ```

        After the editing is complete, press the Esc key to exit the edit mode and enter `:wq` to save and close the file.

    8.  Run the following command to apply the configuration:

        ```
        source ~/.bash_profile
        ```

    9.  Install the process manager to control Node.js applications.

        This process manager keeps the applications in the running state.

        ```
        npm install pm2 -g
        ```

    10. Run the `node -v` and `npm -v` commands to check the Node.js version.

3.  Install Ghost.

    1.  Create a directory to which to install Ghost.

        ```
        mkdir -p /var/www/ghost
        ```

    2.  Go to the Ghost installation directory and run the following command to download the latest Ghost package:

        ```
        cd /var/www/ghost
        wget https://ghost.org/zip/ghost-latest.zip
        mv ghost-latest.zip ghost.zip
        ```

    3.  Decompress the Ghost package.

        ```
        yum install unzip -y
        unzip ghost.zip
        ```

    4.  Install GCC and C++ compilers.

        ```
        yum -y install gcc gcc-c++
        ```

    5.  Use npm to install Ghost.

        ```
        npm install -production
        ```

    6.  Run the `npm start` command to start Ghost and check whether Ghost is installed.

        If the following command output is displayed, Ghost is started. You can press Ctrl+C to close Ghost.

        ```
        [2020-04-13 04:00:01] INFO Ghost is running in development...
        [2020-04-13 04:00:01] INFO Listening on: 127.0.0.1:2368
        [2020-04-13 04:00:01] INFO Url configured as: http://121.196. *. */
        [2020-04-13 04:00:01] INFO Ctrl+C to shut down
        [2020-04-13 04:00:01] INFO Ghost boot 2.185s
        ```

    7.  Modify the config.development.json file in the /var/www/ghost/core/shared/config/env directory.

        ```
        vi /var/www/ghost/core/shared/config/env/config.development.json
        ```

    8.  Set the domain name of Ghost to the URL in the config.development.json file.

        ![ghost1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0529919951/p98140.png)

        Press the Esc key to exit the edit mode and enter `:wq` to save and close the file.

4.  Specify NGINX as the reverse proxy for Ghost.

    1.  Go to the NGINX configuration directory.

        ```
        cd /etc/nginx/conf.d/
        ```

    2.  Create a NGINX configuration file for Ghost.

        ```
        vim /etc/nginx/conf.d/ghost.conf
        ```

    3.  Add the following content to the ghost.conf file and set server\_name to the domain name of Ghost that is used in your actual runtime environment.

        ```
        upstream ghost {
            server 127.0.0.1:2368;
        }
        server {
            listen      80;
            server_name myghostblog.com;
        
            access_log  /var/log/nginx/ghost.access.log;
            error_log   /var/log/nginx/ghost.error.log;
        
            proxy_buffers 16 64k;
            proxy_buffer_size 128k;
        
            location / {
                proxy_pass  http://ghost;
                proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
                proxy_redirect off;
        
                proxy_set_header    Host            $host;
                proxy_set_header    X-Real-IP       $remote_addr;
                proxy_set_header    X-Forwarded-For $proxy_add_X_forwarded_for;
                proxy_set_header    X-Forwarded-Proto https;
            }
        }
        ```

    4.  Change the name of the default configuration file default.conf to default.conf.bak, so NGINX is applicable only to ghost.conf.

        ```
        mv default.conf default.conf.bak
        ```

    5.  Restart NGINX.

        ```
        systemctl restart nginx.service
        ```

5.  Start Ghost.

    ```
    cd /var/www/ghost/
    npm start
    ```

6.  Connect to the Ghost blogging platform.

    1.  Enter the URL http://<Public IP address of the ECS instance\> or http://<Domain name of the Ghost blogging platform\> in the address bar of your browser to connect to the Ghost blogging platform.

        ![Ghost web page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0529919951/p12480.png)

        **Note:** If the system returns Error Code 502, check whether the firewall is disabled.

    2.  Enter the URL http://<Public IP address of the ECS instance/ghost\> in the address bar of your browser if you want to edit your Ghost blogging platform.

        ![Edit the Ghost blogging platform](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0529919951/p12481.png)


## Step 4: Purchase a domain name

You can specify a unique domain name for your website. This allows users to visit your website by using a simple domain name instead of a complex IP address.

We recommend that you go to Alibaba Cloud to purchase a domain name. For more information, see [Register a generic domain name](/intl.en-US/Quick Start/Register a generic domain name.md).

## Step 5: Apply for an ICP filing

You must apply for an ICP filing for the domain name that is associated with a website hosted on a server in mainland China. Your website cannot provide services until you obtain the ICP filing number for the domain name.

Alibaba Cloud ICP Filing System can help you simplify the ICP filing procedure. You can apply for an ICP filing free of charge. Typically, the review takes about 20 days.

## Step 6: Resolve the domain name to the IP address of the instance

You must resolve the domain name to the IP address of the ECS instance, so users can visit your website by using the domain name. For more information, see[Configure the DNS settings for a domain name](https://www.alibabacloud.com/help/doc-detail/58131.htm).

