# 创建ECS实例

本文以Python SDK为例，为您演示如何通过CreateInstance等阿里云API弹性地创建和管理ECS实例。

本文提供了创建ECS实例的完整代码示例，并提供了代码示例解析，详情请参见：

-   [创建按量付费ECS实例](#section_rhd_5un_xac)
-   [创建实例时自动检测并启动ECS实例](#section_zio_a8c_ukj)
-   [分配公网IP](#section_p1m_una_x1n)
-   [创建包年包月ECS实例](#section_688_w5k_tnj)

更多代码示例请参见[阿里云代码示例库（CodeSample）](https://developer.aliyun.com/codesample)。

## 完整代码

本文的完整代码如下所示，您可以自行根据实际情况修改和设置参数取值。

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 4.4.3, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
import time
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526.CreateInstanceRequest import CreateInstanceRequest
from aliyunsdkecs.request.v20140526.DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526.StartInstanceRequest import StartInstanceRequest
# configuration the log output formatter, if you want to save the output to file,
# append ",filename='ecs_invoke.log'" after datefmt.

logging.basicConfig(level=logging.INFO, format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s', datefmt='%a, %d %b %Y %H:%M:%S')

clt = client.AcsClient('<accessKeyId>', '<accessSecret>', '<region-Id>')
IMAGE_ID = 'ubuntu_18_04_64_20G_alibase_20190624.vhd'
INSTANCE_TYPE = 'ecs.g6.large'
SECURITY_GROUP_ID = 'sg-bp1i4c0xgqxadew2****'
INSTANCE_RUNNING = 'Running'
VSWITCH_ID = 'vsw-bp1ddbrxdlrcbim46****'

def create_instance_action():
    instance_id = create_after_pay_instance(IMAGE_ID, INSTANCE_TYPE, SECURITY_GROUP_ID, VSWITCH_ID)
    check_instance_running(instance_id)

# def create_prepay_instance_action():
#     instance_id = create_prepay_instance(IMAGE_ID, INSTANCE_TYPE, SECURITY_GROUP_ID, VSWITCH_ID)
#     check_instance_running(instance_id=instance_id)

# create one after pay ecs instance.
def create_after_pay_instance(image_id, instance_type, security_group_id, vsw_vswitch_id):
    request = CreateInstanceRequest()
    request.set_ImageId(image_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceType(instance_type)
    request.set_IoOptimized('optimized')
    request.set_VSwitchId(vsw_vswitch_id)
    request.set_SystemDiskCategory('cloud_ssd')
    response = _send_request(request)
    instance_id = response.get('InstanceId')
    logging.info("instance %s created task submit successfully.", instance_id)
    return instance_id

# create one prepay ecs instance.
def create_prepay_instance(image_id, instance_type, security_group_id, vsw_vswitch_id):
    request = CreateInstanceRequest()
    request.set_ImageId(image_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceType(instance_type)
    request.set_IoOptimized('optimized')
    request.set_VSwitchId(vsw_vswitch_id)
    request.set_SystemDiskCategory('cloud_ssd')
    request.set_Period(1)
    request.set_InstanceChargeType('PrePaid')
    response = _send_request(request)
    instance_id = response.get('InstanceId')
    logging.info("instance %s created task submit successfully.", instance_id)
    return instance_id

def check_instance_running(instance_id):
    detail = get_instance_detail_by_id(instance_id, INSTANCE_RUNNING)
    index = 0
    while detail is None and index < 60:
        detail = get_instance_detail_by_id(instance_id)
        time.sleep(10)
    if detail and detail.get('Status') == 'Stopped':
        logging.info("instance %s is stopped now.")
        start_instance(instance_id)
        logging.info("start instance %s job submit.")
    detail = get_instance_detail_by_id(instance_id, INSTANCE_RUNNING)
    while detail is None and index < 60:
        detail = get_instance_detail_by_id(instance_id, INSTANCE_RUNNING)
        time.sleep(10)
    logging.info("instance %s is running now.", instance_id)
    return instance_id

def start_instance(instance_id):
    request = StartInstanceRequest()
    request.set_InstanceId(instance_id)
    _send_request(request)

# output the instance owned in current region.
def get_instance_detail_by_id(instance_id, status='Stopped'):
    logging.info("Check instance %s status is %s", instance_id, status)
    request = DescribeInstancesRequest()
    request.set_InstanceIds(json.dumps([instance_id]))
    response = _send_request(request)
    instance_detail = None
    if response is not None:
        instance_list = response.get('Instances').get('Instance')
        for item in instance_list:
            if item.get('Status') == status:
                instance_detail = item
                break
        return instance_detail

# send open api request
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
    logging.info("Create ECS by OpenApi!")
    create_instance_action()
    # create_prepay_instance_action()
```

## 创建按量付费ECS实例

前提条件：开通按量付费ECS资源时，您的阿里云账户余额（即现金余额）和代金券的总值不得小于100.00元人民币。您可以在[阿里云用户中心](https://usercenter2.aliyun.com/home)完成账号充值。

必选属性：

-   SecurityGroupId：安全组ID。安全组相当于虚拟防火墙，通过安全组规则控制和保护实例的网络出入请求。建议按需开放和设置安全组出入规则时，不要默认开放所有的出入规则。更多详情，请参见[CreateSecurityGroup](/cn.zh-CN/API参考/安全组/CreateSecurityGroup.md)。
-   InstanceType：实例规格。例如，选择2核8GiB g6.large则入参为ecs.g6.large。更多详情，请参见[实例规格族汇总](/cn.zh-CN/实例/实例规格族.md)。
-   ImageId：镜像ID。您可以使用公共镜像或者自定义镜像。更多详情，请参见[DescribeImages](/cn.zh-CN/API参考/镜像/DescribeImages.md)。
-   VSwitchId：交换机ID。创建一台VPC类型的ECS实例需要指定交换机ID。更多详情，请参见[DescribeVSwitches](/cn.zh-CN/API参考/交换机/DescribeVSwitches.md)。

1.  创建ECS实例。

    如以下代码所示，创建一台VPC类型的ECS实例，使用SSD云盘做系统盘，对应参数值为cloud\_ssd，选择I/O优化实例则传入optimized属性。CreateInstance还提供了其他请求参数，如何调整，请参见[CreateInstance](/cn.zh-CN/API参考/实例/CreateInstance.md)。

    ```
    # create one after pay ecs instance.
    def create_after_pay_instance(image_id, instance_type, security_group_id, vsw_vswitch_id):
        request = CreateInstanceRequest()
        request.set_ImageId(image_id)
        request.set_SecurityGroupId(security_group_id)
        request.set_InstanceType(instance_type)
        request.set_IoOptimized('optimized')
        request.set_VSwitchId(vsw_vswitch_id)
        request.set_SystemDiskCategory('cloud_ssd')
        response = _send_request(request)
        instance_id = response.get('InstanceId')
        logging.info("instance %s created task submit successfully.", instance_id)
        return instance_id
    ```

2.  查询ECS实例状态。

    有关ECS实例的状态信息，请参见[实例生命周期介绍](/cn.zh-CN/实例/实例生命周期介绍.md)。其中：

    -   仅Stopped状态的实例可以执行StartInstance操作。
    -   仅Running状态的实例可以执行StopInstance操作。
    查询ECS实例状态可以通过实例ID（InstanceId）过滤。在DescribeInstances请求中通过传入JSON数组格式的String参数来查询实例状态，详情请参见[DescribeInstances](/cn.zh-CN/API参考/实例/DescribeInstances.md)。以下代码会检查实例的状态，并返回相应的实例信息：

    ```
    # output the instance owned in current region.
    def get_instance_detail_by_id(instance_id, status='Stopped'):
        logging.info("Check instance %s status is %s", instance_id, status)
        request = DescribeInstancesRequest()
        request.set_InstanceIds(json.dumps([instance_id]))
        response = _send_request(request)
        instance_detail = None
        if response is not None:
            instance_list = response.get('Instances').get('Instance')
            for item in instance_list:
                if item.get('Status') == status:
                    instance_detail = item
                    break
            return instance_detail
    ```

3.  启动ECS实例。

    创建成功后的ECS实例默认状态为Stopped。如果需要实例进入Running状态，可以通过StartInstance完成，详情请参见[StartInstance](/cn.zh-CN/API参考/实例/StartInstance.md)。

    ```
    def start_instance(instance_id):
        request = StartInstanceRequest()
        request.set_InstanceId(instance_id)
        _send_request(request)
    ```

4.  停止ECS实例。

    如果需要运行中的实例进入Stopped状态，可以通过StopInstance完成，详情请参见[StopInstance](/cn.zh-CN/API参考/实例/StopInstance.md)。

    ```
    def stop_instance(instance_id):
        request = StopInstanceRequest()
        request.set_InstanceId(instance_id)
        _send_request(request)
    ```


## 创建实例时自动检测并启动ECS实例

ECS实例的启动和停止都是异步操作，您可以在脚本创建并同时检测ECS实例符合状态时执行相应操作。以下示例代码的逻辑是：

1.  得到实例ID后，自动检测实例是否处于Stopped的状态。
2.  如果是Stopped，发起StartInstance指令。
3.  等待ECS实例进入Running状态。

```
def check_instance_running(instance_id):
    detail = get_instance_detail_by_id(instance_id, INSTANCE_RUNNING)
    index = 0
    while detail is None and index < 60:
        detail = get_instance_detail_by_id(instance_id)
        time.sleep(10)
    if detail and detail.get('Status') == 'Stopped':
        logging.info("instance %s is stopped now.")
        start_instance(instance_id)
        logging.info("start instance %s job submit.")
    detail = get_instance_detail_by_id(instance_id, INSTANCE_RUNNING)
    while detail is None and index < 60:
        detail = get_instance_detail_by_id(instance_id, INSTANCE_RUNNING)
        time.sleep(10)
    logging.info("instance %s is running now.", instance_id)
    return instance_id
```

## 分配公网IP

如果在创建ECS实例的过程中，指定了公网带宽，若需要公网的访问权限请调用API来分配公网IP。更多详情，请参见[AllocatePublicIpAddress](/cn.zh-CN/API参考/网络/AllocatePublicIpAddress.md)。

## 创建包年包月ECS实例

前提条件：通过API创建包年包月ECS实例的流程与ECS控制台创建流程不同，API流程使用的是自动扣费的模式。请在创建ECS实例之前确保账号支付方式有足够的余额或者信用额度，在创建ECS实例时实行直接扣费。

与创建按量付费ECS实例相比，您需要指定计费方式和计费时长。以下示例的时长为一个月。

```
request.set_Period(1)
request.set_InstanceChargeType(‘PrePaid’)
```

创建包年包月实例的示例代码如下：

```
# create one prepay ecs instance.
def create_prepay_instance(image_id, instance_type, security_group_id, vsw_vswitch_id):
    request = CreateInstanceRequest()
    request.set_ImageId(image_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceType(instance_type)
    request.set_IoOptimized('optimized')
    request.set_VSwitchId(vsw_vswitch_id)
    request.set_SystemDiskCategory('cloud_ssd')
    request.set_Period(1)
    request.set_InstanceChargeType('PrePaid')
    response = _send_request(request)
    instance_id = response.get('InstanceId')
    logging.info("instance %s created task submit successfully.", instance_id)
    return instance_id
```

