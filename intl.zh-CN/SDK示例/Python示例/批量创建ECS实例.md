# 批量创建ECS实例

RunInstances批量创建实例接口可以帮助您一次创建多台ECS按量付费或包年包月实例来完成应用的开发和部署，方便实现弹性的资源创建。

调用API前，您需要先创建AccessKey。具体操作，请参见[创建AccessKey]()。

**说明：** 禁止使用阿里云账号AccessKey，因为阿里云账号AccessKey泄露会威胁您所有资源的安全。请使用RAM用户AccessKey进行操作，可有效降低AccessKey泄露的风险。

和CreateInstance接口相比，RunInstances接口有以下优点：

-   单次可以最多创建100台实例，避免重复调用。
-   实例创建之后，实例会自动变成Starting状态，然后变成Running状态，不需要您调用StartInstance的操作。
-   创建实例的时候指定了InternetMaxBandwidthOut，则自动为您分配公网IP，不需要您再调用分配IP的操作。
-   您也可以一次创建100台抢占式实例，充分满足您的弹性需求。
-   创建的参数保持和CreateInstance保持兼容，增加了Amount参数来设定创建的个数，以及AutoReleaseTime参数来设定自动释放时间，不需要您再额外设置自动释放时间。
-   创建返回一个InstanceIdSets会记录相关的InstanceIds，您只需要根据实例ID轮询实例状态即可。详情请参见[DescribeInstanceStatus](/intl.zh-CN/API参考/实例/DescribeInstanceStatus.md)。

