# 使用faascmd

您可以通过本教程了解faascmd命令的用法。

使用faascmd工具之前，您需要先配置faascmd。具体操作，请参见[配置faascmd](/intl.zh-CN/最佳实践/FaaS实例最佳实践/faascmd工具/配置faascmd.md)。

使用授权命令前，您需要完成以下操作：

1.  已为FaaS新建一个OSS bucket，用于上传原始编译的DCP文件。
2.  已在该FaaS OSS bucket中，新建一个名为compiling\_logs的文件夹。

faascmd语法说明如下：

-   faascmd工具提供的所有命令和参数都严格区分大小写。
-   faascmd命令中，参数、`=`、取值间不能有多余空格。

本文介绍的faascmd命令如下：

-   [授权](#section_l22_m3t_2lm)
-   [查看授权策略](#section_zns_gx0_rw5)
-   [删除授权策略](#section_4ql_7ju_xc6)
-   [查看OSS Bucket下所有的objects](#section_pai_qvg_9a3)
-   [上传原始编译文件](#section_bd6_8gn_vz1)
-   [下载OSS Bucket中的object](#section_518_vs9_hic)
-   [新建FPGA镜像](#section_4mb_909_zbm)
-   [查看FPGA镜像](#section_o0h_qkz_zzx)
-   [删除FPGA镜像](#section_k1c_yj3_wls)
-   [下载FPGA镜像](#section_0xf_a3k_662)
-   [查看FPGA镜像下载状态](#section_a6q_bsy_kau)
-   [发布FPGA镜像](#section_wct_1ue_ya8)
-   [查看FPGA实例的信息](#section_5za_vje_45r)

## 授权

`faascmd auth`命令用于授权faas admin访问您的OSS bucket。

命令格式：

```
faascmd auth --bucket=<YourFaasOSSBucketName>
```

示例代码：

![授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4875688951/p31129.png)

**说明：** 如果同一主账号下有多个RAM用户，建议RAM用户间共享一个OSS bucket，以避免重复修改或覆盖授权策略。

## 查看授权策略

`faascmd list_policy`命令用来查看指定的OSS bucket是否已添加到相应的授权策略（faasPolicy）里。

命令格式：

```
faascmd list_policy
```

示例代码：

![查看授权策略](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5875688951/p31130.png)

**说明：** 请关注您的OSS Bucket和OSS Bucket/compiling\_logs是否出现在列出的策略信息中。

## 删除授权策略

`faascmd delete_policy`命令用于删除授权策略（faasPolicy）。

命令格式：

```
faascmd delete_policy
```

示例代码：

![删除授权策略](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5875688951/p31131.png)

**说明：** 如果同一主账号下有多个RAM用户，建议您通过[RAM控制台](https://ram.console.aliyun.com/)操作，以避免误删授权策略。

## 查看OSS Bucket下所有的objects

`faascmd list_objects`命令用于查看OSS Bucket下所有的objects。

命令格式：

```
faascmd list_objects
```

示例代码：

![查看objects](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5875688951/p31132.png)

**说明：** 您可以配合grep命令筛选出您想要的文件。例如：`faascmd list_objects | grep "xxx"` 。

## 上传原始编译文件

`faascmd upload_object`命令用于将本地编译的原始文件上传到指定的OSS bucket中。

命令格式：

```
faascmd upload_object --object=<NewFileNameInOSSBucket> --file=<YourFilePath>/<FileNameYouWantToUpload>           
```

示例代码：

![upload_object](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5875688951/p31112.png)

**说明：**

-   如果需上传的文件在当前目录下，则无需提供路径。
-   Intel FPGA的本地编译原始文件为.gbs格式；Xilinx FPGA的本地编译原始文件为脚本处理后得到的tar包。

## 下载OSS Bucket中的object

`faascmd get_object`命令用来下载OSS Bucket中指定的object。

命令格式：

```
faascmd get_object --object=<YourObjectName> --file=<YourLocalPath>/<YourFileName>
```

示例代码：

![get_object](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5875688951/p31115.png)

**说明：** 如果您不提供路径，则默认下载到当前文件夹。

## 新建FPGA镜像

`faascmd create_image`命令用来提交制作FPGA镜像的请求。请求成功时，返回FpgaImageUUID。

命令格式：

```
faascmd create_image --object=<YourObjectName> 
--fpgatype=<intel/xilinx>  --encrypted=<true/false> 
--kmskey=<key/如果encrypted为true，必选；否则可选> 
--shell=<Shell Version/必选> --name=<name/可选> 
--description=<description/可选> --tags=<tags/可选>
```

示例代码：

![create_image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5875688951/p31117.png)

## 查看FPGA镜像

`faascmd list_images`命令用于查看用户制作的所有FPGA镜像的信息。

命令格式：

```
faascmd list_images
```

示例代码：

![list_images](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5875688951/p31118.png)

**说明：** 每个RAM用户最多允许保留10个FPGA镜像。

## 删除FPGA镜像

`faascmd delete_image`命令用于删除FPGA镜像。

命令格式：

```
faascmd delete_image --imageuuid=<yourImageuuid>
```

示例代码：

![delete_image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5875688951/p31120.png)

## 下载FPGA镜像

`faascmd download_image`命令用于提交下载FPGA镜像的请求。

命令格式：

```
faascmd download_image  --instanceId=<YourInstanceId> 
--fpgauuid=<Yourfpgauuid> --fpgatype=<intel/xilinx> 
--imageuuid=<YourImageuuid> --imagetype=<afu> 
--shell=<YourImageShellVersion>
```

示例代码：

```
faascmd download_image --instanceId=XXXXX --fpgauuid=XXXX --fpgatype=intel --imageuuid=XXXX
```

## 查看FPGA镜像下载状态

`faascmd fpga_status`命令用于查看当前FPGA板卡状态或FPGA镜像的下载进度。

命令格式：

```
faascmd fpga_status --fpgauuid=<Yourfpgauuid> --instanceId=<YourInstanceId>
```

示例代码：

![fpga_status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5875688951/p31126.png)

## 发布FPGA镜像

`faascmd publish_image`命令用来提交发布FPGA镜像的请求。

命令格式：

```
faascmd publish_image --imageuuid=<YourImageuuid> --imageid=<YourInstanceImageid>
```

**说明：**

-   imageuuid是您要发布到云市场的FPGA镜像id。您可以通过`faascmd list_images`命令查看。
-   imageid是FPGA实例的镜像id。您可以通过[ECS管理控制台](https://ecs.console.aliyun.com)的实例详情页查看。

## 查看FPGA实例的信息

`faascmd list_instances`命令用于获取FPGA实例的基本信息，包括实例ID、FPGA板卡信息和Shell版本。

命令格式：

```
faascmd list_instances --instanceId=<YourInstanceId>
```

示例代码：

![list_instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5875688951/p31128.png)

