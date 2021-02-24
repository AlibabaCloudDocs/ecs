# Manually deploy a Java web environment on an instance that runs CentOS 7

This topic describes how to manually deploy a Java web environment on an ECS instance. This topic is applicable to individual users who are new to website construction on ECS instances.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   To use ECS instances that are located in mainland China regions, make sure that you have completed real-name verification for your account.
-   An ECS instance is created. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

The following instance type and software versions are used in this topic. The operations may vary with the versions of your software.

-   Instance type: ecs.c6.large
-   Operating system: CentOS 7.4
-   Tomcat: Tomcat 8.5.53

    **Note:** Tomcat 8.5.53 is used in this example. The source code is constantly upgraded and you can obtain the appropriate version.

-   JDK: JDK 1.8.0\_241
-   FTP tool: WinSCP

## Step 1: Download the source code

1.  Click [here](https://mirrors.aliyun.com/apache/tomcat/tomcat-8/) to download Apache Tomcat.

2.  Download JDK.

    1.  Click [here](https://www.oracle.com/java/technologies/javase-downloads.html) to download the JDK installation package.

        **Note:** If you run the wget command on the instance to download the JDK installation package and an error is reported when you decompress the package, you can download the JDK installation package and upload it to the ECS instance.

    2.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    3.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

    4.  Select the region where the ECS instance is deployed.

    5.  On the **Instances** page, find the purchased instance, and view the public IP address of the instance in the **IP Address** column.

    6.  In WinSCP, connect to the Linux instance by using the public IP address.

    7.  Upload the downloaded Apache Tomcat and JDK installation packages to the root directory of the Linux instance.


## Step 2: Prepare for installation

1.  Add an inbound rule to the security group of the ECS instance to allow traffic on the required ports. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    In this example, SSH port 22 and HTTP port 8080 are enabled.

2.  Connect to the Linux instance. For more information, see [Connect to a Linux instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using VNC.md).

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

5.  To ensure system security, we recommend that you create a standard user to run Tomcat.

    In this example, a standard user named www is created.

    ```
    useradd www
    ```

6.  Run the following command to create a root directory for the Java website:

    ```
    mkdir -p /data/wwwroot/default
    ```

7.  Upload the WAR package of Java web project files to the root directory and change the owner of files under the root directory to www.

    In this example, the following commands are run to create a Tomcat test page under the root directory and change the owner of files under the root directory to www.

    ```
    echo Tomcat test > /data/wwwroot/default/index.jsp
    ```

    ```
    chown -R www.www /data/wwwroot
    ```


## Step 3: Install JDK

1.  Run the following command to create a directory:

    ```
    mkdir /usr/java
    ```

2.  Run the following commands in sequence to grant the execute permissions on jdk-8u241-linux-x64.tar.gz and decompress it to /usr/java:

    ```
    chmod +x jdk-8u241-linux-x64.tar.gz
    ```

    ```
    tar xzf jdk-8u241-linux-x64.tar.gz -C /usr/java
    ```

3.  Set environment variables.

    1.  Run the `vi /etc/profile` command to open the /etc/profile file.

    2.  Press the `I` key to add the following content:

        ```
        # set java environment
        export JAVA_HOME=/usr/java/jdk1.8.0_241
        export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
        export PATH=$JAVA_HOME/bin:$PATH
        ```

    3.  Press the Esc key to exit the edit mode. Enter `:wq` and press the Enter key to save and close the configuration file.

4.  Run the following command to load the environment variables:

    ```
    source /etc/profile
    ```

5.  Run the following command to view the JDK version:

    ```
    java -version
    ```

    The following response indicates that JDK is installed.

    ![jdk180241](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5229919951/p97228.png)


## Step 4: Install Apache Tomcat

1.  Run the following commands in sequence:

    1.  Decompress apache-tomcat-8.5.53.tar.gz.

        ```
        tar xzf apache-tomcat-8.5.53.tar.gz
        ```

    2.  Rename the Tomcat directory.

        ```
        mv apache-tomcat-8.5.53 /usr/local/tomcat/
        ```

    3.  Configure the owner of the file.

        ```
        chown -R www.www /usr/local/tomcat/
        ```

    The /usr/local/tomcat/ directory contains the following subdirectories:

    -   bin: stores Tomcat script files, such as scripts used to enable and disable the Tomcat service.
    -   conf: stores various global configuration files of the Tomcat server, among which server.xml and web.xml are the most important files.
    -   webapps: serves as the main web publishing directory of Tomcat. It stores web application files by default.
    -   logs: stores Tomcat operation log files.
2.  Configure the server.xml file.

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
            <? xml version="1.0" encoding="UTF-8"? >
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

        3.  Press the Esc key to exit the edit mode. Enter `:wq` and press the Enter key to save and close the configuration file.
3.  Configure the Java Virtual Machine \(JVM\) memory parameters.

    1.  Run the `vi /usr/local/tomcat/bin/setenv.sh` command to create a file named /usr/local/tomcat/bin/setenv.sh.

    2.  Press the I key to add the following content:

        ```
        JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'                          
        ```

    3.  Press the Esc key to exit the edit mode. Enter `:wq` and press the Enter key to save and close the configuration file.

4.  Configure a script to enable Tomcat to run on system startup.

    1.  Run the following command to download the Tomcat startup script.

        **Note:** The script originates from the community and is for reference only. Alibaba Cloud does not make any guarantee, express or implied, with respect to the reliability of the script, as well as potential impacts of operations on the script. If you fail to download the script by running the wget command, you can use a browser to access `https://raw.githubusercontent.com/oneinstack/oneinstack/master/init.d/Tomcat-init` to obtain the script content.

        ```
        wget https://raw.githubusercontent.com/oneinstack/oneinstack/master/init.d/Tomcat-init
        ```

    2.  Run the following command to rename Tomcat-init:

        ```
        mv Tomcat-init /etc/init.d/tomcat
        ```

    3.  Run the following command to grant the execute permissions on the /etc/init.d/tomcat file:

        ```
        chmod +x /etc/init.d/tomcat
        ```

    4.  Run the following command to configure the JAVA\_HOME script to enable Tomcat to run on system startup:

        **Note:** The JDK version in the script must be the same as that you installed. Otherwise, Tomcat fails to start.

        ```
        sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_241@' /etc/init.d/tomcat                  
        ```

5.  Run the following commands to enable Tomcat to run on system startup:

    ```
    chkconfig --add tomcat
    chkconfig tomcat on
    ```

6.  Run the following command to start Tomcat:

    ```
    service tomcat start             
    ```

7.  Open your browser and enter a URL in the `http://<Public IP address of the ECS instance>:8080` format in the address bar to connect to the ECS instance.

    The following response indicates that Tomcat is installed.

    ![Response](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9229919951/p12137.png)


When Tomcat becomes available, we recommend that you configure websites on the instance and map domain names to the public IP address of the instance.

