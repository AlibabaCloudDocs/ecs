# Best practices for ECS security groups \(part 2\)

This topic describes the best practices on how to add a security group rule, cancel a security group rule, add ECS instances to a security group, and remove ECS instances from a security group.

## Network types

Alibaba Cloud provides two types of networks: classic network and virtual private cloud \(VPC\). These network types support different security group rules.

-   For the classic network, you can configure inbound rules for internal network traffic, outbound rules for internal network traffic, inbound rules for Internet traffic, and outbound rules for Internet traffic.
-   For VPCs, you can configure inbound and outbound rules for internal network traffic.

Different security groups may have different network types. Classic network-type ECS instances can be added only to classic network-type security groups. VPC-type ECS instances can be added only to security groups in the VPCs where the instances are located.

## Basic knowledge of internal network communication between security groups

Before you begin, you must learn about the following items about internal network communication between security groups:

-   By default, only the ECS instances in the same security group can access each other. The instances in different security groups of the same account are inaccessible to each other over the internal network. This applies to both the classic network and VPCs. Therefore, the classic network-type ECS instances are secure over the internal network.
-   If you have two ECS instances in different security groups and the instances are not inaccessible to each other over the internal network as you expected, you must check the internal network rules of your security groups. If an internal network rule meets one of the following conditions, we recommend that you reconfigure the rule:
    -   Traffic on all ports is allowed.
    -   The authorization object is specified in the form of CIDR block when the SourceCidrIp parameter is set to 0.0.0.0/0 or 10.0.0.0/8. For classic network-type security groups, the preceding internal network rule allows external resources to access the security group.
-   If you want to allow resources in different security groups to communicate with each other, you must configure security group rules to allow mutual access between the security groups. To allow access over the internal network, you must specify security groups as authorization objects, instead of CIDR blocks.

## Attributes of security rules

Security rules describe access permissions by using the following attributes:

-   Policy: the access control policy. Valid value: accept and drop.
-   Priority: the priority. Security group rules are assigned priorities in descending order based on the time when the rules are created. The priority of a security rule ranges from 1 to 100. The default value is 1, which indicates the highest priority. A greater value indicates a lower priority.
-   NicType: the network type. If you specify a security group as an authorization object by setting SourceGroupId instead of SourceCidrIp, you must set NicType to intranet.
-   Description:
    -   IpProtocol: the IP protocol. Valid values: tcp, udp, icmp, gre, and all. A value of all indicates all protocols.
    -   PortRange: the port range that corresponds to the IP protocol.
        -   If the value of IpProtocol is tcp or udp, the valid port numbers are 1 to 65535. You can specify a port range in the format of <start port number\>/<end port number\>. For example, 1/200 indicates that the port range is 1-200. If the value is 200/1, an error is reported when the API operation is called.
        -   If the value of IpProtocol is icmp, gre, or all, the port range is -1/-1, which indicates all ports.
    -   To control access from a security group, you must set SourceGroupId to the ID of the security group. In this case, you can choose to or not to configure SourceGroupOwnerAccount based on whether the rule is to control access between security groups across accounts. SourceGroupOwnerAccount specifies the account to which the source security group belongs.
    -   To control access from specific IP addresses, you must set the SourceCidrIp parameter to the IP addresses in CIDR notation.

## Create a rule to allow inbound requests

When you create a security group by using the console or by calling an API operation, a default rule is added to the security group to deny all inbound requests. If the default rule is not suitable, configure inbound rules on your own.

For example, if you want to enable port 80 which is connected to the Internet and then use the port to provide HTTP services externally, do not impose limits on CIDR blocks but set SourceCidrIp to 0.0.0.0/0 to allow inbound requests. Configure the following parameters to create an inbound rule to allow all inbound requests. The parameters and values outside the brackets are used in the ECS console, whereas, the parameters and values inside the brackets are used in ECS API operations.

-   NIC Type \(NicType\): Public \(internet\). If the security group is of the VPC type, NIC Type is automatically set to Internal \(intranet\). The security group can be accessed by other security groups over elastic IP addresses \(EIPs\).
-   Action \(Policy\): Allow \(accept\).
-   Rule Direction: Inbound \(inbound\).
-   Protocol Type \(IpProtocol\): Custom TCP \(tcp\).
-   Port Range \(PortRange\): 80/80.
-   Authorized Object \(SourceCidrIp\): 0.0.0.0/0.
-   Priority \(Priority\): 1.

