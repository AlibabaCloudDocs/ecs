# Install ECS SDK for Java

This topic describes how to install Elastic Compute Service \(ECS\) SDK for Java and the Alibaba Cloud SDK core library.

JDK 1.6 or later is installed.

The Alibaba Cloud Developer Center provides ECS SDK for Java, and Maven project dependencies and JAR packages of the Alibaba Cloud SDK core library. You can write code to call Alibaba Cloud SDKs to access Alibaba Cloud products and services.

In this example, the Windows 10 64-bit operating system and the IntelliJ IDEA Java development tool are used.

1.  Use one of the following methods to configure the Maven project management tool in IDEA:

    -   Use the integrated Maven project management tool in IDEA.
    -   Download the Maven software corresponding to the operating system from the official Maven website \([Download Apache Maven](http://maven.apache.org/download.cgi)\) and manually configure the Maven tool.
2.  Go to [Alibaba Cloud SDKs](https://developer.aliyun.com/tools/sdk?#/java) to obtain the **Alibaba Cloud SDK core library** and Maven dependencies of **ECS**.

3.  Create a Maven project by using one of the following methods:

    -   Method 1: Create a Maven project in IDEA.

        ![maven1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7942674161/p101344.png)

    -   Method 2: Convert an existing project into a Maven project.
        1.  Right-click the project to be converted and select **Add Framework Support...**.

            ![maven2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8942674161/p101351.png)

        2.  Select **Maven** and click **OK**.

            ![maven3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8942674161/p101353.png)

4.  Add the aliyun-java-sdk-core, aliyun-java-sdk-ecs, and fastjson dependencies to the pom.xml file in the project directory.

    After the dependencies are added, the Maven project management tool automatically downloads the corresponding JAR packages.

    **Note:** SDK packages are frequently updated. We recommend that you obtain the latest version of dependencies from the official Alibaba Cloud SDKs website.

    ```
    <dependencies>
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-core</artifactId>
            <version>4.5.6</version>
        </dependency>
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-ecs</artifactId>
            <version>4.19.9</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.73</version>
        </dependency>
    </dependencies>
    ```

5.  Check External Libraries in the project directory.

    If a command output similar to the one shown in the following figure is generated, the dependencies are imported.

    ![pom.xml](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8157745261/p137047.png)


