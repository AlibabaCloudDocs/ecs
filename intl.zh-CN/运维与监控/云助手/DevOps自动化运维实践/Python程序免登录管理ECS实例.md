---
keyword: [云助手, 远程命令, 运维插件, 阿里云, ecs]
---

# Python程序免登录管理ECS实例

云助手命令可以在多台ECS实例中批量执行Shell、Bat或者PowerShell脚本。相对于通过SSH或者RDP远程登录ECS实例进行运维操作，您可以使用云助手免登录直接为ECS实例进行运维操作。本文介绍在Python开发环境中使用云助手运维管理ECS实例。

-   目标ECS实例已安装云助手客户端。具体步骤，请参见[云助手客户端](/intl.zh-CN/运维与监控/云助手/配置云助手客户端/安装云助手客户端.md)。
-   已更新Python开发环境的SDK依赖aliyun-python-sdk-ecs至2.1.2或以上版本。更多详情，请前往[GitHub Repo Alibaba Cloud](https://develop.aliyun.com/tools/sdk)获取最新版本。

## 操作步骤

1.  根据ECS实例的配置，以及您需要执行的操作，编写Shell、Bat或者PowerShell命令。

    更多命令示例，请参见[查看实例系统配置](/intl.zh-CN/运维与监控/云助手/DevOps自动化运维实践/查看实例系统配置.md)和[修改实例配置与安装应用](/intl.zh-CN/运维与监控/云助手/DevOps自动化运维实践/修改实例配置与安装应用.md)。

2.  查询满足条件的ECS实例。

    ECS实例状态必须为**运行中**（`Running`）。查询实例的Python SDK示例请参见[查询ECS实例](/intl.zh-CN/SDK示例/Python示例/查询ECS实例.md)。

3.  获取账号的AccessKey，以及查询地域ID。

    具体步骤，请参见[地域和可用区]()和[创建AccessKey]()。

4.  为一台或多台ECS实例执行云助手命令。

    示例代码如下：

    ```
    # coding=utf-8
    # If the Python sdk is not installed, run 'sudo pip install aliyun-python-sdk-ecs'.
    # Make sure you're using the latest sdk version.
    # Run 'sudo pip install --upgrade aliyun-python-sdk-ecs' to upgrade.
    
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkecs.request.v20140526.RunCommandRequest import RunCommandRequest
    from aliyunsdkecs.request.v20140526.DescribeInvocationResultsRequest import DescribeInvocationResultsRequest
    import json
    import sys
    import base64
    import time
    import logging
    
    # Configure the log output formatter
    logging.basicConfig(level=logging.INFO,
                        format="%(asctime)s %(name)s [%(levelname)s]: %(message)s",
                        datefmt='%m-%d %H:%M')
    
    logger = logging.getLogger()
    
    access_key = '<yourAccessKey ID>'             # 设置您的AccessKey ID
    access_key_secret = '<yourAccessKey Secret>'  # 设置您的AccessKey Secret
    region_id = '<yourRegionId>'                  # 实例所属地域ID
    
    
    
    
    client = AcsClient(access_key, access_key_secret, region_id)
    
    def base64_decode(content, code='utf-8'):
        if sys.version_info.major == 2:
            return base64.b64decode(content)
        else:
            return base64.b64decode(content).decode(code)
    
    
    def get_invoke_result(invoke_id):
        request = DescribeInvocationResultsRequest()
        request.set_accept_format('json')
    
        request.set_InvokeId(invoke_id)
        response = client.do_action_with_exception(request)
        response_detail = json.loads(response)["Invocation"]["InvocationResults"]["InvocationResult"][0]
        status = response_detail.get("InvocationStatus","")
        output = base64_decode(response_detail.get("Output",""))
        return status,output
    
    
    def run_command(cmdtype,cmdcontent,instance_id,timeout=60):
        """
        cmdtype: 命令类型： RunBatScript;RunPowerShellScript;RunShellScript
        cmdcontent: 命令内容
        instance_id： 实例ID
        """
        try:
            request = RunCommandRequest()
            request.set_accept_format('json')
    
            request.set_Type(cmdtype)
            request.set_CommandContent(cmdcontent)
            request.set_InstanceIds([instance_id])
            # 执行命令的超时时间，单位s,默认是60s,请根据执行的实际命令来设置
            request.set_Timeout(timeout)
            response = client.do_action_with_exception(request)
            invoke_id = json.loads(response).get("InvokeId")
            return invoke_id
        except Exception as e:
            logger.error("run command failed")
    
    
    
    def wait_invoke_finshed_get_out(invoke_id,wait_count,wait_interval):
        for i in range(wait_count):
            status,output = get_invoke_result(invoke_id)
            if status not in ["Running","Pending","Stopping"]:
                return status,output
            time.sleep(wait_interval)
    
        logger.error("after wait %d times, still can not wait invoke-id %s finished")
        return "",""
    
    
    
    def run_task():
        # 设置云助手命令的命令类型
        cmdtype = "RunShellScript"
        # 设置云助手命令的命令内容
        cmdcontent = """
        #!/bin/bash
        yum check-update
        """
        # 设置超时时间
        timeout = 60
        # 设置您的实例ID
        ins_id = "i-wz9bsqk9pa0d2oge****" 
        # 执行命令
        invoke_id = run_command(cmdtype,cmdcontent,ins_id,timeout)
        logger.info("run command,invoke-id:%s" % invoke_id)
    
        # 等待命令执行完成,循环查询10次，每次间隔5秒，查询次数和间隔请根据实际情况配置
        status,output = wait_invoke_finshed_get_out(invoke_id,10,5)
        if status:
            logger.info("invoke-id execute finished,status: %s,output:%s" %(status,output))
    
    
    if __name__ == '__main__':
        run_task()
    ```


**相关文档**  


[CreateCommand](/intl.zh-CN/API参考/云助手/CreateCommand.md)

[InvokeCommand](/intl.zh-CN/API参考/云助手/InvokeCommand.md)

[DescribeInvocationResults](/intl.zh-CN/API参考/云助手/DescribeInvocationResults.md)

[DescribeCommands](/intl.zh-CN/API参考/云助手/DescribeCommands.md)

