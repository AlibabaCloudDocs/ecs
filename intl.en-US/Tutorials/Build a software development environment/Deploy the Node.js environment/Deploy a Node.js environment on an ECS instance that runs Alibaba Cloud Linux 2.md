# Deploy a Node.js environment on an ECS instance that runs Alibaba Cloud Linux 2

This topic describes how to install Node.js and deploy a project on an ECS instance that runs Alibaba Cloud Linux 2.

An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).

Node.js is a JavaScript runtime environment built on the Chrome V8 engine. You can use Node.js to build an online application that supports extension. Node.js uses an event-driven and non-blocking I/O model. This lightweight and efficient model is suitable for data-intensive real-time applications that run on distributed devices. The Node.js package manager \(npm\) is the largest ecosystem of open source libraries in the world. Node.js is applicable to the following typical scenarios:

-   Real-time applications: instant messaging and real-time notifications, such as Socket.IO.
-   Distributed applications: efficient parallel I/O to consume existing data.
-   Utilities: a variety of utilities from frontend compression and deployment applications such as grunt to desktop graphical user interface applications.
-   Game applications: real-time and high-concurrency applications in the gaming field, such as the Pomelo framework of NetEase.
-   Web rendering applications: applications with stable APIs to improve the rendering performance of web pages.
-   Consistent frontend and backend programming environments: applications that allow frontend developers to take on server-side development, such as the full-stack Javascript MongoDB, Express.js, AngularJS, and Node.js. \(MEAN\) framework.

## Step 1: Create and connect to an ECS instance

1.  Use the Alibaba Cloud Linux 2.1903 LTS 64-bit public image to create an ECS instance. For more information, see [Create an ECS instance]().

2.  Connect to the ECS instance. For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).


## Step 2: Deploy the Node.js environment

Deploy the Node.js environment by using one of the following methods:

-   NVM

    Node Version Manager \(NVM\) is the software used to manage Node.js versions. You can use NVM to switch among Node.js versions with ease. NVM is suitable for developers who are dedicated to Node.js or users who want to efficiently update or switch among Node.js versions.

    To install multiple Node.js versions by using NVM, perform the following steps:

    1.  Use Git to clone source code to the local ~/.nvm directory, and check for the latest update.

        ```
        yum install git
        git clone https://github.com/cnpm/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
        ```

    2.  Activate NVM.

        ```
        echo ". ~/.nvm/nvm.sh" >> /etc/profile
        source /etc/profile
        ```

    3.  Retrieve a list of all Node.js versions.

        ```
        nvm list-remote
        ```

    4.  Install multiple Node.js versions.

        ```
        nvm install v6.9.5
        nvm install v7.4.0
        ```

    5.  Run the `nvm ls` command to check the installed Node.js versions.

        v7.4.0 is used in this example. The following command output is displayed:

        ```
        [root@iZXXXXZ .nvm]# nvm ls
                 v6.9.5
        ->       v7.4.0
                 system
        stable -> 7.4 (-> v7.4.0) (default)
        unstable -> 6.9 (-> v6.9.5) (default)
        ```

    6.  Run the `nvm use <Version number>` command to switch among the Node.js versions.

        The Node.js version is switched to v7.4.0 in this example. The following command output is displayed:

        ```
        [root@iZXXXXZ .nvm]# nvm use v7.4.0
        Now using node v7.4.0
        ```

-   Binary file

    The installation package used in the deployment is a compiled binary file. After you decompress the package, the node and npm files already exist in the bin folder. Therefore, you do not need to recompile the binary file.

    To deploy the Node.js environment by using the binary file, perform the following steps:

    1.  Download the Node.js installation package.

        ```
        wget https://nodejs.org/dist/v6.9.5/node-v6.9.5-linux-x64.tar.xz
        ```

    2.  Decompress the package.

        ```
        tar xvf node-v6.9.5-linux-x64.tar.xz
        ```

    3.  After you create a soft link, you can run node and npm commands directly in any directory.

        ```
        ln -s /root/node-v6.9.5-linux-x64/bin/node /usr/local/bin/node
        ln -s /root/node-v6.9.5-linux-x64/bin/npm /usr/local/bin/npm
        ```

    4.  Check the versions of node and npm.

        ```
        node -v
        npm -v
        ```

        At this point, the Node.js environment is installed. By default, the software is installed in the /root/node-v6.9.5-linux-x64/ directory.

    5.  To install the software in another directory such as /opt/node/, run the following commands in sequence:

        ```
        mkdir -p /opt/node/
        mv /root/node-v6.9.5-linux-x64/* /opt/node/
        rm -f /usr/local/bin/node
        rm -f /usr/local/bin/npm
        ln -s /opt/node/bin/node /usr/local/bin/node
        ln -s /opt/node/bin/npm /usr/local/bin/npm
        ```


## Step 3: Deploy a test project

1.  Create the example.js project file.

    ```
    cd ~
    touch example.js
    ```

2.  Modify the example.js project file.

    1.  Run the following command to open example.js:

        ```
        vim example.js
        ```

    2.  Press the I key to enter the edit mode.

    3.  Paste the following content to the project file:

        ```
        const http = require('http');
        const hostname = '0.0.0.0';
        const port = 3000;
        const server = http.createServer((req, res) => { 
            res.statusCode = 200;
            res.setHeader('Content-Type', 'text/plain');
            res.end('Hello World\n');
        }); 
        
        server.listen(port, hostname, () => { 
            console.log(`Server running at http://${hostname}:${port}/`);
        });
        ```

        **Note:** In this example, port 3000 is specified as the service port. You can also set another port in your actual runtime environment. However, you must add an inbound rule to the security group of the ECS instance to allow traffic on the specified port. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    4.  Press the Esc key to exit the edit mode. Enter :wq and press the Enter key to save and close the file.

3.  Run the project and obtain the port number of the project.

    ```
    node ~/example.js &
    ```

4.  Run the following command to check whether the deployed instance is listening on the specified port.

    ```
    netstat -tpln
    ```

    In this example, port 3000 is included in the command output, indicating that the instance is listening on the port.

5.  Log on to the [ECS console](https://ecs.console.aliyun.com), and add an inbound rule to the security group of the ECS instance to allow traffic on the specified port, such as port 3000 in this example.

    For more information about how to add security group rules, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

6.  Enter `http://<Public IP address of the ECS instance>:Port number` in the address bar of your browser to access the project.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5329919951/p12144.png)


