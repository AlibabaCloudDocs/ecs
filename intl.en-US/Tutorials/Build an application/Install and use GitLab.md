# Install and use GitLab

GitLab is a self-managed Git project warehouse developed by Ruby and provides access to public or private projects through a web interface. This topic describes how to install and use GitLab on an ECS instance.

An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).

An ECS instance is created and meets the following requirements:

-   The instance has at least two vCPUs and 4 GiB of memory. In the examples in this topic, the instance uses the following configurations:
    -   Instance type: ecs.c6.large
    -   Operating system: CentOS 7.2 64-bit
-   The security group rule described in the following table is added to the security group of the instance. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    |Direction|Protocol|Port range|Authorization object|
    |---------|--------|----------|--------------------|
    |Inbound|HTTP\(80\)|80|0.0.0.0/0|


## Manually install GitLab

1.  Install the dependency package.

    ```
    sudo yum install -y curl policycoreutils-python openssh-server
    ```

    **Note:** In the examples in this topic, the CentOS 7.2 64-bit operating system is used. If you use an ECS instance that runs CentOS 8, you cannot find the `policycoreutils-python` dependency package when you run the preceding command on the instance. This is because the dependency package is not included in the software source of CentOS 8. The absence of this dependency package does not affect the deployment of GitLab. You can ignore this issue and continue to run subsequent commands.

2.  Set SSH to run at startup and start SSH.

    ```
    sudo systemctl enable sshd
    sudo systemctl start sshd
    ```

3.  Install Postfix to send notification emails.

    ```
    sudo yum install postfix
    ```

4.  Set Postfix to run at startup.

    ```
    sudo systemctl enable postfix
    ```

5.  Start Postfix.

    1.  Run the `vim /etc/postfix/main.cf` command to open the main.cf file and find the code line shown in the following figure.

        ![set_inet](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8529919951/p38837.png)

    2.  Press the I key to enter the edit mode.

    3.  Change the code line to `inet_interfaces = all`.

    4.  Press the Esc key to exit the edit mode. Enter :wq and press the Enter key to save and close the file.

    5.  Run the `sudo systemctl start postfix` command to start Postfix.

6.  Add the GitLab software package repository.

    ```
     curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
    ```

7.  Install GitLab.

    ```
    sudo EXTERNAL_URL="<Public IP address of the ECS instance>" yum install -y gitlab-ce
    ```

    **Note:** You can obtain the public IP address of the ECS instance from the Instances page in the ECS console.

8.  Use a browser to access the public IP address of the ECS instance.

    The following page indicates that GitLab is installed. You must reset the GitLab root password.

    ![gitlab1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8529919951/p92789.png)


## Use GitLab

1.  Log on to GitLab.

    In the address bar of your browser, enter the public IP address of the ECS instance where GitLab is installed and press the Enter key. The GitLab logon page is displayed. Use the `root` username and the new password that you set at your first logon to log on.

    ![gl2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p92794.png)

    The following page indicates that you are logged on.

    ![gl3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p92797.png)

2.  Create a project.

    1.  Use the software repository provided by Linux to install Git.

        ```
        yum install git
        ```

        ![install_git](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p12262.png)

    2.  Generate a key file.

        Run the following command to generate the .ssh/id\_rsa key file:

        ```
        ssh-keygen
        ```

        ![Keys](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p12263.png)

        Run the following command to view the content of the id\_rsa.pub public key file. In the next step, you must paste the content into the SSH key configuration file on the ECS instance where GitLab is installed.

        ```
        cat .ssh/id_rsa.pub
        ```

        ![Public key](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p12264.png)

    3.  On the GitLab homepage, create a project.

        ![new_project](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p12265.png)

        ![new_project_2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p12274.png)

    4.  Add an SSH key and import the content of the key file generated in Substep b.

        ![import-sshkey-1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p12266.png)

        ![import-sshkey-2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p12275.png)

        The following page indicates that the SSH key is added.

        ![import-ssh-key-complete](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p12267.png)

    5.  Record the address of the new project for later use.

        ![Project address](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p12268.png)

3.  Configure GitLab.

    1.  Add the name of the user who will use GitLab.

        ```
        git config --global user.name "testname" 
        ```

    2.  Add the email address of the user who will use GitLab.

        ```
        git config --global user.email "abc@example.com" 
        ```

    3.  Clone the project you created in the previous step to create a local directory that has the same name as the project. All the project files are available in the directory.

        ```
        git clone git@iZxxxxxxxxxxxxxxxxx3Z:root/test.git
        ```

        ![Configure GitLab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9529919951/p12269.png)

4.  Upload a file.

    1.  Access the local project directory you created in the previous step.

        ```
        cd test/ 
        ```

    2.  Create a file as the target file to upload to GitLab.

        ```
        echo "test" > /root/test.sh
        ```

    3.  Copy the target file or directory to the local project directory.

        ```
        cp /root/test.sh . / 
        ```

        ![Upload the file](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0629919951/p12270.png)

    4.  Add the test.sh file to the index.

        ```
        git add test.sh
        ```

    5.  Commit the test.sh file to the local GitLab repository.

        ```
        git commit -m "test.sh"
        ```

    6.  Synchronize the file to the ECS instance.

        ```
        git push -u origin master
        ```

        ![Command used to synchronize the file](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0629919951/p12271.png)

        The test.sh file is synchronized to GitLab and displayed on the Project page.

        ![File synchronization results](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0629919951/p12272.png)


