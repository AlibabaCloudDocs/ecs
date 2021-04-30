# 批量创建ECS实例

本文介绍如何通过阿里云ECS Java SDK调用RunInstances创建一台或多台ECS实例。

创建ECS实例前，您必须提前查询以下信息：

-   调用DescribeRegions查询ECS实例启动的阿里云地域，假设为cn-hangzhou。
-   调用DescribeImages接口查看要使用的镜像ID，假设为freebsd\_11\_02\_64\_30G\_alibase\_20190722.vhd。
-   调用DescribeInstanceTypes查询ECS实例使用的实例规格，假设为ecs.g5.large。详情请参见[实例规格族](/cn.zh-CN/实例/实例规格族.md)。
-   调用DescribeSecurityGroups查询指定地域中的一个或多个安全组ID，假设为sg-bp1fg655nh68xyz9i\*\*\*。安全组的网络类型将决定ECS实例的网络类型，例如，如果您选择的是一个专有网络VPC类型的安全组，则新建的ECS实例会自动加入安全组所属的专有网络VPC。
-   如果安全组的网络类型为专有网络VPC，调用VPC API DescribeVSwitches查询安全组所属专有网络VPC中的虚拟交换机ID，假设为vsw-bp1wt4qpuavdb6y6k8\*\*\*。
-   开通按量付费ECS资源时，您的阿里云账户余额（即现金余额）和代金券的总值不得小于100.00元人民币。

本文调用RunInstances接口创建并自动启动多台ECS实例。详情请参见[RunInstances](/cn.zh-CN/API参考/实例/RunInstances.md)。

**说明：** 调用RunInstances会创建ECS实例等计费资源，会产生实际费用。如果您只需测试示例代码，可以代码中设置DryRun方法，只发送检查请求，不会创建实例。检查项包括是否填写了必需参数、请求格式、业务限制和ECS库存等。

## 代码示例

以下代码适用于公网带宽采用按流量计费、实例计费方式采用按量付费、网络类型采用专有网络VPC的新建ECS实例：

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.alibaba.fastjson.JSON;
import java.util.*;
import java.util.UUID;
import com.aliyuncs.ecs.model.v20140526.*;

public class RunInstances {

    public static void main(String[] args) {
        // 创建并初始化DefaultAcsClient实例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<yourAccessKeyId>", "<yourAccessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建API请求，并设置参数。
        RunInstancesRequest request = new RunInstancesRequest();
        request.setRegionId("cn-hangzhou");
        request.setImageId("freebsd_11_02_64_30G_alibase_20190722.vhd");
        request.setInstanceType("ecs.g5.large");
        request.setSecurityGroupId("sg-bp1fg655nh68xyz9i***");
        request.setVSwitchId("vsw-bp1wt4qpuavdb6y6k8***");
        request.setInstanceName("MyFirstEcsInstance");
        request.setDescription("MyFirstEcsInstance");
        request.setInternetMaxBandwidthOut(2);
        request.setInternetChargeType("PayByTraffic");
        request.setClientToken(UUID.randomUUID().toString());

        // 添加一块数据盘，数据盘类型为SSD云盘，容量为100GiB，并开启了随ECS实例释放。
        List<RunInstancesRequest.DataDisk> dataDiskList = new ArrayList<RunInstancesRequest.DataDisk>();

        RunInstancesRequest.DataDisk dataDisk1 = new RunInstancesRequest.DataDisk();
        dataDisk1.setSize(100);
        dataDisk1.setCategory("cloud_ssd");
        dataDisk1.setDeleteWithInstance(true);
        dataDiskList.add(dataDisk1);
        request.setDataDisks(dataDiskList);
        // 批量创建五台ECS实例，如果不设置该参数，默认创建一台ECS实例。
        // request.setAmount(5);
        // 如果缺少库存可以接受的最低创建数量。
        // request.setMinAmount(2);

        List<RunInstancesRequest.Tag> tagList = new ArrayList<RunInstancesRequest.Tag>();

        RunInstancesRequest.Tag tag1 = new RunInstancesRequest.Tag();
        tag1.setKey("EcsProduct");
        tag1.setValue("DocumentationDemo");
        tagList.add(tag1);
        request.setTags(tagList);
        // 打开预检参数功能，不会实际创建ECS实例，只检查参数正确性、用户权限或者ECS库存等问题。
        // 实际情况下，设置了DryRun参数后，Amount必须为1，MinAmount必须为空，您可以根据实际需求修改代码。
        // request.setDryRun(true);
        request.setInstanceChargeType("PostPaid");

        // 发起请求并处理返回或异常。
        RunInstancesResponse response;
        try {
            response = client.getAcsResponse(request);

            System.out.println(JSON.toJSONString(response));

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

实际返回结果为：

```
{
    "RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368",
    "InstanceIdSets":{
        "InstanceIdSet":[
            "i-instanceid1",
            "i-instanceid2",
            "i-instanceid3"
        ]
    }
}
```

**相关文档**  


[RunInstances](/cn.zh-CN/API参考/实例/RunInstances.md)

[DescribeRegions](/cn.zh-CN/API参考/地域/DescribeRegions.md)

[DescribeImages](/cn.zh-CN/API参考/镜像/DescribeImages.md)

[DescribeInstanceTypes](/cn.zh-CN/API参考/实例/DescribeInstanceTypes.md)

[DescribeSecurityGroups](/cn.zh-CN/API参考/安全组/DescribeSecurityGroups.md)

[DescribeVSwitches](/cn.zh-CN/API参考/交换机/DescribeVSwitches.md)

