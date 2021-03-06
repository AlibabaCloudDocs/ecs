# Use faascmd

This topic describes how to use faascmd commands.

faascmd is configured. For more information, see [Configure faascmd](/intl.en-US/Best Practices/FaaS instances best practices/faascmd tool/Configure faascmd.md).

The following conditions are met before you can use the authorization command:

1.  An Object Storage Service \(OSS\) bucket is created for FPGA as a Service \(FaaS\) to upload the originally compiled DCP file.
2.  A folder named compiling\_logs is created in the bucket.

Description of the faascmd command syntax:

-   All commands and parameters provided by faascmd are case-sensitive.
-   In faascmd commands, extra spaces are not allowed between parameters, `equal signs (=)`, or values.

This topic describes the following faascmd commands:

-   [Authorize RAM users](#section_l22_m3t_2lm)
-   [View an authorization policy](#section_zns_gx0_rw5)
-   [Delete an authorization policy](#section_4ql_7ju_xc6)
-   [View all objects in an OSS bucket](#section_pai_qvg_9a3)
-   [Upload an originally compiled file](#section_bd6_8gn_vz1)
-   [Download an object from an OSS bucket](#section_518_vs9_hic)
-   [Create an FPGA image](#section_4mb_909_zbm)
-   [View FPGA images](#section_o0h_qkz_zzx)
-   [Delete FPGA images](#section_k1c_yj3_wls)
-   [Download an FPGA image](#section_0xf_a3k_662)
-   [View the download status of an FPGA image](#section_a6q_bsy_kau)
-   [Publish an FPGA image](#section_wct_1ue_ya8)
-   [Query information of FPGA-accelerated instances](#section_5za_vje_45r)

## Authorize RAM users

You can run the `faascmd auth` command to authorize a RAM user to access your OSS buckets as a FaaS administrator.

Command format:

```
faascmd auth --bucket=<YourFaasOSSBucketName>
```

Sample code

![Authorize RAM users](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5614488951/p31129.png)

**Note:** If your Alibaba Cloud account has multiple RAM users, we recommend that you share the OSS bucket to the RAM users so that you do not have to repeatedly modify or overwrite authorization policies.

## View an authorization policy

You can run the `faascmd list_policy` command to check whether the specified OSS bucket is contained in the corresponding authorization policy \(faasPolicy\).

Command format:

```
faascmd list_policy
```

Sample code

![View an authorization policy](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6614488951/p31130.png)

**Note:** Check whether your OSS bucket and the compiling\_logs folder in the bucket are displayed in the policy information.

## Delete an authorization policy

You can run the `faascmd delete_policy` command to delete an authorization policy \(faasPolicy\).

Command format:

```
faascmd delete_policy
```

Sample code

![Delete an authorization policy](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6614488951/p31131.png)

**Note:** If your Alibaba Cloud account has multiple RAM users, we recommend that you perform this operation in the [RAM console](https://ram.console.aliyun.com/) to avoid unexpected policy deletion.

## View all objects in an OSS bucket

You can run the `faascmd list_objects` command to view all objects in an OSS bucket.

Command format:

```
faascmd list_objects
```

Sample code

![View objects](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6614488951/p31132.png)

**Note:** You can combine this command with the grep command to filter objects. Example: `faascmd list_objects | grep "xxx"`.

## Upload an originally compiled file

You can run the `faascmd upload_object` command to upload original copies of files compiled on your local PC to a specified OSS bucket.

Command format:

```
faascmd upload_object --object=<NewFileNameInOSSBucket> --file=<YourFilePath>/<FileNameYouWantToUpload>           
```

Sample code

![upload_object](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6614488951/p31112.png)

**Note:**

-   If the file to be uploaded is stored in the current directory, you do not need to specify a path.
-   Locally compiled original files provided by Intel FPGA are in the .gbs format and those provided by Xilinx FPGA are compressed as packages in the .tar format after script processing.

## Download an object from an OSS bucket

You can run the `faascmd get_object` command to download the specified object from an OSS bucket.

Command format:

```
faascmd get_object --object=<YourObjectName> --file=<YourLocalPath>/<YourFileName>
```

Sample code

![get_object](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6614488951/p31115.png)

**Note:** If you do not specify a path, the object is downloaded to the current folder.

## Create an FPGA image

You can run the `faascmd create_image` command to submit a request to create an FPGA image. If the request succeeds, FpgaImageUUID is returned.

Command format:

```
faascmd create_image --object=<YourObjectName> 
--fpgatype=<intel/xilinx>  --encrypted=<true/false> 
--kmskey=<key/If encrypted is set to true, this parameter is required. Otherwise, this parameter is optional.> 
--shell=<Shell Version/Required> --name=<name/Optional> 
--description=<description/Optional> --tags=<tags/Optional>
```

Sample code

![create_image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6614488951/p31117.png)

## View FPGA images

You can run the `faascmd list_images` command to view the information of all FPGA images that you created.

Command format:

```
faascmd list_images
```

Sample code

![list_images](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6614488951/p31118.png)

**Note:** Each RAM user can have up to 10 FPGA images.

## Delete FPGA images

You can run the `faascmd delete_image` command to delete an FPGA image.

Command format:

```
faascmd delete_image --imageuuid=<yourImageuuid>
```

Sample code

![delete_image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6614488951/p31120.png)

## Download an FPGA image

You can run the `faascmd download_image` command to submit a request to download an FPGA image.

Command format:

```
faascmd download_image  --instanceId=<YourInstanceId> 
--fpgauuid=<Yourfpgauuid> --fpgatype=<intel/xilinx> 
--imageuuid=<YourImageuuid> --imagetype=<afu> 
--shell=<YourImageShellVersion>
```

Sample code

```
faascmd download_image --instanceId=XXXXX --fpgauuid=XXXX --fpgatype=intel --imageuuid=XXXX
```

## View the download status of an FPGA image

You can run the `faascmd fpga_status` command to view the status of the current FPGA board card or the download progress of the FPGA image.

Command format:

```
faascmd fpga_status --fpgauuid=<Yourfpgauuid> --instanceId=<YourInstanceId>
```

Sample code

![fpga_status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6614488951/p31126.png)

## Publish an FPGA image

You can run the `faascmd publish_image` command to submit a request to publish an FPGA image.

Command format:

```
faascmd publish_image --imageuuid=<YourImageuuid> --imageid=<YourInstanceImageid>
```

**Note:**

-   imageuuid indicates the ID of the image that you want to publish to Alibaba Cloud Marketplace. You can run the `faascmd list_images` command to view this image ID.
-   imageid indicates the image ID of the current FPGA-accelerated instance. You can go to the product details page in the [ECS console](https://ecs.console.aliyun.com) to view this image ID.

## Query information of FPGA-accelerated instances

You can run the `faascmd list_instances` command to query the basic information of an FPGA-accelerated instance such as the instance ID, FPGA board card information, and shell version.

Command format:

```
faascmd list_instances --instanceId=<YourInstanceId>
```

Sample code

![list_instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7614488951/p31128.png)

