# Manually deploy a Java web environment on an ECS instance that runs Alibaba Cloud Linux 2

This topic describes how to manually deploy a Java web environment on an ECS instance that runs Alibaba Cloud Linux 2. This topic is applicable to individual users who are new to website construction on ECS instances.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   To use ECS instances that are located in mainland China regions, make sure that you have completed real-name verification for your account.
-   An ECS instance is created. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

The following instance type and software versions are used in this topic. The operations may vary with the versions of your software.

-   Instance type: ecs.c6.large
-   Operating system: Alibaba Cloud Linux 2.1903 LTS 64-bit
-   JDK: 1.8.0\_262
-   Tomcat: 8.5.59

    **Note:** Tomcat 8.5.59 is used in this example. The installation package is constantly upgraded and you can obtain an appropriate installation package version.


## Step 1: Prepare the environment

1.  Add inbound rules to the security group of the ECS instance to allow traffic on the required ports. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    In this example, traffic on SSH port 22 and HTTP port 8080 is allowed.

2.  Connect to the instance. For more information, see[Connect to a Linux instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using VNC.md).

3.  Disable the firewall.

    1.  Run the systemctl status firewalld command to check the status of the firewall.

        ![Check the status of the firewall](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8229919951/p32172.png)

        -   If the firewall is in the inactive state, the firewall is disabled.
        -   If the firewall is in the active state, the firewall is enabled. In this example, the firewall is in the active state. Therefore, you must disable the firewall.
    2.  Disable the firewall. If the firewall is in the inactive state, skip this step.

        -   To temporarily disable the firewall, run the systemctl stop firewalld command.

            **Note:** After you run this command, the firewall is temporarily disabled. It enters the active state after you restart the instance next time.

        -   To permanently disable the firewall, run the systemctl disable firewalld command.

            **Note:** You can enable the firewall again. For more information, see [Firewalld documentation](https://firewalld.org/).

4.  Disable Security-Enhanced Linux \(SELinux\).

    1.  Run the getenforce command to check the status of SELinux.

        ![Check the status of SELinux](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8229919951/p21065.png)

        -   If the status of SELinux is Disabled, SELinux is disabled.
        -   If the status of SELinux is Enforcing, SELinux is enabled. In this example, SELinux is in the Enforcing state. You must disable SELinux.
    2.  Disable SELinux. If SELinux is in the Disabled state, skip this step.

        -   To temporarily disable SELinux, run the setenforce 0 command.

            **Note:** After you run this command, SELinux is temporarily disabled. It enters the enforcing state after you restart Linux next time.

        -   To permanently disable SELinux, do as follows: Run the vi /etc/selinux/config command, edit the SELinux configuration file, and press Enter. Move your pointer to the line of `SELINUX=enforcing` and press `i` to enter the edit mode. Change SELINUX=enforcing to `SELINUX=disabled` and press `Esc`. Then, enter `:wq` and press Enter to save and close the SELinux configuration file.

            **Note:** You can enable SELinux again. For more information, see [SELinux documentation](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/5/html/deployment_guide/ch-selinux#s1-SELinux-resources).

    3.  Restart the system to make the changes take effect.

5.  For security reasons, create a common user named www to run Tomcat.

    ```
    useradd www
    ```

6.  Run the following command to create a website root directory:

    ```
    mkdir -p /data/wwwroot/default
    ```

7.  Set the owner of the website root directory to www.

    ```
    chown -R www.www /data/wwwroot
    ```


## Step 2: Install JDK 1.8

1.  Run the yum command to search for the Java Development Kit \(JDK\) 1.8 package.

    ```
    yum -y list java*
    ```

2.  Install the JDK 1.8 package displayed in the software list.

    ```
    yum -y install java-1.8.0-openjdk-devel.x86_64
    ```

3.  Check the JDK version.

    ```
    java -version
    ```

    The following JDK version information is displayed in this example:

    ```
    openjdk version "1.8.0_262"
    OpenJDK Runtime Environment (build 1.8.0_262-b10)
    OpenJDK 64-Bit Server VM (build 25.262-b10, mixed mode)
    ```

4.  Configure environment variables.

    1.  Open the configuration file.

        ```
        vim /etc/profile
        ```

    2.  At the end of the configuration file, press the i key to enter the edit mode.

    3.  Add the following information.

        **Note:** The `JAVA_HOME` value is the path where JDK is installed. In this example, run the cd /usr/lib/jvm/ command to go to the `jvm` path and then run the ls command to check the file path where JDK is installed.

        ```
        JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.262.b10-0.1.al7.x86_64
        PATH=$PATH:$JAVA_HOME/bin
        CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
        export JAVA_HOME CLASSPATH PATH
        ```

    4.  Press the Esc key, enter `:wq`, and then press the Enter key to save and close the configuration file.

    5.  Immediately apply the environment variables.

        ```
        source /etc/profile
        ```


## Step 3: Install Apache Tomcat

1.  Run the following command to download the Tomcat 8 installation package:

    ```
    wget https://mirror.bit.edu.cn/apache/tomcat/tomcat-8/v8.5.59/bin/apache-tomcat-8.5.59.tar.gz
    ```

    **Note:** The download address of Tomcat may change. For the download address of the new version, visit the [official Tomcat website](https://tomcat.apache.org/).

2.  Decompress the Tomcat 8 installation package.

    ```
    tar -zxvf apache-tomcat-8.5.59.tar.gz
    ```

3.  Move the Tomcat files to the /user/local/tomcat directory.

    ```
    mv apache-tomcat-8.5.59 /usr/local/tomcat/
    ```

4.  Set the owner of the files to www.

    ```
    chown -R www.www /usr/local/tomcat/
    ```

    The /usr/local/tomcat/ directory contains the following subdirectories:

    -   bin: stores Tomcat script files, such as scripts used to enable and disable the Tomcat service.
    -   conf: stores various global configuration files of the Tomcat server, among which server.xml and web.xml are the most important files.
    -   webapps: specifies the main directory used for web publishing of Tomcat and stores web application files by default.
    -   logs: stores Tomcat operation log files.
5.  Configure the server.xml file.

    1.  Run the following command to switch to the /usr/local/tomcat/conf/ directory:

        ```
        cd /usr/local/tomcat/conf/
        ```

    2.  Run the following command to rename the server.xml file:

        ```
        mv server.xml server.xml_bk
        ```

    3.  Create a server.xml file.

        1.  Run the `vi server.xml` command to create a server.xml file.
        2.  Press the I key to add the following content:

            ```
            <? xml version="1.0" encoding="UTF-8"? encoding="UTF-8"?>
            <Server port="8006" shutdown="SHUTDOWN">
            <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener"/>
            <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener"/>
            <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener"/>
            <Listener className="org.apache.catalina.core.AprLifecycleListener"/>
            <GlobalNamingResources>
            <Resource name="UserDatabase" auth="Container"
             type="org.apache.catalina.UserDatabase"
             description="User database that can be updated and saved"
             factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
             pathname="conf/tomcat-users.xml"/>
            </GlobalNamingResources>
            <Service name="Catalina">
            <Connector port="8080"
             protocol="HTTP/1.1"
             connectionTimeout="20000"
             redirectPort="8443"
             maxThreads="1000"
             minSpareThreads="20"
             acceptCount="1000"
             maxHttpHeaderSize="65536"
             debug="0"
             disableUploadTimeout="true"
             useBodyEncodingForURI="true"
             enableLookups="false"
             URIEncoding="UTF-8"/>
            <Engine name="Catalina" defaultHost="localhost">
            <Realm className="org.apache.catalina.realm.LockOutRealm">
            <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
              resourceName="UserDatabase"/>
            </Realm>
            <Host name="localhost" appBase="/data/wwwroot/default" unpackWARs="true" autoDeploy="true">
            <Context path="" docBase="/data/wwwroot/default" debug="0" reloadable="false" crossContext="true"/>
            <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
            prefix="localhost_access_log." suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
            </Host>
            </Engine>
            </Service>
            </Server>
            ```

        3.  Press the Esc key, enter `:wq`, and then press the Enter key to save and close the configuration file.
6.  Configure the Java Virtual Machine \(JVM\) memory parameters.

    1.  Run the `vi /usr/local/tomcat/bin/setenv.sh` command to create a file named /usr/local/tomcat/bin/setenv.sh.

    2.  Press the I key to add the following content:

        ```
        JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'                          
        ```

    3.  Press the Esc key, enter `:wq`, and then press the Enter key to save and close the configuration file.

7.  Configure a script to make Tomcat run on system startup.

    1.  Run the following command to download the Tomcat startup script.

        **Note:** The script originates from the community and is for reference only. Alibaba Cloud does not make any guarantee, express or implied, with respect to the performance and reliability of the script, as well as potential impacts of operations on the script.

        ```
        wget http://raw.githubusercontent.com/oneinstack/oneinstack/master/init.d/Tomcat-init
        ```

    2.  Run the following command to rename Tomcat-init:

        ```
        mv Tomcat-init /etc/init.d/tomcat
        ```

    3.  Run the following command to grant the execute permission on the /etc/init.d/tomcat file:

        ```
        chmod +x /etc/init.d/tomcat
        ```

    4.  Run the following command to configure the JAVA\_HOME script.

        **Note:** The JDK version in the script must be the same as that you installed. Otherwise, Tomcat fails to start.

        ```
        sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.262.b10-0.1.al7.x86_64@' /etc/init.d/tomcat
        ```

8.  Run the following commands to enable Tomcat to run at startup:

    ```
    chkconfig --add tomcat
    chkconfig tomcat on
    ```

9.  Run the following command to start Tomcat:

    ```
    service tomcat start             
    ```


## Step 4: Deploy and verify the test project

Upload the WAR package of Java web project files to the website root directory and change the owner of files in the root directory to www. You can use a remote connection tool that has a file transfer feature or build an FTP site to upload project files. In this example, the website root directory is /data/wwwroot/default. Perform the following operations to create a Tomcat test page in the website root directory and access the page:

1.  Deploy the test file.

    ```
    echo Tomcat test > /data/wwwroot/default/index.jsp
    ```

2.  Open your browser and enter `http://<Public IP address of the ECS instance>:8080` in the address bar to connect to the ECS instance.

    The following figure shows that Tomcat is installed.

    ![Command output](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9229919951/p12137.png)


