# Implement high availability by using Server Load Balancer {#concept_tvg_jjw_wdb .concept}

Server Load Balancer is a traffic distribution control service that distributes traffic to multiple backend ECS instances based on the forwarding policies.

## Scenarios {#section_mnt_qkw_wdb .section}

In the following scenarios, you can use Server Load Balancer to greatly improve high availability of ECS instances.

-   **High-traffic services**

    If traffic of an application is high, you can configure monitoring rules to distribute traffic to different ECS instances. In addition, you can use the session persistence function to forward requests from the same client to the same backend ECS instance to improve access efficiency.

-   **System extension**

    Based on the business development requirements, you can add or remove ECS instances at any time to extend the service capability of application systems and adapt to various Web servers and application servers. For more information, see [add backend servers](../../../../reseller.en-US/User Guide/Backend servers/Backend server overview.md#).

-   **Eliminate a single-point of failures**

    You can add multiple ECS instances behind a Server Load Balancer instance. When some ECS instances are faulty, Server Load Balancer automatically shields faulty ECS instances and distributes requests to healthy ECS instances, guaranteeing that the application systems can still work normally.

-   **Intra-city disaster tolerance \(multi-zone disaster tolerance\)**

    You can deploy the Server Load Balancer instances in a region with multiple zones to implement intra-city disaster tolerance. With this feature, when one data center fails, Server Load Balancer can quickly switch front-end traffic to other zones in the same region to restore the service capability.

    **Note:** If at least one ECS instance is added for each zone, the efficiency of Server Load Balancer is the highest in this deployment mode.

-   **Cross-region disaster tolerance**

    You can deploy the Server Load Balancer instances in different regions, and attach ECS instances of different zones in the corresponding regions. The upper layer uses Alibaba Cloud DNS as intelligent DNS, and resolves domain names to service addresses of Server Load Balancer instances in different regions, thus implementing global load balancing. When the system becomes unavailable in a region, you can temporarily stop DNS so that access of all users is not affected.


## Preparations {#section_unt_qkw_wdb .section}

Before using Server Load Balancer, make the following preparations.

-   **Plan regions where the Server Load Balancer instances are deployed**

    Alibaba Cloud provides Server Load Balancer for all the regions.

    **Note:** 

    -   To reduce the latency and increase the download speed, we recommend that you select the region closest to your customers.
    -   As Server Load Balancer does not support cross-region deployment, plan regions and select the same region as the backend ECS instance.
-   **Select the type \(public or private network\) of the Server Load Balancer instance**

    Determine the Server Load Balancer instance type based on your service type. After a Server Load Balancer instance is created, the system allocates a public or private IP address based on the type of the Server Load Balancer instance.

    -   Public network Server Load Balancer instances are only assigned public IP addresses. These Server Load Balancers are accessible over the Internet.
    -   Private network Server Load Balancer instances are only assigned private IP addresses. Server Load Balancer is accessible only over the Alibaba Cloud intranet, but not over the Internet. No fee is charged for private network Server Load Balancer instances.
-   Select listening protocols

    Server Load Balancer supports Layer-4 \(TCP and UDP\) and Layer-7 \(HTTP and HTTPS\) listening.

    -   During Layer-4 listening, requests are directly forwarded to the backend server and headers are not modified. After requests of clients arrive at the Server Load Balancer listener, the Server Load Balancer servers establish TCP connections with backend ECS instances through the backend ports configured for listening.
    -   In principle, Layer-7 listening is a way of implementing reverse proxy. After requests of clients arrive at the Server Load Balancer listener, the Server Load Balancer servers establish TCP connections with the backend ECS instances, namely to access the HTTP backend servers through the new TCP connections again instead of directly forwarding packets to the backend ECS instances.
    Compared with Layer-4 listening, Layer-7 listening requires an extra step of Tengine processing. Therefore, the performance of Layer-7 listening is not as good as that of Layer-4 listening. In addition, Layer-7 listening performance may be reduced by such factors as insufficient number of client ports and too many backend server connections. If high performance requirements are raised, Layer-4 listening is recommended.

-   **Prepare backend servers**

    Add ECS instances behind a Server Load Balancer instance to process requests forwarded by the front-end listener. Before creating a Server Load Balancer instance, create ECS instances and deploy related applications. When creating an ECS instance, note the following items:

    -   Region and zone of the ECS instance

        Make sure that the region of the ECS instance is the same as that of the Server Load Balancer instance. In addition, we recommend that you deploy ECS instances in different zones to improve the local availability.

    -   ECS configuration

        After deploying applications on the ECS instances, you do not have to perform special configuration. However, to configure a Layer-4 listener \(TCP or UDP\) for Linux ECS instances, make sure that the following parameters in the net.ipv4.conf file are set to 0:

        ```
        net.ipv4.conf.default.rp_filter = 0
        net.ipv4.conf.all.rp_filter = 0
        net.ipv4.conf.eth0.rp_filter = 0
        ```

    -   ECS instance deployment

        Now, no quota is set for backend ECS instances that can be configured for a Server Load Balancer instance. However, to guarantee stability and efficiency of your external services, we recommend that you add ECS instances of application servers that provide different services or perform different tasks to different Server Load Balancer instances based on service types or application modules.


## Procedure {#section_vny_jsw_wdb .section}

1.  Create ECS instances. You must have at least two ECS instances to use the Server Load Balancer service. For more information, see [create ECS instances](../../../../reseller.en-US/User Guide/Instances/Create an instance/Create an instance by using the wizard.md#).
2.  After the ECS instances are created, deploy related applications on the ECS instances. For more information, see [install static web pages](../../../../reseller.en-US/Quick Start (New Console)/Install static web pages.md#).
3.  Create a Server Load Balancer instance. A Server Load Balancer instance can be mapped to multiple listeners and backend servers. For more information, see [create an SLB instance](../../../../reseller.en-US/Quick Start (New Console)/Create an SLB instance.md#).
4.  After the Server Load Balancer instance is created, add at least one listener and one group of backend servers behind it. For more information, see [configure an SLB instance](../../../../reseller.en-US/Quick Start (New Console)/Configure an SLB instance.md#).

## Billing description {#section_h4t_qkw_wdb .section}

Server Load Balancer supports PayByTraffic. The specific charging items vary according to the instance type and performance type. For more information, see [pricing](https://partners-intl.aliyun.com/help/doc-detail/74811.htm).

