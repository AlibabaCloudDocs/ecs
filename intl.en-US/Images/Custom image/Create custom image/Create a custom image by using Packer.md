# Create a custom image by using Packer

Packer is a lightweight open source tool for creating images and runs on commonly used mainstream operating systems such as Windows, Linux, and macOS. This topic describes how to install and use Packer to create a custom image.

A Linux instance is used in the following examples. For more information about how to install Packer in Windows, visit [Packer documentation](https://www.packer.io/intro/getting-started/install.html).

## Step 1: Install Packer

1.  Connect to a Linux instance.

    For more information, see [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).

2.  Run the `cd /usr/local/bin` command to access the /usr/local/bin directory.

    **Note:** The /usr/local/bin directory is an environment variable directory. You can install Packer to this directory or the directory that is added to environment variables.

3.  Run the `wget https://releases.hashicorp.com/packer/1.1.1/packer_1.1.1_linux_amd64.zip` command to download the Packer package.

    You can go to the [Download Packer](https://www.packer.io/downloads.html) page to download other versions of Packer packages.

4.  Run the `unzip packer_1.1.1_linux_amd64.zip` command to decompress the package.

5.  Run the `packer -v` command to verify the installation status of Packer.

    -   If the Packer version number is returned, Packer is installed.
    -   If the `command not found` error is returned, Packer is not installed properly.

## Step 2: Define a Packer template

If you want to use Packer to create a custom image, you must create a template in the JSON format. In the template, you must specify the image builder and provisioner. For more information, visit [Alicloud Image Builder](https://www.packer.io/docs/builders/alicloud-ecs.html) and [Provisioners](https://www.packer.io/docs/provisioners). Packer provides a variety of provisioners that allow you to configure the content generation mode for custom images. A Shell provisioner is used to define a Packer template in the following example.

Create a JSON file named alicloud in the Linux instance and paste the following information to the file:

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

The following table describes the parameters that you must specify.

|Parameter|Description|
|:--------|:----------|
|access\_key|The AccessKey ID of your account. For more information, see [Create an AccessKey pair](). **Note:** To avoid disclosing the AccessKey pair of your Alibaba Cloud account, we recommend that you create a RAM user and use the credentials of the RAM user to create an AccessKey pair. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md) and [Create an AccessKey](). |
|secret\_key|The AccessKey secret of your account. For more information, see [Create an AccessKey]().|
|region|The region of the temporary instance used to create the custom image.|
|image\_name|The name of the custom image.|
|source\_image|The name of the source image used to create the custom image. You can obtain the name from the public image list of Alibaba Cloud.|
|instance\_type|The type of the temporary instance used to create the custom image.|
|internet\_charge\_type|The billing method for network usage of the temporary instance used to create the custom image.|
|provisioners|The provisioner used to create the custom image. For more information, visit [Provisioners](https://www.packer.io/docs/provisioners).|

## Step 3: Create a custom image by using Packer

Perform the following operations to create a custom image by using the Packer template file that you specified:

1.  Run the `export ALICLOUD_ACCESS_KEY=<Your AccessKey ID>` command to import your AccessKey ID.

2.  Run the `export ALICLOUD_SECRET_KEY=<Your AccessKey secret>` command to import your AccessKey secret.

3.  Run the `packer build alicloud.json` command to create a custom image.


The following section shows the command output. It describes how to create a custom image that contains ApsaraDB for Redis:

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

[Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md)

**Related topics**  


[packer-provider](https://github.com/alibaba/packer-provider)

[Packer documentation](https://www.packer.io/docs)

