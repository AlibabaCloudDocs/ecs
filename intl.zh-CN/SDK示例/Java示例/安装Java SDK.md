# 安装Java SDK

本文介绍了如何安装ECS Java SDK以及阿里云核心库。

安装ECS Java SDK必须使用JDK 1.6或更高版本。

阿里云开发者中心为您提供了ECS Java SDK以及阿里云核心库的Maven项目依赖及JAR包，您可以编写代码调用阿里云SDK来实现对阿里云的产品和服务的访问。

本文示例中，客户端为Windows10 64位操作系统，使用的Java开发工具为IntelliJ IDEA。

1.  通过以下任一方式在IDEA中配置Maven项目管理工具。

    -   使用IDEA中集成的Maven项目管理工具。
    -   访问Maven官方下载页面（[Download Apache Maven](http://maven.apache.org/download.cgi)）下载对应操作系统的Maven工具，手动配置Maven工具。
2.  访问[阿里云开发工具包（SDK）](https://developer.aliyun.com/tools/sdk?#/java)，获取阿里云的**SDK核心库**以及**云服务器**的Maven项目依赖。

3.  通过以下任一方式创建Maven项目。

    -   方式一：在IDEA中添加一个Maven项目。

        ![maven1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9037428951/p101344.png)

    -   方式二：将已有的项目转换为Maven项目。
        1.  右键单击要转换的项目，并选择**Add Framework Support...**。

            ![maven2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0137428951/p101351.png)

        2.  选择**Maven**，并单击**OK**。

            ![maven3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0137428951/p101353.png)

4.  在项目目录下的pom.xml文件中，添加阿里云核心库aliyun-java-sdk-core、云服务器aliyun-java-sdk-ecs及fastjson依赖。

    添加依赖后，Maven项目管理工具会自动下载相关jar包。

    **说明：** SDK包更新频繁，建议您通过上文提供的阿里云开发工具包官网链接获取最新版本依赖。

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

5.  查看项目目录下的External Libraries。

    如图所示，表示已成功导入依赖。

    ![pom.xml](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0137428951/p137047.png)


