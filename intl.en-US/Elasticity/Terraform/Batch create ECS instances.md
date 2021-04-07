# Batch create ECS instances

This topic describes how to use Terraform to batch create ECS instances.

Before you begin, make sure that you have completed the following operations:

-   Prepare an Alibaba Cloud account and an AccessKey pair \(AccessKey ID and AccessKey secret\) to use Terraform. You can go to the [Security Management](https://usercenter.console.aliyun.com/?spm=5176.doc52740.2.3.QKZk8w#/manage/ak) page of the Alibaba Cloud console to create or view your AccessKey pair.
-   Install and configure Terraform. For more information, see [Install and configure Terraform in the local PC]() and [Use Terraform in Cloud Shell]().

1.  Create a VPC and a vSwitch.

    1.  Create the terraform.tf file, enter the following content, and then save the file to the current working directory.

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

    2.  Run the `terraform apply` command to create the VPC and vSwitch.
    3.  Run the `terraform show` command to view the created VPC and vSwitch.

        You can also log on to the VPC console to view the attributes of the VPC and vSwitch.

2.  Create a security group within the created VPC, and then add a security group rule to allow access from all IP addresses.

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

    2.  Run the `terraform apply` command to create a security group and add a security group rule.
    3.  Run the `terraform show` command to view the created security group and added security group rule.

        You can also log on to the ECS console to view the security group and security group rule.

3.  Use a module to batch create ECS instances. In this example, three ECS instances are created.

    1.  In the terraform.tf file, add the following content:

        ```
        module "tf-instances" {  
         source                      = "alibaba/ecs-instance/alicloud"  
         region                      = "cn-beijing" 
         number_of_instances         = "3" 
         vswitch_id                  = alicloud_vswitch.vsw.id  
         group_ids                   = [alicloud_security_group.default.id]  
         private_ips                 = ["172.16.0.10", "172.16.0.11", "172.16.0.12"]  
         image_ids                   = ["ubuntu_18_04_64_20G_alibase_20190624.vhd"]  
         instance_type               = "ecs.n2.small"   
         internet_max_bandwidth_out  = 10  
         associate_public_ip_address = true  
         instance_name               = "my_module_instances_"  
         host_name                   = "sample"  
         internet_charge_type        = "PayByTraffic"    
         password                    = "User@123"  
         system_disk_category        = "cloud_ssd"  
         data_disks = [    
          {      
            disk_category = "cloud_ssd"      
            disk_name     = "my_module_disk"      
            disk_size     = "50"    
          } 
         ]
        }
        ```

        **Note:** In the preceding example, a public IP address is assigned to the instance because `associate_public_ip_address = true` and `internet_max_bandwidth_out = 10` For a detailed description of the parameters, see [Parameter description](https://registry.terraform.io/modules/alibaba/ecs-instance/alicloud/1.2.2?tab=inputs).

    2.  Run the `terraform apply` command to create the ECS instance.
    3.  Run the `terraform show` command to view the created ECS instance.
    4.  Run the ssh root@<publicip\> command and enter the password to access the ECS instances.

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
  name   = "default"
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

module "tf-instances" {  
 source                      = "alibaba/ecs-instance/alicloud"  
 region                      = "cn-beijing"  
 number_of_instances         = "3"  
 vswitch_id                  = alicloud_vswitch.vsw.id  
 group_ids                   = [alicloud_security_group.default.id]  
 private_ips                 = ["172.16.0.10", "172.16.0.11", "172.16.0.12"]  
 image_ids                   = ["ubuntu_18_04_64_20G_alibase_20190624.vhd"]  
 instance_type               = "ecs.n2.small"   
 internet_max_bandwidth_out  = 10
 associate_public_ip_address = true  
 instance_name               = "my_module_instances_"  
 host_name                   = "sample"  
 internet_charge_type        = "PayByTraffic"   
 password                    = "User@123" 
 system_disk_category        = "cloud_ssd"  
 data_disks = [    
  {      
    disk_category = "cloud_ssd"      
    disk_name     = "my_module_disk"      
    disk_size     = "50"    
  } 
 ]
}
```

**Related topics**  


[terraform-alicloud-ecs-instance](https://github.com/terraform-alicloud-modules/terraform-alicloud-ecs-instance)

