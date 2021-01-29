# Create an ECS instance

This topic describes how to create an Elastic Compute Service \(ECS\) instance by using Terraform.

Before you begin, ensure that you have completed the following operations:

-   Prepare an Alibaba Cloud account and an AccessKey pair \(AccessKey ID and AccessKey secret\) to use Terraform. You can go to the [Security Management](https://usercenter.console.aliyun.com/?spm=5176.doc52740.2.3.QKZk8w#/manage/ak) page of the Alibaba Cloud console to create or view your AccessKey pair.
-   Install and configure Terraform. For more information, see [Install and configure Terraform in the local PC]() and [Use Terraform in Cloud Shell]().

1.  Create a VPC and a VSwitch.

    1.  Create the terraform.tf file, enter the following content, and save the file to the current working directory.

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

    2.  Run the `terraform apply` command to create the VPC and VSwitch.
    3.  Run the `terraform show` command to view the created VPC and VSwitch.

        You can also log on to the VPC console to view the attributes of the VPC and VSwitch.

2.  Create a security group in the VPC created in the previous step, and add a security group rule to allow access from all IP addresses.

    1.  In terraform.tf, add the following content:

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

    2.  Run the `terraform apply` command to create the security group and add the security group rule.
    3.  Run the `terraform show` command to view the created security group and added security group rule.

        You can also log on to the ECS console to view the security group and security group rule.

3.  Create an ECS instance.

    1.  In terraform.tf, add the following content:

        ```
        resource "alicloud_instance" "instance" {
          # cn-beijing
          availability_zone = "cn-beijing-b"
          security_groups = alicloud_security_group.default. *.id
        
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

        **Note:**

        -   In the preceding example, `Internet_max_bandwidth_out` is set to 10. Therefore, the ECS instance is assigned a public IP address automatically.
        -   For a detailed description of the parameters, see [Parameter description](https://www.terraform.io/docs/providers/alicloud/r/instance.html).
    2.  Run the `terraform apply` command to create the ECS instance.
    3.  Run the `terraform show` command to view the created ECS instance.
    4.  Run the ssh root@<publicip\> command and enter the password to access the ECS instance.

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
  security_groups = alicloud_security_group.default. *.id
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

