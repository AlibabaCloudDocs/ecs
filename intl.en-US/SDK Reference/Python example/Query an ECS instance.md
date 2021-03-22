# Query an ECS instance

You can manage an ECS instance by using the ECS console or by calling API operations. Alibaba Cloud provides SDKs in multiple languages to encapsulate APIs. This topic describes how to use an API operation to query an ECS instance in Python.

For more information about the sample code used to query an ECS instance, see [Sample code](#section_pxa_ljn_dg5). For more information about the parse of the sample code, see the following topics:

-   [Query the list of regions supported by the current account](#section_jdo_nr8_xi4)
-   [Query ECS instances in a specific region](#section_ryw_4wu_d4a)

## Create a RAM user and obtain its AccessKey pair

An AccessKey pair that consists of an AccessKey ID and an AccessKey secret is required if you want to use API operations to manage an ECS instance. To ensure the security of cloud services, you must create a RAM user, generate an AccessKey pair for the RAM user, and authorize the RAM user to manage ECS instances by using APIs.

Perform the following operations to create a RAM user and obtain its AccessKey pair:

1.  Create a RAM user. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md).

2.  Obtain the AccessKey pair of the RAM user. For more information, see [Create an AccessKey pair]().

3.  Grant the RAM user **full access to ECS** by attaching the `AliyunECSFullAccess` policy. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md).


## Install ECS SDK for Python

Make sure that you have prepared the runtime environment for Python. Python 2.7 or later is used in this topic.

Run the following command to install SDK for Python:

```
pip install aliyun-python-sdk-ecs
```

If you are prompted that you do not have the permissions, run the following sudo command to continue the installation:

```
sudo pip install aliyun-python-sdk-ecs
```

SDK for Python 2.1.2 is used in this topic.

## Sample code

The following content is the sample code. You can modify the code and change the values of parameters based on your actual needs.

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is greater than 2.1.2, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526.DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526.DescribeRegionsRequest import DescribeRegionsRequest
# configuration the log output formatter, if you want to save the output to file,
# append ",filename='ecs_invoke.log'" after datefmt.

logging.basicConfig(level=logging.INFO, format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s', datefmt='%a %d %b %Y %H:%M:%S')
clt = client.AcsClient('<accessKeyId>', '<accessSecret>', '<region-Id>')

# sample api to list aliyun open api.
def hello_aliyun_regions():
    request = DescribeRegionsRequest()
    response = _send_request(request)
    if response is not None:
        region_list = response.get('Regions').get('Region')
        assert response is not None
        assert region_list is not None
        result = map(_print_region_id, region_list)
        logging.info("region list: %s", list(result))

# output the instance owned in current region.
def list_instances():
    request = DescribeInstancesRequest()
    response = _send_request(request)
    if response is not None:
        instance_list = response.get('Instances').get('Instance')
        result = map(_print_instance_id, instance_list)
        logging.info("current region include instance %s", list(result))

def _print_instance_id(item):
    instance_id = item.get('InstanceId')
    return instance_id

def _print_region_id(item):
    region_id = item.get("RegionId")
    return region_id

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
    logging.info("Hello Aliyun OpenApi!")
    hello_aliyun_regions()
    list_instances()
```

## Query the list of regions supported by the current account

Create a file named hello\_ecs\_api.py. Before you use SDK for Python, use the Alibaba Cloud AccessKey ID and AccessKey secret of the RAM user to instantiate an AcsClient object.

**Note:** The AccessKey ID and AccessKey secret allow the RAM user to access ECS API of Alibaba Cloud with full permissions. You must keep the AccessKey pair confidential.

```
import json
import logging
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526.DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526.DescribeRegionsRequest import DescribeRegionsRequest
logging.basicConfig(level=logging.INFO, format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s', datefmt='%a %d %b %Y %H:%M:%S')
clt = client.AcsClient('<accessKeyId>', '<accessSecret>', '<region-Id>')
```

Query the list of regions that are supported by your current account after the AcsClient object is instantiated. For more information, see [DescribeRegions](/intl.en-US/API Reference/Regions/DescribeRegions.md).

```
def hello_aliyun_regions():
    request = DescribeRegionsRequest()
    response = _send_request(request)
    region_list = response.get('Regions').get('Region')
    assert response is not None
    assert region_list is not None
    result = map(_print_region_id, region_list)
    logging.info("region list: %s", list(result))
def _print_region_id(item):
    region_id = item.get("RegionId")
    return region_id
def _send_request(request):
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)
hello_aliyun_regions()
```

Run `python hello_ecs_api.py` on the command line to obtain the list of regions that are supported by the current account. The following example shows a command output:

```
region list: ['cn-qingdao', 'cn-beijing', 'cn-zhangjiakou', 'cn-huhehaote', 'cn-wulanchabu', 'cn-hangzhou', 'cn-shanghai', 'cn-shenzhen', 'cn-heyuan', 'cn-guangzhou', 'cn-chengdu', 'cn-hongkong', 'ap-northeast-1', 'ap-southeast-1', 'ap-southeast-2', 'ap-southeast-3', 'ap-southeast-5', 'ap-south-1', 'us-east-1', 'us-west-1', 'eu-west-1']
```

## Query ECS instances in a specific region

The process of querying the instance list is similar to that of querying the region list. You must replace the input parameter with DescribeInstancesRequest and configure relevant variables. For more information, see [DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md).

```
def list_instances():
    request = DescribeInstancesRequest()
    response = _send_request(request)
    if response is not None:
        instance_list = response.get('Instances').get('Instance')
        result = map(_print_instance_id, instance_list)
        logging.info("current region include instance %s", list(result))
def _print_instance_id(item):
    instance_id = item.get('InstanceId')
    return instance_id
def _send_request(request):
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)
list_instances()
```

The following example shows a command output:

```
current region include instance ['i-bp165p6xk2tmdhj0****', 'i-bp1a01zbqmsun5odo****'']
```

For more information about API operations for resource query, see [List of API operations by function](/intl.en-US/API Reference/List of API operations by function.md). For example, to query the list of disks, you can call the [DescribeDisks](/intl.en-US/API Reference/Disk/DescribeDisks.md) operation by replacing the input parameter with DescribeDisksRequest and configuring relevant variables.

