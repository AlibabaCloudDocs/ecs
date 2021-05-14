# ECS安全组实践（二）

本文从授权和撤销安全组规则、加入和移出安全组讲解云服务器ECS的安全组最佳实践。

## 网络类型

阿里云的网络类型分为经典网络和专有网络VPC，对安全组支持不同的设置规则：

-   如果是经典网络，您可以设置内网入方向、内网出方向、公网入方向和公网出方向的安全组规则。
-   如果是专有网络VPC，您可以设置内网入方向和内网出方向的安全组规则。

安全组是区分网络类型的，一台经典网络类型的ECS实例只能加入经典网络的安全组。一台专有网络VPC类型的ECS实例只能加入本VPC的安全组。

## 安全组内网通讯的概念

本文开始之前，您应知道以下几个安全组内网通讯的概念：

-   默认只有同一个安全组的ECS实例可以网络互通。即使是同一个账户下的ECS实例，如果分属不同安全组，内网网络也是不通的。这个对于经典网络和专有网络VPC都适用。所以，经典网络类型的ECS实例也是内网安全的。
-   如果您有两台ECS实例，不在同一个安全组，您希望它们内网不互通，但实际上它们却内网互通，那么，您需要检查您的安全组内网规则设置。如果内网协议存在下面的协议，建议您重新设置。

    -   允许所有端口。
    -   授权对象为CIDR网段（SourceCidrIp）：0.0.0.0/0或者10.0.0.0/8的规则。
    **说明：** 如果是经典网络，上述协议会造成您的内网暴露给其它的访问。

-   如果您想实现在不同安全组的资源之间的网络互通，您应使用安全组方式授权。对于内网访问，您应使用源安全组授权，而不是CIDR网段授权。

## 安全组规则的属性

安全组规则主要是描述不同的访问权限，包括如下属性：

-   Policy：授权策略，参数值可以是accept（允许）或drop（拒绝）。
-   Priority：优先级，根据安全组规则的创建时间降序排序匹配。规则优先级可选范围为1~100，默认值为1，即最高优先级。数字越大，代表优先级越低。
-   NicType：网卡类型。如果只指定了SourceGroupId而没有指定SourceCidrIp，表示通过安全组方式授权，此时，NicType必须指定为intranet。
-   规则描述：
    -   IpProtocol：IP协议，取值：tcp、udp、icmp、gre或all。all表示所有的协议。
    -   PortRange：IP协议相关的端口号范围：
        -   IpProtocol取值为tcp或udp时，端口号取值范围为1~65535，格式必须是“起始端口号/终止端口号”，如“1/200”表示端口号范围为1~200。如果输入值为“200/1”，接口调用将报错。
        -   IpProtocol取值为icmp、gre或all时，端口号范围值为-1/-1，表示不限制端口。
    -   如果通过安全组授权，应指定SourceGroupId，即源安全组ID。此时，根据是否跨账号授权，您可以选择设置源安全组所属的账号SourceGroupOwnerAccount。
    -   如果通过CIDR授权，应指定SourceCidrIp，即源IP地址段，必须使用CIDR格式。

## 授权一条入网请求规则

在控制台或者通过API创建一个安全组时，入网方向默认deny all，即默认情况下您拒绝所有入网请求。这并不适用于所有的情况，所以您要适度地配置您的入网规则。

例如，如果您需要开启公网的80端口对外提供HTTP服务，因为是公网访问，您希望入网尽可能多访问，所以在IP网段上不应做限制，可以设置为0.0.0.0/0，具体设置可以参见以下描述，其中，括号外为控制台参数，括号内为OpenAPI参数，两者相同就不做区分。

-   网卡类型（NicType）：如果是经典网络，填写公网（internet）。如果是专有网络VPC，只需要填写内网（intranet），通过EIP实现公网访问。
-   授权策略（Policy）：允许（accept）。
-   规则方向：入方向。
-   协议类型（IpProtocol）：自定义TCP（tcp）。
-   端口范围（PortRange）：80/80。
-   授权对象（SourceCidrIp）：0.0.0.0/0。
-   优先级（Priority）：1。

