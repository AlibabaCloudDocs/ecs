# 访问控制RAM介绍

访问控制RAM用于为人员、云服务等指定身份并基于身份授予资源访问权限，从而控制对阿里云资源的访问。

## 身份管理

访问控制RAM中的身份包括实体身份（RAM用户、RAM用户组）和虚拟身份（RAM角色）。

-   RAM用户有确定的登录密码和访问密钥，RAM用户组则用于分类职责相同的RAM用户，RAM用户和RAM用户组均可以被赋予一组权限策略。RAM用户可以对应企业内的人员、应用等，在需要协同使用资源的场景中，避免直接共享阿里云账号的密码等机密信息，缩小机密信息的可见范围，并为RAM用户和RAM用户组赋予最小权限，即使不慎泄露机密信息，也不会危及阿里云账号下的所有资源。
-   RAM角色有确定的身份，可以被赋予一组权限策略，但是没有确定的登录密码或访问密钥。RAM角色需要由一个受信的实体扮演，该实体在扮演RAM角色时即获得RAM角色的权限。在云产品通信的场景中，为受信的实体（例如ECS实例）绑定RAM角色后，该实体可以基于STS（Security Token Service）临时凭证访问其他云产品的API，避免将AccessKey写在配置文件中等高危操作，保证AccessKey的安全。

## 权限管理

访问控制RAM通过权限策略描述授权的具体内容，权限策略包括固定的基本元素，更多信息，请参见[权限策略基本元素](/intl.zh-CN/权限策略管理/权限策略语言/权限策略基本元素.md)。为RAM用户、RAM用户组、RAM角色添加一组权限策略后，即可让其有权限访问指定资源。

权限策略分为系统策略和自定义策略。

-   系统策略：阿里云预定义的常用权限策略，您只能使用不能修改。部分云服务器ECS相关的系统策略如下：

    -   AliyunECSFullAccess：云服务器ECS的管理权限，包括创建、查看、删除相关资源等操作。
    -   AliyunECSReadOnlyAccess：云服务器ECS的只读权限，只可查看相关资源。
    -   AliyunECSNetworkInterfaceManagementAccess：弹性网卡的管理权限，包括创建、查看、删除弹性网卡等操作。
    -   AliyunECSAssistantFullAccess：云助手命令的管理权限，包括创建、执行、查看、删除云助手命令等操作。
    -   AliyunECSAssistantReadonlyAccess：云助手命令的只读权限，只可查看云助手命令相关信息。
    -   AliyunECSImageExportRolePolicy：导出ECS实例镜像所需的权限，包括读OSS Bukcet、读写OSS Object等操作。
    -   AliyunECSImageImportRolePolicy：导入镜像所需的权限，包括读OSS Bukcet、读OSS Object操作。
    -   AliyunECSInstanceForYundunSysTrustRolePolicy：安全增强型实例使用阿里云可信服务所需的权限。
    -   AliyunECSDiskEncryptRolePolicy：加密云盘所需的权限。
    更多系统策略的详情信息，请参见[系统策略示例]()。

-   自定义策略：您按需自行创建和维护的权限策略，关于自定义策略的操作和示例，请参见[创建自定义策略](/intl.zh-CN/权限策略管理/自定义策略/创建自定义策略.md)和[权限策略示例库概览](/intl.zh-CN/权限策略管理/权限策略示例库/权限策略示例库概览.md)。

## 应用示例

在企业内部控制员工的资源使用权限：

1.  为需要创建和管理资源的职位创建SysAdmins用户组，并添加权限策略，授予执行所有操作的权限。
2.  为需要使用资源的职位创建Developers用户组，并添加权限策略，授予调用StartInstance、StopInstance、DescribeInstances接口的权限。
3.  为员工创建RAM用户，并按照各自职位加入用户组。
4.  为加强网络安全控制，添加权限策略，规定如果组内用户的IP地址不是来自企业网络，则拒绝其访问资源。
5.  如果某开发人员的职位变更为系统管理员，将其RAM用户从Developers用户组移动到SysAdmins用户组 。
6.  如果Developers用户组的RAM用户需要更大权限，修改用户组的权限策略即可应用到用户组中的所有RAM用户。

为ECS实例绑定RAM角色，然后基于STS临时凭证访问其他阿里云产品：

-   AliyunECSImageExportDefaultRole：为ECS实例绑定该角色后，即可获得导出ECS实例镜像所需的权限，对应的默认权限策略为AliyunECSImageExportRolePolicy。
-   AliyunECSImageImportDefaultRole：为ECS实例绑定该角色后，即可获得导入镜像所需的权限，对应的默认权限策略为AliyunECSImageImportRolePolicy。
-   AliyunECSInstanceForYundunSysTrustRole：为ECS实例绑定该角色后，即可获得使用阿里云可信服务所需的权限，对应的默认权限策略为AliyunECSInstanceForYundunSysTrustRolePolicy。
-   AliyunECSDiskEncryptDefaultRole：为ECS实例绑定该角色后，即可获得加密云盘所需的权限，对应的默认权限策略为AliyunECSDiskEncryptRolePolicy。

**相关文档**  


[什么是访问控制](/intl.zh-CN/产品简介/什么是访问控制.md)

