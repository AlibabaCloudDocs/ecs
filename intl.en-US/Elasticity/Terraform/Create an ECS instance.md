# Create an ECS instance

This topic describes how to create an Elastic Compute Service \(ECS\) instance by using Terraform.

1.  Create a VPC and a vSwitch.

    Terraform 0.11 is used in this example.

    **Note:** In Terraform 0.11 and earlier, the example usage of the variable expression is `vpc_id = "${alicloud_vpc.vpc.id}"`. In Terraform 0.12 and later, the example usage of the variable expression is updated to `vpc_id = "alicloud_vpc.vpc.id"`. Use the corresponding variable expression based on your Terraform version.

    1.  Create the terraform.tf file, enter the following content, and then save the file to the current working directory.

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

    2.  Run the terraform init command to initialize the environment.

    3.  Run the terraform plan command to view resources.

    4.  After you confirm that the resources are correct, run the terraform apply command to create the VPC and vSwitch.

    5.  Run the terraform show command to view the created VPC and vSwitch.

        You can also log on to the VPC console to view the attributes of the VPC and vSwitch.

2.  Create a security group and apply the security group to the created VPC.

    1.  In the terraform.tf file, add the following content:

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

    2.  Run the terraform plan command to view resources.

    3.  After you confirm that the resources are correct, run the terraform apply command to create the security group and add the security group rule.

    4.  Run the terraform show command to view the created security group and added security group rule.

        You can also log on to the ECS console to view the security group and security group rule.

3.  Creates an ECS instance.

    1.  In the terraform.tf file, add the following content:

        ```
        resource "alicloud_instance" "instance" {
          # cn-beijing
          availability_zone = "cn-beijing-b"
          security_groups = ["${alicloud_security_group.default. *.id}"]
        
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

        **Note:**

        -   In the preceding example, `internet_max_bandwidth_out = 10` is set to 10. As a result, a public IP address is automatically assigned to the instance.
        -   For more information about the parameters, visit the Argument Reference section in [alicloud\_instance](https://www.terraform.io/docs/providers/alicloud/r/instance.html).
    2.  Run the terraform plan command to view resources.

    3.  After you confirm that the resources are correct, run the terraform apply command to create the ECS instance.

    4.  Run the terraform show command to view the created ECS instance.

    5.  Run the ssh root@<publicip\> command and enter the password to access the ECS instances.


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
  security_groups = ["${alicloud_security_group.default. *.id}"]

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