**说明：** 上面的建议仅对公网有效。内网请求不建议使用CIDR网段，请参见[经典网络的内网安全组规则不要使用CIDR或者IP授权](#section_plq_zn2_2fb)。

## 禁止一个入网请求规则

禁止一条规则时，您只需要配置一条拒绝策略，并设置较低的优先级即可。这样，当有需要时，您可以配置其它高优先级的规则覆盖这条规则。例如，您可以采用以下设置拒绝6379端口被访问。

-   网卡类型（NicType）：内网（intranet）。
-   授权策略（Policy）：拒绝（drop）。
-   规则方向：入方向。
-   协议类型（IpProtocol）：自定义TCP（tcp）。
-   端口范围（PortRange）：6379/6379。
-   授权对象（SourceCidrIp）：0.0.0.0/0。
-   优先级（Priority）：100。

## 经典网络的内网安全组规则不要使用CIDR或者IP授权

对于经典网络类型的ECS实例，阿里云默认不开启任何内网的入规则。内网的授权一定要谨慎。

**说明：** 为了安全考虑，不建议开启任何基于CIDR网段的授权。

对于ECS实例来说，内网的IP经常变化，另外，这个IP的网段是没有规律的，所以，建议您通过安全组授权对经典网络内网的访问。

例如，您在安全组sg-redis上构建了一个redis的集群，为了只允许特定的机器（例如sg-web）访问这个redis的服务器编组，您不需要配置任何CIDR，只需要添加一条入规则：指定相关的安全组ID即可。

-   网卡类型（NicType）：内网（intranet）。
-   授权策略（Policy）：允许（accept）。
-   规则方向：入方向。
-   协议类型（IpProtocol）：自定义TCP（tcp）。
-   端口范围（PortRange）：6379/6379。
-   授权对象（SourceGroupId）：sg-web。
-   优先级（Priority）：1。

对于专有网络VPC类型的实例，如果您已经通过多个VSwitch规划好自己的IP范围，您可以使用CIDR设置作为安全组入规则。但是，如果您的专有网络VPC网段不够清晰，建议您优先考虑使用安全组作为入规则。

## 将需要互相通信的ECS实例加入同一个安全组

一个ECS实例最多可以加入5个安全组，而同一安全组内的ECS实例之间是网络互通的。如果您在规划时已经有多个安全组，而且，直接设置多个安全组规则过于复杂的话，您可以新建一个安全组，然后将需要内网通讯的ECS实例加入这个新的安全组。

这里也不建议您将所有的ECS实例都加入一个安全组，这将会使得您的安全组规则设置变的复杂。对于一个中大型应用来说，每个服务器编组的角色不同，合理地规划每个服务器的入方向请求和出方向请求是非常有必要的。

您可以在控制台上将一台实例加入安全组，具体操作，请参见[ECS实例加入安全组](/intl.zh-CN/安全/安全组/ECS实例加入安全组.md)。

如果您对阿里云的OpenAPI非常熟悉，您可以通过OpenAPI进行批量操作，具体操作，请参见[查询ECS实例](/intl.zh-CN/SDK示例/Python示例/查询ECS实例.md)。对应的Python代码片段如下：

```
def join_sg(sg_id, instance_id):
    request = JoinSecurityGroupRequest()
    request.set_InstanceId(instance_id)
    request.set_SecurityGroupId(sg_id)
    response = _send_request(request)
    return response
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
```

## 将ECS实例移出安全组

如果ECS实例加入不合适的安全组，将会允许本该拒绝的访问或者拒绝本该允许的访问，这时您可以选择将ECS实例从这个安全组中移出。但是在移出安全组之前必须保证您的ECS实例已经加入其它安全组。

**说明：** 将ECS实例从安全组移出，将会导致这台ECS实例和当前安全组内的网络不通，建议您在移出之前做好充分的测试。

对应的Python代码片段如下：

```
def leave_sg(sg_id, instance_id):
    request = LeaveSecurityGroupRequest()
    request.set_InstanceId(instance_id)
    request.set_SecurityGroupId(sg_id)
    response = _send_request(request)
    return response
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
```

## 定义合理的安全组名称和标签

合理的安全组名称和描述有助于您快速识别当前复杂的规则组合。您可以通过修改名称和描述来帮助自己识别安全组。

您也可以通过为安全组设置标签分组管理自己的安全组。您可以在控制台直接设置标签，具体操作请参见[设置标签](/intl.zh-CN/标签与资源/标签/创建或绑定标签.md)，也可以通过API设置标签。

## 删除不需要的安全组

安全组中的安全组规则类似于一条条白名单和黑名单。所以，请不要保留不需要的安全组，以免因为错误加入某台ECS实例而造成不必要的麻烦。

