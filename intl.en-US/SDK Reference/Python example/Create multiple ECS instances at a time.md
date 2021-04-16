# Create multiple ECS instances at a time

You can call RunInstances to create multiple pay-as-you-go or subscription ECS instances. This allows you to scale resources with ease to meet requirements of developing and deploying applications.

An AccessKey pair is created before you call the API operation. For more information about the procedure, see [Create an AccessKey pair]().

**Note:** Do not use the AccessKey pair of your Alibaba Cloud account. If the AccessKey pair is leaked, the security of all your resources is threatened. We recommend that you use the AccessKey pair of a RAM user to reduce the risk of leakage.

Compared with CreateInstance, RunInstances has the following benefits:

-   A maximum of 100 ECS instances can be created at a time.
-   After an ECS instance is created, the status of the instance automatically becomes Starting and then Running. You do not need to call the StartInstance operation.
-   If you specify InternetMaxBandwidthOut when you create an ECS instance, a public IP address is automatically assigned to the instance. You do not need to call an API operation to assign a public IP address to the instance.
-   You can create up to 100 preemptible instances at a time to meet your business requirements.
-   The parameters of RunInstances are compatible with those of CreateInstance. The Amount parameter is added to specify the number of ECS instances that you want to create. The AutoReleaseTime parameter is added to specify the automatic release time.
-   After ECS instances are created, InstanceIdSets that contains InstanceIds is returned. You can query the status of the instances based on their IDs. For more information, see [DescribeInstanceStatus](/intl.en-US/API Reference/Instances/DescribeInstanceStatus.md).

This topic provides the sample code to show how to create multiple ECS instances at a time. For more information, see [Sample code](#section_v50_4ex_kmq). This topic also provides the explanation of the sample code. For more information, see the following topics:

-   [Create multiple ECS instances at a time](#Createinstances)
-   [Create multiple ECS instances and assign public IP addresses](#section_lsw_clk_kfb)
-   [Create multiple ECS instances and set their automatic release time](#section_yxk_2lk_kfb)

## Install ECS SDK for Python

Ensure that you have prepared the runtime environment for Python. Python 2.7 or later is used in this topic.

SDK for Python 4.4.3 is used in this topic. If you are using an earlier version, update it.

```
pip install aliyun-python-sdk-ecs
```

If you are prompted that you do not have the permission, use the following sudo command to continue the installation:

```
sudo pip install aliyun-python-sdk-ecs
```

## Sample code

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

# Your AccessKey ID.
ak_id = "your-access-key-id"

# Your AccessKey secret.
ak_secret = "your-access-key-secret"

# The region ID of the ECS instances.
region_id = "cn-hangzhou"

clt = client.AcsClient(ak_id, ak_secret, region_id)

# The instance type.
instance_type = "ecs.g6.large"

# The ID of the selected VSwitch.
vswitch_id = "vsw-bp1ddbrxdlrcbim46****"

# The ID of the image that you use.
image_id = "<imageid>"

# The ID of the security group in the current VPC.
security_group_id = "sg-bp1i4c0xgqxadew2****"

# The number of ECS instances that you want to create. Valid values: 1 to 100. Default value: 1.
amount = 2;

# The automatic release time. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. The release time ranges from 30 minutes after the current time to three years later than the current time.
auto_release_time = "2020-04-17T18:20:00Z"

# Create and start ECS instances.
def create_multiple_instances():
    request = build_request()
    request.set_Amount(amount)
    _execute_request(request)

# Create ECS instances and assign public IP addresses.
def create_multiple_instances_with_public_ip():
    request = build_request()
    request.set_Amount(amount)
    request.set_InternetMaxBandwidthOut(1)
    _execute_request(request)

# Create ECS instances and set their automatic release time.
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

# Initiate an API request.
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
    # Create and start ECS instances.
    create_multiple_instances()
    # Create ECS instances and bind public IP addresses.
    # create_multiple_instances_with_public_ip()
    # Create ECS instances and set their automatic release time.
    # create_multiple_instances_with_auto_release_time()
```

## Create multiple ECS instances at a time

You can specify the required parameters to create multiple ECS instances at a time.

In the following example, two ECS instances are created. The status of the instances is automatically checked every 10 seconds. The creation is completed after the ECS instances enter the Running state.

```
# Your AccessKey ID.
ak_id = "your-access-key-id"

# Your AccessKey secret.
ak_secret = "your-access-key-secret"

# The region ID of the ECS instances.
region_id = "cn-hangzhou"

clt = client.AcsClient(ak_id, ak_secret, region_id)

# The instance type.
instance_type = "ecs.g6.large"

# The ID of the selected VSwitch.
vswitch_id = "vsw-bp1ddbrxdlrcbim46****"

# The ID of the image that you use.
image_id = "<imageid>"

# The ID of the security group in the current VPC.
security_group_id = "sg-bp1i4c0xgqxadew2****"

# The number of ECS instances that you want to create. Valid values: 1 to 100. Default value: 1.
amount = 2;

# The automatic release time. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. The earliest release time is 30 minutes after the current time. The latest release time cannot be three years later than the current time.
auto_release_time = "2020-04-17T18:20:00Z"

# Create and start ECS instances.
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

# Initiate an API request.
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

## Create multiple ECS instances and assign public IP addresses

You can specify the public bandwidth when you create multiple ECS instances. In the following example, the instances are assigned with a bandwidth of 1 Mbit/s:

```
# Create ECS instances and assign public IP addresses.
def create_multiple_instances_with_public_ip():
    request = build_request()
    request.set_Amount(amount)
    request.set_InternetMaxBandwidthOut(1)
    _execute_request(request)
```

## Create multiple ECS instances and set their automatic release time

You can specify the automatic release time when you create multiple ECS instances. Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC. The release time ranges from 30 minutes after the current time to three years later than the current time. For more information, see [ISO 8601 Time Format](/intl.en-US/API Reference/Appendix/ISO 8601 Time Format.md).

```
# Create ECS instances and set their automatic release time.
def create_multiple_instances_with_auto_release_time():
    request = build_request()
    request.set_Amount(amount)
    request.set_AutoReleaseTime(auto_release_time)
    _execute_request(request)
```

