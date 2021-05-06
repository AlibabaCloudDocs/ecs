# 使用Packer创建自定义镜像

Packer是一款轻量级的镜像定义工具，能够运行在常用的主流操作系统（如Windows、Linux和macOS）上。参见本文安装并使用Packer，轻松创建自定义镜像。

本文描述以Linux系统的服务器为例，Windows系统的操作请参见[Packer官方文档](https://www.packer.io/intro/getting-started/install.html)。

## 步骤一：安装Packer

1.  连接并登录到Linux服务器。

    登录ECS Linux实例服务器，请参见[使用用户名密码验证连接Linux实例](/cn.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/使用用户名密码验证连接Linux实例.md)。

2.  执行命令`cd /usr/local/bin`进入/usr/local/bin目录。

    **说明：** /usr/local/bin目录为环境变量目录，您可以将Packer安装到该目录下或其他已添加到环境变量的目录下。

3.  执行命令`wget https://releases.hashicorp.com/packer/1.1.1/packer_1.1.1_linux_amd64.zip`获取Packer安装包。

    访问[Packer下载页面](https://www.packer.io/downloads.html)，获取其他版本Packer安装包。

4.  执行命令`unzip packer_1.1.1_linux_amd64.zip`解压文件。

5.  执行命令`packer -v`验证Packer安装状态。

    -   若Linux服务器返回Packer版本号，表示您已正确安装Packer。
    -   若Linux服务器提示`command not found`表示Packer未正确安装。

## 步骤二：定义Packer模板

使用Packer创建自定义镜像时，需要创建一个JSON格式的模板文件。在该模板文件中，您需要指定创建自定义镜像的生成器和配置器。详情请参见[Alicloud Image Builder（生成器）](https://www.packer.io/docs/builders/alicloud-ecs.html)和[Provisioners（配置器）](https://www.packer.io/docs/provisioners)。Packer具有多种配置器，可用于配置自定义镜像的内容生成方式，以下以常用的Shell配置器为例，定义Packer模板。

在Linux服务器中创建名为alicloud的json文件并粘贴以下内容。

```
{
     "variables": {
       "access_key": "{{env `ALICLOUD_ACCESS_KEY`}}",
       "secret_key": "{{env `ALICLOUD_SECRET_KEY`}}"
     },
     "builders": [{
       "type":"alicloud-ecs",
       "access_key":"{{user `access_key`}}",
       "secret_key":"{{user `secret_key`}}",
       "region":"cn-beijing",
       "image_name":"packer_basic",
       "source_image":"centos_7_02_64_20G_alibase_20170818.vhd",
       "ssh_username":"root",
       "instance_type":"ecs.n1.tiny",
       "internet_charge_type":"PayByTraffic",
       "io_optimized":"true"
     }],
     "provisioners": [{
       "type": "shell",
       "inline": [
         "sleep 30",
         "yum install redis.x86_64 -y"
       ]
     }]
   }
```

您需要自定义的参数值如下表所示。

|参数|描述|
|:-|:-|
|access\_key|您的AccessKeyID。更多详情，请参见[创建AccessKey]()。 **说明：** 由于AccessKey权限过大，为防止错误操作，建议您创建RAM用户，并使用RAM子账号创建AccessKey。具体步骤，请参见[创建RAM用户](/cn.zh-CN/用户管理/创建RAM用户.md)和[创建AccessKey]()。 |
|secret\_key|您的AccessKeySecret。更多详情，请参见[创建AccessKey]()。|
|region|创建自定义镜像时使用临时资源的地域。|
|image\_name|自定义镜像的名称。|
|source\_image|基础镜像的名称，可以从阿里云公共镜像列表获得。|
|instance\_type|创建自定义镜像时生成的临时实例的类型。|
|internet\_charge\_type|创建自定义镜像时临时实例的公网带宽付费类型。|
|provisioners|创建自定义镜像时使用的Packer配置器类型。详情请参见[Packer配置器](https://www.packer.io/docs/provisioners)。|

## 步骤三：使用Packer创建自定义镜像

指定Packer模板文件生成自定义镜像的操作步骤如下：

1.  运行命令`export ALICLOUD_ACCESS_KEY=<您的AccessKeyID>`导入您的AccessKeyID。

2.  运行命令`export ALICLOUD_SECRET_KEY=<您的AccessKeySecret>`导入您的AccessKeySecret。

3.  运行命令`packer build alicloud.json`创建自定义镜像。


示例运行结果如下，以下示例将创建含Redis的自定义镜像。

```
alicloud-ecs output will be in this color.
==> alicloud-ecs: Prevalidating alicloud image name...
alicloud-ecs: Found image ID: centos_7_02_64_20G_alibase_20170818.vhd
==> alicloud-ecs: Start creating temporary keypair: packer_59e44f40-c8d6-0ee3-7fd8-b1ba08ea94b8
==> alicloud-ecs: Start creating alicloud vpc
---------------------------
==> alicloud-ecs: Provisioning with shell script: /var/folders/3q/w38xx_js6cl6k5mwkrqsnw7w0000gn/T/packer-shell257466182
alicloud-ecs: Loaded plugins: fastestmirror
---------------------------
alicloud-ecs: Total                                              1.3 MB/s | 650 kB 00:00
alicloud-ecs: Running transaction check
---------------------------
==> alicloud-ecs: Deleting temporary keypair...
Build 'alicloud-ecs' finished.
==> Builds finished. The artifacts of successful builds are:
--> alicloud-ecs: Alicloud images were created:
cn-beijing: m-2ze12578be1oa4ovs6r9
```

[使用自定义镜像创建实例](/cn.zh-CN/实例/创建实例/使用自定义镜像创建实例.md)

**相关文档**  


[packer-provider](https://github.com/alibaba/packer-provider)

[Packer官方文档](https://www.packer.io/docs)

