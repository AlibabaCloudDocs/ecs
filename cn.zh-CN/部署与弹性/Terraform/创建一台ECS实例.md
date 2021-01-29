# 创建一台ECS实例

本文介绍如何使用Terraform创建一台ECS实例。

在开始之前，请您确保完成以下操作：

-   使用Terraform，您需要一个阿里云账号和访问密钥（AccessKey）。 请在阿里云控制台中的[AccessKey管理页面](https://usercenter.console.aliyun.com/?spm=5176.doc52740.2.3.QKZk8w#/manage/ak)上创建和查看您的AccessKey。
-   已经安装并配置了Terraform，具体操作请参见[在本地安装和配置Terraform]()和[在Cloud Shell中使用Terraform]()。

1.  创建专有网络和交换机。

    1.  创建terraform.tf文件，输入以下内容，并保存在当前的执行目录中。

        ```
        resource "alicloud_vpc" "vpc" {
          name       = "tf_test_foo"
          cidr_block = "172.16.0.0/12"
        }
        
        resource "alicloud_vswitch" "vsw" {
          vpc_id            = alicloud_vpc.vpc.id
          cidr_block        = "172.16.0.0/21"
          availability_zone = "cn-beijing-b"
        }
        ```

    2.  运行`terraform apply`开始创建。
    3.  运行`terraform show`查看已创建的专有网络和交换机。

        您也可以登录VPC控制台查看专有网络和交换机的属性。

2.  在上一步创建的专有网络中创建一个安全组，并添加一个允许任何地址访问的安全组规则。

    1.  在terraform.tf文件中增加以下内容。

        ```
        resource "alicloud_security_group" "default" {
          name = "default"
          vpc_id = alicloud_vpc.vpc.id
        }
        
        resource "alicloud_security_group_rule" "allow_all_tcp" {
          type              = "ingress"
          ip_protocol       = "tcp"
          nic_type          = "intranet"
          policy            = "accept"
          port_range        = "1/65535"
          priority          = 1
          security_group_id = alicloud_security_group.default.id
          cidr_ip           = "0.0.0.0/0"
        }
        ```

    2.  运行`terraform apply`开始创建。
    3.  运行`terraform show`查看已创建的安全组和安全组规则。

        您也可以登录ECS控制台查看安全组和安全组规则。

3.  创建ECS实例。

    1.  在terraform.tf文件中增加以下内容。

        ```
        resource "alicloud_instance" "instance" {
          # cn-beijing
          availability_zone = "cn-beijing-b"
          security_groups = alicloud_security_group.default.*.id
        
          # series III
          instance_type        = "ecs.n2.small"
          system_disk_category = "cloud_efficiency"
          image_id             = "ubuntu_18_04_64_20G_alibase_20190624.vhd"
          instance_name        = "test_foo"
          vswitch_id = alicloud_vswitch.vsw.id
          internet_max_bandwidth_out =10
          password = "<replace_with_your_password>"
        }
        ```

        **说明：**

        -   在上述示例中，指定了`internet_max_bandwidth_out= 10`，因此会自动为实例分配一个公网IP。
        -   详细的参数解释请参见 [阿里云参数说明](https://www.terraform.io/docs/providers/alicloud/r/instance.html)。
    2.  运行`terraform apply`开始创建。
    3.  运行`terraform show`查看已创建的ECS实例。
    4.  运行ssh root@<publicip\>，并输入密码来访问ECS实例。

```
provider "alicloud" {}

resource "alicloud_vpc" "vpc" {
  name       = "tf_test_foo"
  cidr_block = "172.16.0.0/12"
}

resource "alicloud_vswitch" "vsw" {
  vpc_id            = alicloud_vpc.vpc.id
  cidr_block        = "172.16.0.0/21"
  availability_zone = "cn-beijing-b"
}

resource "alicloud_security_group" "default" {
  name = "default"
  vpc_id = alicloud_vpc.vpc.id
}

resource "alicloud_instance" "instance" {
  # cn-beijing
  availability_zone = "cn-beijing-b"
  security_groups = alicloud_security_group.default.*.id
  # series III
  instance_type        = "ecs.n2.small"
  system_disk_category = "cloud_efficiency"
  image_id             = "ubuntu_18_04_64_20G_alibase_20190624.vhd"
  instance_name        = "test_foo"
  vswitch_id = alicloud_vswitch.vsw.id
  internet_max_bandwidth_out = 10
}

resource "alicloud_security_group_rule" "allow_all_tcp" {
  type              = "ingress"
  ip_protocol       = "tcp"
  nic_type          = "intranet"
  policy            = "accept"
  port_range        = "1/65535"
  priority          = 1
  security_group_id = alicloud_security_group.default.id
  cidr_ip           = "0.0.0.0/0"
}
```

