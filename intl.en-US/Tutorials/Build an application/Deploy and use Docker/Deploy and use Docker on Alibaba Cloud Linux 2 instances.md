---
keyword: [Docker, container, Linux, ECS, cloud server, Alibaba Cloud, Alibaba Cloud Linux 2]
---

# Deploy and use Docker on Alibaba Cloud Linux 2 instances

This topic describes how to deploy and use Docker on an Elastic Compute Service \(ECS\) instance that runs an Alibaba Cloud Linux 2.1903 LTS 64-bit operating system. This topic is intended for developers who are familiar with Linux but new to Alibaba Cloud elastic ECS.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   At least one ECS instance is created. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

    The following instance configurations are used in the examples:

    -   Instance type: ecs.g6.large
    -   Operating system: Alibaba Cloud Linux 2.1903 LTS 64-bit

        **Note:** The operation commands described in this example can also be used in the CentOS 7 operating system.

    -   Network type: Virtual Private Cloud \(VPC\)
    -   IP address: a public IP address

This topic describes the following operations:

-   Deploy Docker. For more information, see the [Deploy Docker](#section_gtl_cjs_ls2) section.
-   Use Docker.
    -   For information about the basic usage of Docker, see the [Use Docker](#section_x1c_w5u_5wb) section.
    -   For information about how to create a Docker image, see the [Create a Docker image](#section_i4r_m92_6ev) section.

## Deploy Docker

This section describes how to manually install Docker. You can also purchase a Docker image from [Alibaba Cloud Marketplace](https://market.aliyun.com/software) to deploy Docker on an ECS instance.

1.  Remotely connect to an ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Perform the following operations in sequence to add the YUM repository:

    -   Update the YUM repository.

        ```
        yum -y update
        ```

    -   Install the EPEL repository.

        ```
        yum install -y epel-release 
        ```

    -   Remove the YUM cache.

        ```
        yum clean all
        ```

    **Note:** You can run the yum list command to view all available packages.

3.  Install and run Docker.

    ```
    yum install docker-io -y
    systemctl start docker
    ```

4.  Check the Docker version information and verify whether Docker is installed.

    ```
    docker --version
    ```

    A command output similar to the following one indicates that Docker is installed.

    ![site](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7750579161/p128549.png)


## Use Docker

You can use Docker in the following ways:

-   Manage the Docker daemon.

    ```
    systemctl start docker     #Run the Docker daemon.
    systemctl stop docker      #Stop the Docker daemon.
    systemctl restart docker   #Restart the Docker daemon.
    systemctl enable docker    #Configure Docker to run on system startup.
    ```

-   Manage images. Apache images from Alibaba Cloud Container Registry are used in the following examples.

    ```
    docker pull registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5
    ```

    -   Modify the tags of images from Alibaba Cloud Container Registry to make the images easy to identify.

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
    -   Enter a container. Run the `docker images` command to obtain the ImageId value, which is e1abc\*\*\*\*. Then, run the `docker run` command to access the container.

        ```
        docker run -it e1abc**** /bin/bash
        ```

    -   Exit the container. Run the `exit` command to exit the container.
    -   You can combine the `run` command with the `–d` parameter to run the container in the background. The `--name` parameter specifies apache as the container name.

        ```
        docker run -d --name apache e1abc****
        ```

    -   Access the container that runs in the background.

        ```
        docker exec -it apache /bin/bash
        ```

    -   Query the container ID.

        ```
        docker ps
        ```

    -   Create an image from the container. Description of the parameters in the command: `docker commit <Container ID or container name> [<Repository name> [: <Tag>]]`.

        ```
        docker commit containerID/containerName repository:tag
        ```

    -   To easily test and restore an image, you can run the source image, derive a new image that has a simple name from the source image, and then test the new image.

        ```
        docker commit 4c8066cd8**** apachephp:v1
        ```

    -   Run the container and map port 8080 of the host to the container.

        ```
        docker run -d -p 8080:80 apachephp:v1
        ```

        In a browser, enter the IP address of the instance followed by the port number 8080 to connect to the container. The following response indicates that the container runs normally.

        **Note:** An inbound rule must be added to a security group of the ECS instance to allow inbound traffic on port 8080. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

        ![Mapping result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9629919951/p12348.png)


## Create a Docker image

1.  Prepare Dockerfile.

    1.  Create and edit Dockerfile.

        ```
        vim Dockerfile
        ```

    2.  Press the I key to enter the edit mode. Add the following content to the file:

        ```
        #Declare a base image.
        FROM apachephp:v1
        #Declare the owner of the base image.
        MAINTAINER DTSTACK
        #The commands that you want to run before the container starts. You must append these commands to the end of the RUN command. Dockerfile can contain only a maximum of 127 lines. If you have commands that exceed 127 lines, we recommend that you write these commands to a script.
        RUN mkdir /dtstact
        #The commands that are run on system startup. The last command must be a frontend command that runs constantly. Otherwise, the container exits after all commands are run. 
        ENTRYPOINT ping www.aliyun.com
        ```

    3.  Press the Esc key. Enter `:wq` and press the Enter key to save and exit Dockerfile.

2.  Build an image.

    ```
    docker build -t webalibabacloudlinux:v1 .    # . specifies the path of Dockerfile and must be provided.
    docker images                                #Check whether the image is built.
    ```

3.  Run the container and check its status.

    ```
    docker run -d webalibabacloudlinux:v1    #Run the container in the background.
    docker ps                                #Query the containers that are in the running state.
    docker ps -a                             #Query all containers, including those in the stopped state.
    docker logs CONTAINER ID/IMAGE           #Check the startup log to troubleshoot the issue based on the container ID or name if the container does not appear in the query results.
    ```

4.  Create an image.

    ```
    docker commit fb2844b6**** dtstackweb:v1     #Append the container ID and the name and version number of the new image to the end of the commit parameter. 
    docker images                                #Query images that are downloaded and created on premises.
    ```

5.  Push the image to a remote repository.

    By default, the image is pushed to Docker Hub. You must log on to Docker, bind a tag to the image, and then name the image in the `<Docker username>/<image name>:<tag>` format. Then the push is complete.

    ```
    docker login --username=dtstack_plus registry.cn-shanghai.aliyuncs.com #Enter the password of the image registry after you run this command.
    docker tag [ImageId] registry.cn-shanghai.aliyuncs.com/dtstack123/test:[Tag]
    docker push registry.cn-shanghai.aliyuncs.com/dtstack123/test:[Tag]
    ```


