# General process

This topic describes how to use the ECS Java SDK by taking DescribeImages as an example. DescribeImages is the operation used by the ECS Java SDK to query available image resources.

You have created an AccessKey pair. For information about how to create an AccessKey pair, see [Create an AccessKey]().

**Note:** To protect the AccessKey pair of your Alibaba Cloud account, we recommend that you create a RAM user, grant the RAM user the permissions to access ECS instances, and then use the AccessKey pair of the RAM user to call the Java SDK. For more information, see [Implement access control by using RAM](/intl.en-US/Security/Implement access control by using RAM.md).

-   In this example, the IClientProfile and IAcsClient classes are included in aliyun-java-sdk-core, and the other classes are included in aliyun-java-sdk-ecs.
-   The purpose of this example is to query ECS public images. For information about public images, see image related documentation. For more information, see [Overview](/intl.en-US/Images/Public image/Overview.md).
-   The following table compares the methods used by the previous SDK and by the new SDK, their classes, and objects. If you are using the previous SDK, we recommend that you switch to the new version to obtain the new features.

    |Item|New SDK|Earlier SDK|
    |:---|-------|:----------|
    |Submit a request|getAcsResponse\(\)|execute\(\)|
    |Class that stores the AccessKey pair|IClientProfile|AliyunClient|
    |Objects for storing identity credentials|DefaultProfile.getProfile\(RegionId, AccessKey, AccessKeySecret\)|new DefaultAliyunClient\(APIUrl, AccessKey, AccessKeySecret\)|
    |Package name prefix|com.aliyuncs|com.aliyun.api|


1.  Generate the profile object from the IClientProfile class.

    The profile object stores the region, AccessKey ID, and AccessKey secret, such as the cn-hangzhou in this example. For more information about regions, see [Regions and zones]().

    ```
    IClientProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<yourAccessKeyID>", "<yourAccessKeySecret>");
    ```

2.  Generate the object client of IAcsClient from the IClientProfile class.

    Subsequently obtain response from IClientProfile.

    ```
    IAcsClient client = new DefaultAcsClient(profile);
    ```

3.  Create a request for the API opertion and use the constructor to generate a default class request.

    The class is named after the API operation name followed by Request. The API operation for obtaining the image list is named DescribeImages and the corresponding request class name is DescribeImagesRequest.

    ```
    DescribeImagesRequest request = new DescribeImagesRequest();
    ```

4.  Set parameters for the request class.

    Set required parameters in the API operation through the setXxx method of the request class. Set parameters through the setXxx method. In the example:

    -   The DescribeImages API operation uses RegionId to specify the region.
    -   The DescribeImages API operation uses ImageOwnerAlias to specify the image type to be queried. The value of setImageOwnerAlias is system, which indicates public images.
    ```
    request.setImageOwnerAlias("system");
    ```

5.  Obtain the response corresponding to the specified request parameter through the client object.

    ```
    DescribeImagesResponse response = client.getAcsResponse(request);
    System.out.println(JSON.toJSONString(response));
    ```

6.  Obtain the returned parameter value by calling the corresponding getXxx method in response.

    If you need to obtain the name of an image, you must obtain the collection of image objects by calling getImages\(\), the information of the target image by traversing the image objects, and the details of the image by calling getgetImageName\(\) or getgetImageId.

    ```
    for(DescribeImagesResponse.Image image:response.getImages())
                {
                    System.out.println(image.getImageId());
                    System.out.println(image.getImageName());
                }
    ```

    Based on different API operations, the response may contain multi-layer information. For example, if you call the DescribeImages operation, the response is represented as a collection in the form of list that stores the information about each image. You must obtain the collection of image objects by calling getImages\(\), the information of an image by traversing the image objects, and the details of the image by calling getXxx.

7.  Handle server and client errors by using catch\(\).

    -   Server error

        ```
        catch (ServerException e) {
                    e.printStackTrace();
        ```

    -   Client error

        ```
        catch (ClientException e) {
                    System.out.println("ErrCode:" + e.getErrCode());
                    System.out.println("ErrMsg:" + e.getErrMsg());
                    System.out.println("RequestId:" + e.getRequestId());
        ```


-   The complete response is as follows:

    ```
    {
        "PageNumber": 1,
        "TotalCount": 43,
        "PageSize": 1,
        "RegionId": "cn-hangzhou",
        "RequestId": "C93F3D9F-CF25-47DF-9C0F-614395E5DCAC",
        "Images": {
            "Image": [
                {
                    "ImageId": "freebsd_11_02_64_30G_alibase_20190722.vhd",
                    "Description": "",
                    "OSNameEn": "FreeBSD  11.2 64 bit",
                    "ProductCode": "",
                    "ResourceGroupId": "",
                    "OSType": "linux",
                    "Architecture": "x86_64",
                    "OSName": "FreeBSD  11.2 64-bit",
                    "DiskDeviceMappings": {
                        "DiskDeviceMapping": []
                    },
                    "ImageOwnerAlias": "system",
                    "Progress": "100%",
                    "IsSupportCloudinit": false,
                    "Usage": "instance",
                    "CreationTime": "2019-07-23T05:41:06Z",
                    "Tags": {
                        "Tag": []
                    },
                    "ImageVersion": "",
                    "Status": "Available",
                    "ImageName": "freebsd_11_02_64_30G_alibase_20190722.vhd",
                    "IsSupportIoOptimized": true,
                    "IsSelfShared": "",
                    "IsCopied": false,
                    "IsSubscribed": false,
                    "Platform": "Freebsd",
                    "Size": 30
                }
            ]
        }
    }
    ```

-   Obtain the query results of specific returned parameters, such as ImageId and ImageName:

    ```
    freebsd_11_02_64_30G_alibase_20190722.vhd
    freebsd_11_02_64_30G_alibase_20190722.vhd
    ```


## Sample code

The following example shows complete Java SDK code.

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.alibaba.fastjson.JSON;
import java.util.*;
import com.aliyuncs.ecs.model.v20140526.*;

public class DescribeImages {

    public static void main(String[] args) {
        DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "LTAjVUwKznS*****", "BNPO1zoNSi484oizGM9fzzwJJ*****");
        IAcsClient client = new DefaultAcsClient(profile);

        DescribeImagesRequest request = new DescribeImagesRequest();
        request.setRegionId("cn-hangzhou");
        request.setImageOwnerAlias("system");
        request.setPageNumber(1);
        request.setPageSize(1);

        try {
            DescribeImagesResponse response = client.getAcsResponse(request);
            System.out.println(JSON.toJSONString(response));
            for(DescribeImagesResponse.Image image:response.getImages())
            {
                System.out.println(image.getImageId());
                System.out.println(image.getImageName());
            }
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

**Related topics**  


[DescribeImages](/intl.en-US/API Reference/Images/DescribeImages.md)

