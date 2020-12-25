---
keyword: [Cloud Assistant, remote command, O&M plug-in, Alibaba Cloud, ecs]
---

# Use Python to manage ECS instances without logging on to the instances

You can use Cloud Assistant to simultaneously run a command on multiple ECS instances at a time. The command can be a shell, batch, or PowerShell command. Different from SSH or RDP, Cloud Assistant allows you to perform O&M operations on ECS instances in Phython.

-   The Cloud Assistant client is installed on the ECS instances. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).
-   The aliyun-python-sdk-ecs SDK dependency in Python is updated to V2.1.2 or later. For the latest version of ECS SDK for Python, visit [GitHub Repo Alibaba Cloud](https://develop.aliyun.com/tools/sdk).

## Procedure

1.  Compile the shell, batch, or PowerShell command based on the instance configurations and the operations that you want to perform.

    For more information about example commands, see [View instance configurations](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/View instance configurations.md) and [Modify instance configurations and install applications](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Modify instance configurations and install applications.md).

2.  Find the instances that meet the specified requirements.

    The instances must be in the **Running** \(`Running`\) state. For examples of how to use ECS SDK for Python to query instances, see [Query an ECS instance](/intl.en-US/SDK Reference/Python example/Query an ECS instance.md).

3.  Obtain the AccessKey pair of your account and query the region ID.

    For more information, see [Regions and zones]() and [Create an AccessKey]().

4.  Run a Cloud Assistant command on one or more ECS instances.

    Sample code:

    ```
    # coding=utf-8
    # If the Python sdk is not installed, run 'sudo pip install aliyun-python-sdk-ecs'.
    # Make sure you're using the latest sdk version.
    # Run 'sudo pip install --upgrade aliyun-python-sdk-ecs' to upgrade.
    
    import json
    import logging
    import os
    import time
    import datetime
    import base64
    from aliyunsdkcore import client
    from aliyunsdkecs.request.v20140526.CreateCommandRequest import CreateCommandRequest
    from aliyunsdkecs.request.v20140526.InvokeCommandRequest import InvokeCommandRequest
    from aliyunsdkecs.request.v20140526.DescribeInvocationResultsRequest import DescribeInvocationResultsRequest
    
    # Configure the log output formatter, if you want to save the output to file,
    # append ",filename='ecs_invoke.log'" after datefmt.
    
    logging.basicConfig(level=logging.INFO,
                        format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                        datefmt='%a, %d %b %Y %H:%M:%S',filename='aliyun_assist_openapi_test.log', filemode='w')
    #access_key = 'Your AccessKey ID'
    #access_key_secret = 'Your AccessKey secret'
    #region_name = 'cn-hangzhou'
    #zone_id = 'cn-hangzhou-f'
    
    access_key = 'LTAIXXXXXXXXXXXX'  # Enter your AccessKey ID.
    access_key_secret = '4dZXXXXXXXXXXXXXXXXXXXXXXXX'  # Enter your AccessKey secret.
    region_name = 'cn-hangzhou'  # Enter your region ID.
    zone_id = 'cn-hangzhou-f'  # Enter your zone ID.
    
    clt = client.AcsClient(access_key, access_key_secret, region_name)
    
    def create_command(command_content, type, name, description):
        request = CreateCommandRequest()
        request.set_CommandContent(command_content)
        request.set_Type(type)
        request.set_Name(name)
        request.set_Description(description)
        response = _send_request(request)
        if response is None:
            return None
        command_id = response.get('CommandId')
        return command_id;
    
    def invoke_command(instance_id, command_id, timed, cronat):
        request = InvokeCommandRequest()
        request.set_Timed(timed)
        InstanceIds = [instance_id]
        request.set_InstanceIds(InstanceIds)
        request.set_CommandId(command_id)
        request.set_Frequency(cronat)
        response = _send_request(request)
        invoke_id = response.get('InvokeId')
        return invoke_id;
    
    def get_task_output_by_id(instance_id, invoke_id):
        logging.info("Check instance %s invoke_id is %s", instance_id, invoke_id)
        request = DescribeInvocationResultsRequest()
        request.set_InstanceId(instance_id)
        request.set_InvokeId(invoke_id)
        response = _send_request(request)
        invoke_detail = None
        output = None
        if response is not None:
            result_list = response.get('Invocation').get('InvocationResults').get('InvocationResult')
            for item in result_list:
                invoke_detail = item
                output = base64.b64decode(item.get('Output'))
                break;
            return output;
    
    def execute_command(instance_id):
        command_str = 'yum check-update'
        command_id = create_command(base64.b64encode(command_str), 'RunShellScript', 'test', 'test')
        if(command_id is None):
            logging.info('create command failed')
            return
    
        invoke_id = invoke_command(instance_id, command_id, 'false', '')
        if(invoke_id is None):
            logging.info('invoke command failed')
            return
    
        time.sleep(15)
    
        output = get_task_output_by_id(instance_id, invoke_id)
        if(output is None):
            logging.info('get result failed')
            return
    
        logging.info("output: %s is \n", output)
    
    # Send API request.
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
        execute_command('i-bp17zhpbXXXXXXXXXXXXX')                
    ```


**References**  


[CreateCommand](/intl.en-US/API Reference/Cloud assistant/CreateCommand.md)

[InvokeCommand](/intl.en-US/API Reference/Cloud assistant/InvokeCommand.md)

[DescribeInvocationResults](/intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md)

[DescribeCommands](/intl.en-US/API Reference/Cloud assistant/DescribeCommands.md)