本文提供了批量创建ECS实例的完整代码示例请参见[完整代码](#section_v50_4ex_kmq)，并提供了代码示例解析，请参见：

-   [批量创建实例](#Createinstances)
-   [批量创建实例并自动分配公网IP](#section_lsw_clk_kfb)
-   [批量创建实例并自动设置自动释放时间](#section_yxk_2lk_kfb)

## 安装ECS Python SDK

首先确保您已经具备Python的Runtime，本文中使用的Python版本为2.7+。

这里以Python为示例，其他SDK的版本大于4.4.3即可。

```
pip install aliyun-python-sdk-ecs
```

如果提示您没有权限，请切换sudo继续执行。

```
sudo pip install aliyun-python-sdk-ecs
```

本文使用的SDK版本为4.4.3， 如果您使用是旧版本的SDK，需要更新。

## 完整代码

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 4.4.3, you can use command 'pip show aliyun-python-sdk-ecs' to check

import json
import logging
import time
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526.DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526.RunInstancesRequest import RunInstancesRequest
logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S')

# 您的access key Id。
ak_id = "your-access-key-id"

# 您的access key secret。
ak_secret = "your-access-key-secret"

# 设置地域。
region_id = "cn-hangzhou"

clt = client.AcsClient(ak_id, ak_secret, region_id)

# 设置实例规格。
instance_type = "ecs.g6.large"

# 选择的交换机。
vswitch_id = "vsw-bp1ddbrxdlrcbim46****"

# 使用的镜像信息。
image_id = "<imageid>"

# 当前VPC类型的安全组。
security_group_id = "sg-bp1i4c0xgqxadew2****"

# 批量创建ECS实例的数量, 取值范围：1-100, 默认值：1。
amount = 2;

# 自动释放时间。使用UTC时间，格式为 yyyy-MM-ddTHH:mm:ssZ。最短释放时间为当前时间半小时之后；最长释放时间不能超过当前时间三年。
auto_release_time = "2020-04-17T18:20:00Z"

# 创建ECS实例并启动。
def create_multiple_instances():
    request = build_request()
    request.set_Amount(amount)
    _execute_request(request)

# 创建ECS实例并分配公网IP。
def create_multiple_instances_with_public_ip():
    request = build_request()
    request.set_Amount(amount)
    request.set_InternetMaxBandwidthOut(1)
    _execute_request(request)

# 创建ECS实例并设置自动释放时间。
def create_multiple_instances_with_auto_release_time():
    request = build_request()
    request.set_Amount(amount)
    request.set_AutoReleaseTime(auto_release_time)
    _execute_request(request)

def _execute_request(request):
    response = _send_request(request)
    if response.get('Code') is None:
        instance_ids = response.get('InstanceIdSets').get('InstanceIdSet')
        running_amount = 0
        while running_amount < amount:
            time.sleep(10)
            running_amount = check_instance_running(instance_ids)
    print("ecs instance %s is running", instance_ids)

def check_instance_running(instance_ids):
    request = DescribeInstancesRequest()
    request.set_InstanceIds(json.dumps(instance_ids))
    response = _send_request(request)
    if response.get('Code') is None:
        instances_list = response.get('Instances').get('Instance')
        running_count = 0
        for instance_detail in instances_list:
            if instance_detail.get('Status') == "Running":
                running_count += 1
        return running_count

def build_request():
    request = RunInstancesRequest()
    request.set_ImageId(image_id)
    request.set_VSwitchId(vswitch_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceName("Instance-Name")
    request.set_InstanceType(instance_type)
    return request

# 发送API请求
def _send_request(request):
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)

if __name__ == '__main__':
    print ("hello ecs batch create instance")
    # 创建ECS实例并启动。
    create_multiple_instances()
    # 创建绑定公网IP的ECS实例。
    # create_multiple_instances_with_public_ip()
    # 创建ECS实例并设置自动释放时间。
    # create_multiple_instances_with_auto_release_time()
```

## 批量创建实例

首先创建RunInstancesRequest的实例，然后填入相关需要的参数即可。

下面的例子创建了2台实例，并且添加了自动每隔10秒钟检查一次实例的运行状态。直到实例状态变成Running结束创建流程。

```
# 您的access key Id。
ak_id = "your-access-key-id"

# 您的access key secret。
ak_secret = "your-access-key-secret"

# 设置地域。
region_id = "cn-hangzhou"

clt = client.AcsClient(ak_id, ak_secret, region_id)

# 设置实例规格。
instance_type = "ecs.g6.large"

# 选择的交换机。
vswitch_id = "vsw-bp1ddbrxdlrcbim46****"

# 使用的镜像信息。
image_id = "<imageid>"

# 当前VPC类型的安全组。
security_group_id = "sg-bp1i4c0xgqxadew2****"

# 批量创建ECS实例的数量, 取值范围：1-100, 默认值：1。
amount = 2;

# 自动释放时间。使用UTC时间，格式为 yyyy-MM-ddTHH:mm:ssZ。最短释放时间为当前时间半小时之后；最长释放时间不能超过当前时间三年。
auto_release_time = "2020-04-17T18:20:00Z"

# 创建ECS实例并启动。
def create_multiple_instances():
    request = build_request()
    request.set_Amount(amount)
    _execute_request(request)

def _execute_request(request):
    response = _send_request(request)
    if response.get('Code') is None:
        instance_ids = response.get('InstanceIdSets').get('InstanceIdSet')
        running_amount = 0
        while running_amount < amount:
            time.sleep(10)
            running_amount = check_instance_running(instance_ids)
    print("ecs instance %s is running", instance_ids)

def check_instance_running(instance_ids):
    request = DescribeInstancesRequest()
    request.set_InstanceIds(json.dumps(instance_ids))
    response = _send_request(request)
    if response.get('Code') is None:
        instances_list = response.get('Instances').get('Instance')
        running_count = 0
        for instance_detail in instances_list:
            if instance_detail.get('Status') == "Running":
                running_count += 1
        return running_count

def build_request():
    request = RunInstancesRequest()
    request.set_ImageId(image_id)
    request.set_VSwitchId(vswitch_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceName("Instance-Name")
    request.set_InstanceType(instance_type)
    return request

# 发送API请求
def _send_request(request):
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)
```

## 批量创建实例并自动分配公网IP

相比批量创建实例的代码，只需要添加一行属性，指定公网的带宽即可。下面的例子中默认给实例都分配了1 M的按流量带宽。

```
# 创建ECS实例并分配公网IP。
def create_multiple_instances_with_public_ip():
    request = build_request()
    request.set_Amount(amount)
    request.set_InternetMaxBandwidthOut(1)
    _execute_request(request)
```

## 批量创建实例并自动设置自动释放时间

相比批量创建实例的代码，只需要添加一行属性，指定实例的自动释放时间即可。自动释放时间按照ISO8601标准表示，并需要使用UTC时间，格式为`yyyy-MM-ddTHH:mm:ssZ`。最短在当前时间之后半小时，最长不能超过当前时间起三年。详情请参见[时间格式](/intl.zh-CN/API参考/附录/时间格式.md)。

```
# 创建ECS实例并设置自动释放时间。
def create_multiple_instances_with_auto_release_time():
    request = build_request()
    request.set_Amount(amount)
    request.set_AutoReleaseTime(auto_release_time)
    _execute_request(request)
```

