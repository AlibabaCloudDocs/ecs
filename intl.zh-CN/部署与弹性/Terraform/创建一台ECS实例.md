# 创建一台ECS实例

本文介绍如何使用Terraform创建一台ECS实例。

1.  创建VPC网络和交换机。

    本示例中Terraform的版本为0.11。

    **说明：** Terraform 0.11及更早的版本，变量表达式使用示例为`vpc_id = "${alicloud_vpc.vpc.id}"`。Terraform 0.12版本进行了更新，变量表达式使用示例为`vpc_id = "alicloud_vpc.vpc.id"`。请根据您安装的版本修改相应的变量表达式的格式。

    1.  创建terraform.tf文件，输入以下内容，并保存在当前的执行目录中。

        ```
        resource "alicloud_vpc" "vpc" {
          name       = "tf_test_foo"
          cidr_block = "172.16.0.0/12"
        }
        
        resource "alicloud_vswitch" "vsw" {
          vpc_id            = "${alicloud_vpc.vpc.id}"
          cidr_block        = "172.16.0.0/21"
          availability_zone = "cn-beijing-b"
        }
        ```

    2.  运行terraform init初始化环境。

    3.  运行terraform plan查看资源。

    4.  确认资源无误后，运行terraform apply开始创建。

    5.  运行terraform show查看已创建的VPC和VSwitch。

        您也可以登录VPC控制台查看VPC和VSwitch的属性。

2.  创建安全组，并将安全组作用于上一步创建的VPC中。

    1.  在terraform.tf文件中增加以下内容。

        ```
        resource "alicloud_security_group" "default" {
          name = "default"
          vpc_id = "${alicloud_vpc.vpc.id}"
        }
        
        resource "alicloud_security_group_rule" "allow_all_tcp" {
          type              = "ingress"
          ip_protocol       = "tcp"
          nic_type          = "intranet"
          policy            = "accept"
          port_range        = "22/22"
          priority          = 1
          security_group_id = "${alicloud_security_group.default.id}"
          cidr_ip           = "0.0.0.0/0"
        }
        ```

    2.  运行terraform plan查看资源。

    3.  确认资源无误后，运行terraform apply开始创建。

    4.  运行terraform show查看已创建的安全组和安全组规则。

        您也可以登录ECS控制台查看安全组和安全组规则。

3.  创建ECS实例。

    1.  在terraform.tf文件中增加以下内容。

        ```
        resource "alicloud_instance" "instance" {
          # cn-beijing
          availability_zone = "cn-beijing-b"
          security_groups = ["${alicloud_security_group.default.*.id}"]
        
          # series III
          instance_type        = "ecs.n2.small"
          system_disk_category = "cloud_efficiency"
          image_id             = "ubuntu_140405_64_40G_cloudinit_20161115.vhd"
          instance_name        = "test_foo"
          vswitch_id = "${alicloud_vswitch.vsw.id}"
          internet_max_bandwidth_out = 10
          password = "<replace_with_your_password>"
        }
        ```

        **说明：**

        -   在上述示例中，指定了`internet_max_bandwidth_out = 10`，因此会自动为实例分配一个公网IP。
        -   详细的参数解释请参见[阿里云参数说明](https://www.terraform.io/docs/providers/alicloud/r/instance.html)。
    2.  运行terraform plan查看资源。

    3.  确认资源无误后，运行terraform apply开始创建。

    4.  运行terraform show查看已创建的ECS实例。

    5.  运行ssh root@<publicip\>，并输入密码来访问ECS实例。


```
provider "alicloud" {}

resource "alicloud_vpc" "vpc" {
  name       = "tf_test_foo"
  cidr_block = "172.16.0.0/12"
}

resource "alicloud_vswitch" "vsw" {
  vpc_id            = "${alicloud_vpc.vpc.id}"
  cidr_block        = "172.16.0.0/21"
  availability_zone = "cn-beijing-b"
}


resource "alicloud_security_group" "default" {
  name = "default"
  vpc_id = "${alicloud_vpc.vpc.id}"
}


resource "alicloud_instance" "instance" {
  # cn-beijing
  availability_zone = "cn-beijing-b"
  security_groups = ["${alicloud_security_group.default.*.id}"]

  # series III
  instance_type        = "ecs.n2.small"
  system_disk_category = "cloud_efficiency"
  image_id             = "ubuntu_140405_64_40G_cloudinit_20161115.vhd"
  instance_name        = "test_foo"
  vswitch_id = "${alicloud_vswitch.vsw.id}"
  internet_max_bandwidth_out = 10
}


resource "alicloud_security_group_rule" "allow_all_tcp" {
  type              = "ingress"
  ip_protocol       = "tcp"
  nic_type          = "intranet"
  policy            = "accept"
  port_range        = "22/22"
  priority          = 1
  security_group_id = "${alicloud_security_group.default.id}"
  cidr_ip           = "0.0.0.0/0"
}
```

