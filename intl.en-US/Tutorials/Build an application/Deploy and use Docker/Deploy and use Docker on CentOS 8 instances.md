---
keyword: [Docker, container, Linux, ECS, cloud server, Alibaba Cloud, CentOS 8]
---

# Deploy and use Docker on CentOS 8 instances

This topic describes how to deploy and use Docker on an ECS instance that runs a CentOS 8.1 64-bit operating system. This tutorial is intended for developers who are familiar with Linux but new to Alibaba Cloud ECS.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   At least one instance is created. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

    The following instance configurations are used in the examples:

    -   Instance type: ecs.g6.large
    -   Operating system: CentOS 8.1 64-bit
    -   Network type: VPC
    -   IP address: a public IP address

This topic describes the following operations:

-   Deploy Docker. For more information, see the [Deploy Docker](#section_kjt_i59_n4a) section.
-   Use Docker.
    -   For information about the basic usage of Docker, see the [Use Docker](#section_kig_gpy_uti) section.
    -   For information about how to create a Docker image, see the [Create a Docker image](#section_o3m_mmi_0bz) section.

## Deploy Docker

You can purchase the required image from [Alibaba Cloud Marketplace](https://market.aliyun.com/software) and easily deploy Docker. You can also manually install Docker as described in this topic.

1.  Remotely connect to an ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to install the dependency package of the Docker store driver:

    ```
    dnf install -y device-mapper-persistent-data lvm2
    ```

3.  Run the following command to add a stable Docker installation package:

    ```
    dnf config-manager --add-repo=https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
    ```

4.  Run the following command to view the added Docker installation package:

    ```
    dnf list docker-ce
    ```

    Sample success response:

    ```
    docker-ce.x86_64        3:19.03.13-3.el7        docker-ce-stable
    ```

5.  Run the following command to install Docker:

    ```
    dnf install -y docker-ce --nobest
    ```

6.  Run the following command to start Docker:

    ```
    systemctl start docker
    ```


## Use Docker

You can use Docker in these ways:

-   Manage the Docker daemon.

    ```
    systemctl start docker     #Run the Docker daemon.
    systemctl stop docker      #Stop the Docker daemon.
    systemctl restart docker   #Restart the Docker daemon.
    ```

-   Manage images. In the following example, Apache images from Alibaba Cloud Container Registry are used.

    ```
    docker pull registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5
    ```

    -   Modify the tags of images in Alibaba Cloud Container Registry to simplify image identification.

        ```
        docker tag registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5:latest aliweb:v1
        ```

    -   Check existing images.

        ```
        docker images
        ```

    -   Force delete an image.

        ```
        docker rmi -f registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5
        ```

-   Manage containers.
    -   Access a container. Run the `docker images` command to obtain the ImageId value, which is e1xxxxxxxxxe. Then, run the `docker run` command to access the container.

        ```
        docker run -it e1xxxxxxxxxe /bin/bash
        ```

    -   Exit the container. Run the `exit` command to exit the container.
    -   You can combine the `run` command with the `–d` parameter to run the container in the background. The `--name` parameter specifies apache as the container name.

        ```
        docker run -d --name apache e1xxxxxxxxxe
        ```

        exit

    -   Access the container that runs in the background.

        ```
        docker exec -it apache /bin/bash
        ```

    -   Create an image from the container. Description of parameters in the command: `docker commit <Container ID or container name> [<Repository name>[:<Tag>]]`.

        ```
        docker commit containerID/containerName repository:tag
        ```

    -   To easily test and restore an image, you can run the source image, derive a new image with a simple name from the source image, and then test the new image.

        ```
        docker commit 4c8066cd8**** apachephp:v1
        ```

    -   Run the container and map port 8080 of the host to the container.

        ```
        docker run -d -p 8080:80 apachephp:v1
        ```

        In a browser, enter the IP address of the instance followed by the port number 8080 to connect to the container. The following response indicates that the container runs normally.

        ![Mapping result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9629919951/p12348.png)


## Create a Docker image

1.  Prepare the following content in Dockerfile:

    1.  Create and edit the Dockerfile file.

        ```
        vim Dockerfile
        ```

    2.  Press the I key to enter the edit mode. Add the following content to the file:

        ```
        FROM apachephp:v1  #Declare the source of the base image.
        MAINTAINER DTSTACK #Declare the image owner.
        RUN mkdir /dtstact #The commands that you want to run before the container starts. You must append these commands to the end of the RUN command. Dockerfile can contain only a maximum of 127 lines. If you have commands that exceed 127 lines, we recommend that you write these commands to a script.
        ENTRYPOINT ping www.aliyun.com #The commands that run at system startup. The last command must be a frontend command that runs constantly. Otherwise, the container will exit after running all commands.
        ```

    3.  Press the Esc key. Enter `:wq` and press the Enter key to save and exit the Dockerfile file.

2.  Build an image.

    ```
    docker build -t webcentos8:v1 .    # . specifies the path of Dockerfile and must be provided.
    docker images                                #Check whether the image is built.
    ```

3.  Run the container and check its status.

    ```
    docker run -d webcentos8:v1           #Run the container in the background.
    docker ps                             #Query the containers that are in the running state.
    docker ps -a                          #Query all containers, including those in the stopped state.
    docker logs CONTAINER ID/IMAGE        #Check the startup log to troubleshoot the issue based on the container ID or name if the container does not appear in the query results.
    ```

4.  Create an image.

    ```
    docker commit fb2844b6**** dtstackweb:v1 #Append the container ID and the name and version number of the new image to the end of the commit command.
    docker images                    #Query images that have been downloaded and created on premises.
    ```

5.  Push the image to a remote repo.

    By default, the image is pushed to Docker Hub. You must log on to Docker, bind a tag to the image, and then name the image in the `Docker username/image name:tag` format. Then the push is completed.

    ```
    docker login --username=dtstack_plus registry.cn-shanghai.aliyuncs.com #Specify the password of the image repository. Enter the password after you run this command.
    docker tag [ImageId] registry.cn-shanghai.aliyuncs.com/dtstack123/test:[Tag]
    docker push registry.cn-shanghai.aliyuncs.com/dtstack123/test:[Tag]
    ```


