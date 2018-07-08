# Use Packer to create a custom image {#concept_idd_4cm_xdb .concept}

[Packer](https://www.packer.io/) is a convenient open-source tool to create custom images. It runs on major operating systems. This document provides information about how to install and use Packer. With Packer, you can easily create a custom image by using only one or two lines of commands.

## Prerequisites {#section_qbp_xcm_xdb .section}

You must have the AccessKey ready. For more information, see [Create AccessKey](https://help.aliyun.com/document_detail/53045.html) .

**Note:** 

The AccessKey has a high level of account privileges. To avoid improper operations and data breach, we recommend that you [Create a RAM user](../../../../intl.en-US/Quick Start/Create a RAM user.md#), and act as a RAM user to [create your AccessKey](https://help.aliyun.com/document_detail/53045.html).

## Step 1.  Install Packer {#section_j5g_gdm_xdb .section}

Go to the official  [download page of Packer](https://www.packer.io/downloads.html) where you can choose and download the version of Packer for your operating system. Follow these steps or visit the official [installation page of Packer](https://www.packer.io/docs/install/index.html) for how to install Packer.

**To install Packer on a Linux server**

1.  Connect and log on to the Linux server. If the server you want to connect to is an ECS Linux instance, see [Connect to a Linux instance by using a password](intl.en-US/User Guide/Connect/Connect to a Linux instance by using a password.md#).
2.  Run `cd /usr/local/bin` to go to the /usr/local/bin directory. 

    **Note:** The /usr/local/bin directory is an environment variable directory. ou can install Packer to this directory or another directory that has been added to the environment variable.

3.  Run `wget https://releases.hashicorp.com/packer/1.1.1/packer_1.1.1_linux_amd64.zip` to download the Packer installer. You can visit the official [download page of Packer](https://www.packer.io/downloads.html) to download installers for other versions of Packer.
4.  Run `unzip packer_1.1.1_linux_amd64.zip` to unzip the package.
5.  Run `packer -v` to verify Packer’s installation status. If the Packer version number is returned, you have successfully installed Packer.  If error **command not found** is returned,  Packer has not been correctly installed.

**To install Packer on a Windows server**

Take Windows Server 2012 64-bit as an example:

1.  Connect and log on to the Windows server. If the server you want to connect to is an ECS Windows instance, see [Connect to a Windows instance](intl.en-US/User Guide/Connect/Connect to a Windows instance.md#).
2.  Open the official [download page of Packer](https://www.packer.io/downloads.html)  and select an appropriate Packer installer for 64-bit Windows.
3.  Unzip the package to a specified directory and install Packer.
4.  Define the directory for Packer in the PATH environment variable.
    1.  Open the **Control Panel**.
    2.  Select **All Control Panel Items** \> **System** \> **Advanced System Settings**.
    3.  Click **Environment Variable**.

        ![](images/4603_en-US.png)

    4.  Find **Path** in the system variable list.

        ![](images/4604_en-US.png)

    5.  Add the Packer installation directory to the **Variable Value**,  such as C:\\Packer as seen in this example. Separate multiple directories with half-width semicolons \(;\).  Click **/OK**。

        ![](images/4605_en-US.png)

5.  Run `packer.exe -v`  in CMD to verify Packer’s installation status.  If the Packer version number is returned, you have successfully installed Packer.  If error  **command not found** prompt is returned,  Packer has not been correctly installed.

## Step 2. Define a Packer template {#section_kwk_bdv_ydb .section}

**Note:** 

To create a custom image by using Packer, firstly, create a JSON format template file. In the template, specify the  [Alibaba Cloud Image Builder](https://www.packer.io/docs/builders/alicloud-ecs.html) and  [Provisioner](https://www.packer.io/docs/provisioners/index.html) for the custom image to be created. Packer  has diverse provisioners for you to choose from when configuring the content generation mode of the custom image.In the following alicloud JSON file, we have used the [Shell](https://www.packer.io/docs/provisioners/shell.html) provisioner as an example to illustrate how to define a Packer template.

Create a JSON file named alicloud and paste the following content:

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
    "io_optimized":"true",
    "internet_charge_type":"PayByTraffic"
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

**Note:** You must customize the values of the following parameters.

|Parameter| Description|
|access\_key| Your AccessKey ID For more details, see creating an accesskey.|
|secret\_key|Your AccessKey Secret For more information, see [Create AccessKey](https://help.aliyun.com/document_detail/53045.html).|
|region|The region of the temporary instance used to create the custom image. |
|image\_name| The custom image’s name|
|source\_image|You can retrieve the basic image name from Alibaba Cloud public image list.|
|instance\_type|Type of the temporary instance generated to create the custom image. |
|internet\_charge\_type|Internet bandwidth billing method for the temporary instance generated for creating the custom image. |
|provisioners|Type of [Packer Provisioner](https://www.packer.io/docs/provisioners/index.html) used for creating the custom image|

## Step 3. Create a custom image by using Packer {#section_jwh_ldv_ydb .section}

Follow these step to specify the Packer template file and create a custom image:

1.  Run `export ALICLOUD_ACCESS_KEY=your AccessKeyID`  to import your AccessKey ID.
2.  Run `export ALICLOUD_SECRET_KEY=your AccessKeySecret`  to import your AccessKey Secret.
3.  Run `packer build alicloud.json` to create the custom image.

The sample runs like follows. The sample creates a custom image containing ApsaraDB for Redis and runs as follows:

```

alicloud-ecs output will be in this color.
==> alicloud-ecs: Prevalidating alicloud image name...
alicloud-ecs: Found image ID: centos_7_02_64_20G_alibase_20170818.vhd
==> alicloud-ecs: Start creating temporary keypair: packer_59e44f40-c8d6-0ee3-7fd8-b1ba08ea94b8
==> alicloud-ecs: Start creating alicloud vpc

==> alicloud-ecs: Provisioning with shell script: /var/folders/3q/w38xx_js6cl6k5mwkrqsnw7w0000gn/T/packer-shell257466182
alicloud-ecs: Loaded plugins: fastestmirror

alicloud-ecs: Total 1.3 MB/s | 650 kB 00:00
alicloud-ecs: Running transaction check

==> alicloud-ecs: Deleting temporary keypair...
Build 'alicloud-ecs' finished.
==> Builds finished. The artifacts of successful builds are:
--> alicloud-ecs: Alicloud images were created:
cn-beijing: m-2ze12578be1oa4ovs6r9
```

## Next steps {#section_chp_qdv_ydb .section}

You can use this custom image to create an ECS instance. For more information, see [Create an instance from a custom image](intl.en-US/User Guide/Instances/Create an instance/Create an instance from a custom image.md#).

## References {#section_ntx_rdv_ydb .section}

-   For more information, visit [packer-provider](https://github.com/alibaba/packer-provider) , the Packer repository of Alibaba Cloud Github.
-   See the [Packer Official Documents](https://www.packer.io/docs/index.html) to learn more about how to use Packer.