**Note:** The preceding values are applicable to security group rules for Internet traffic. For security group rules for internal network traffic, we recommend that you do not use CIDR blocks as authorization objects. For more information, see the [Create an internal network rule for a security group rule to allow internal network communication](#section_plq_zn2_2fb) section in this topic.

## Create a rule to deny inbound requests

To deny inbound requests, you need only to configure a Deny policy that has a low priority. Then, you can configure another rule that has a higher priority to take precedence over this rule if necessary. For example, you can configure the following parameters to create a rule that denies access over port 6379.

-   NIC Type \(NicType\): Internal \(intranet\).
-   Action \(Policy\): Forbid \(drop\).
-   Rule Direction: Inbound \(inbound\).
-   Protocol Type \(IpProtocol\): Custom TCP \(tcp\).
-   Port Range \(PortRange\): 6379/6379.
-   Authorized Object \(SourceCidrIp\): 0.0.0.0/0.
-   Priority \(Priority\): 100.

## Create an internal network rule for a security group rule to allow internal network communication

By default, no inbound rules for internal network traffic are enabled for classic network-type ECS instances. Exercise caution for internal network authorization.

**Note:** For security reasons, we recommend that you do not enable authorization based on CIDR blocks.

For ECS instances, internal IP addresses frequently change and the CIDR blocks to which these IP addresses belong vary. For this reason, we recommend that you allow access to classic network-type ECS instances over the internal network by creating security group rules instead of specifying CIDR blocks.

For example, if you build a Redis cluster in the sg-redis security group and want to permit only specific computers such as those in the sg-web security group to access the servers in the Redis clusters, you need only to create a security group rule that specifies the ID of the source security group, instead of CIDR blocks, as the authorization object.

-   NIC Type \(NicType\): Internal \(intranet\).
-   Action \(Policy\): Allow \(accept\).
-   Rule Direction: Inbound \(inbound\).
-   Protocol Type \(IpProtocol\): Custom TCP \(tcp\).
-   Port Range \(PortRange\): 6379/6379.
-   Authorized Object \(SourceGroupId\): sg-web.
-   Priority \(Priority\): 1.

For VPC-type instances, if you planned an IP address range by using multiple vSwitches, you can use the CIDR blocks in inbound security group rules. However, if your VPC CIDR blocks are not clear, we recommend that you prioritize security groups over CIDR blocks as authorization objects when you configure inbound rules.

## Add ECS instances that require mutual access to the same security group

You can add an ECS instance to up to five security groups. ECS instances in the same security group can communicate with each other over the internal network. If you have multiple security groups but do not want to configure multiple security group rules, you can create a new security group and add the instances that have the requirement for internal network communication to the new security group.

However, we recommend that you do not add all ECS instances to the same security group because this makes the configuration of security group rules messy. For a large or medium-sized application, each server group is assigned a different role. We recommend that you configure appropriate inbound and outbound rules for each server group.

In the ECS console, you can add an ECS instance to a security group by following the instructions in [Add an ECS instance to a security group](/intl.en-US/Security/Security groups/Add an ECS instance to a security group.md).

If you are familiar with Alibaba Cloud OpenAPI, you can use OpenAPI to add multiple instances at the same time. For more information, see [Query an ECS instance](/intl.en-US/SDK Reference/Python example/Query an ECS instance.md). The following Python snippet shows how to add multiple ECS instances to a security group at the same time.

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

## Remove an ECS instance from a security group

If an ECS instance is added to an inappropriate security group, your services may be exposed or blocked. In this case, you can remove the ECS instance from the security group. Before you remove an ECS instance from a security group, make sure that the ECS instance also belongs to another security group.

**Note:** After an ECS instance is removed from a security group, this instance and other instances in the security group cannot access each other. We recommend that you perform sufficient tests before you remove the instance.

The following Python snippet shows how to remove an ECS instance from a security group.

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

## Define appropriate names and tags for security groups

Appropriate names and descriptions can help you identify the meanings of complicated rule combinations. You can change names and descriptions of security groups.

You can configure tags for security groups. Then, you can group and manage security groups by using tags. You can configure tags by using the ECS console or by calling API operations. For more information, see [Create or bind a tag](/intl.en-US/Tag & Resource/Tags/Create or bind a tag.md).

## Delete security groups that are no longer needed

Security group rules of security groups serve as whitelists and blacklists. We recommend that you delete security groups that are no longer needed to avoid issues that may occur if you add an ECS instance to an inappropriate security group.

