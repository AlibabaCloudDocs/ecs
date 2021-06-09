---
keyword: [purchase an instance, enterprise-level instance, GPU-accelerated instance, ECS bare metal instance, Super Computing Cluster, SCC, preemptible instance, reserved instance, connect to an instance, upgrade or downgrade the configurations of an instance, manage an instance, instance security, use Linux instances, instance limits, users inside mainland China purchasing ECS instance resources from outside mainland China, instance billing]
---

# Instance FAQ

This topic provides answers to frequently asked questions about Elastic Compute Service \(ECS\) instances.

-   FAQ about purchasing instances
    -   [How do I check which instance resources are available for purchase in a specific region or zone?](#section_dxe_iha_q0o)
    -   [What do I do if resources are sold out when I attempt to purchase an instance within a specific region or zone?](#section_lxw_bwz_qgb)
    -   [How do I select an instance type that is suitable for my business?](#section_j8t_fwz_mjf)
    -   [How long does it take to create an ECS instance?](#section_ska_yf3_rvx)
    -   [I paid for an ECS instance but no ECS instance was created. Why?](#section_gbw_acs_xwn)
-   FAQ about enterprise-level instances
    -   [What are enterprise-level instances? What are shared instances?](#section_2p8_osd_e5y)
    -   [What are the differences between enterprise-level and shared instances?](#section_cm4_dks_zu1)
    -   [Which instance families are enterprise-level instance families? Which instance families are shared instance families?](#section_y0w_qjj_s3o)
    -   [In what business scenarios do I need to purchase enterprise-level instances?](#section_8gs_zby_36p)
    -   [How is the network performance of enterprise-level instances?](#section_omt_o32_8lt)
    -   [Which disk categories do enterprise-level instances support?](#section_9st_mh4_j3f)
    -   [Which image types do enterprise-level instances support?](#section_h1y_jjt_aer)
    -   [What are the limits on changing the instance types of enterprise-level instances?](#section_rxb_abg_ub7)
    -   [Can I change a shared instance into an enterprise-level instance?](#section_90e_qq9_gmf)
-   FAQ about persistent memory optimized instances
    -   [What characteristics do persistent memory optimized instances have?](#section_rdv_89z_ile)
    -   [What requirements do persistent memory optimized instances have for operating systems?](#section_x40_ira_gbs)
    -   [After I purchase a persistent memory optimized instance, how do I configure its persistent memory as memory?](#section_npj_8f8_af1)
    -   [When persistent memory is used as memory on a persistent memory optimized instance, can I deploy and run Redis applications on the instance?](#section_6pv_zvt_cae)
    -   [I already have a Redis cluster based on regular memory and want to migrate business from this cluster to persistent memory optimized instances. How do I do this? What items do I need to take note of?](#section_nrq_5r7_5mj)
    -   [Can I deploy and run a parameter server \(PS\) architecture on persistent memory optimized instances where persistent memory is used as memory?](#section_cwc_6hc_uoy)
    -   [After I purchase a persistent memory optimized instance, how do I configure its persistent memory as local SSDs?](#section_ccq_ku3_xvg)
    -   [To which applications are local SSDs that can deliver higher performance applicable?](#section_6n2_u99_wgd)
    -   [Can I deploy Redis or MySQL applications on persistent memory optimized instances where persistent memory is used as local SSDs? Do I need to modify the applications in the same way as I do when persistent memory is used as memory?](#section_36t_778_s97)
    -   [How is the performance of persistent memory used as local SSDs, compared with local NVMe SSDs and cloud disks?](#section_j6s_772_zml)
    -   [How reliable is persistent memory?](#section_j6f_n0c_e49)
-   FAQ about GPU-accelerated instances
    -   [After the NVIDIA driver was installed, nvidia-smi did not work and an error message was returned indicating that the NVIDIA driver had not been installed. Why?](#section_6fo_f6k_wy9)
    -   [Why does Windows Graphics not support DirectX-based features?](#section_5mx_en9_guy)
    -   [Do GPU-accelerated instances support Android emulators?](#section_vwn_31g_4fn)
    -   [Can I change the configurations of GPU-accelerated instances?](#section_sbj_dzq_gb1)
    -   [Do pay-as-you-go GPU-accelerated instances support the No Fees for Stopped Instances \(VPC-Connected\) feature?](#section_pw6_mpa_a0f)
    -   [How do I view GPU monitoring data?](#section_lv4_gwl_r5e)
-   FAQ about ECS Bare Metal Instances
    -   [What are the differences between ECS bare metal instances, traditional cloud hosts \(virtual machines\), and traditional physical machines?](#section_m7m_pvm_64b)
    -   [How is the network performance of ECS bare metal instances?](#section_mtz_x6v_4v4)
    -   [Which disk categories do ECS bare metal instances support? How many data disks can be attached to a single ECS bare metal instance?](#section_gu1_xmv_r8f)
    -   [Can ECS bare metal instances have their configurations upgraded or downgraded? Do they support failover?](#section_qzc_rb4_og4)
-   FAQ about Super Computing Cluster \(SCC\)
    -   [How do I create an SCC instance?](#section_9as_2qf_ted)
    -   [How am I billed for SCC instances?](#section_lew_64d_19y)
    -   [How do I create an SCC by using E-HPC?](#section_pq2_wpe_y7q)
    -   [How do I use SCC RDMA?](#section_i2x_rle_0ql)
-   FAQ about preemptible instances
    -   [I do not have overdue payments within my account. Why have my preemptible instances been released?](#section_0ns_pj7_dxg)
    -   [Am I notified when my preemptible instances are about to be released? How am I notified?](#section_b3n_69r_ccj)
    -   [Can the data of a preemptible instance be automatically retained when the instance is released?](#section_hqu_m54_1ac)
    -   [Can I cancel or reschedule the automatic release of a preemptible instance?](#section_4dz_4mk_utb)
    -   [Can preemptible instances be converted into subscription instances?](#section_4bx_hwo_gre)
    -   [To what resources are the prices of preemptible instances applicable?](#section_ns2_1jv_mbr)
    -   [How do I bid for a preemptible instance?](#section_vv0_a6s_5zd)
    -   [What is the relationship between the user-defined maximum hourly price and the spot price of a preemptible instance?](#section_67i_s25_aqc)
    -   [Am I charged the same price for all preemptible instances started at the same time?](#section_y3x_sk2_stu)
    -   [For the first hour after a preemptible instance is created, am I charged at a price that fluctuates with the spot price?](#section_scn_g76_t1n)
    -   [Can I view the spot price of an instance type when I purchase a preemptible instance?](#section_jxg_3ko_6xo)
    -   [Can I view the historical prices of a preemptible instance type? How?](#section_z9a_do7_ofi)
    -   [Do I continue to be billed for preemptible instances after they are stopped?](#section_8yt_11m_q7i)
    -   [How many preemptible instances can be purchased within a single account?](#section_d2v_giu_8a4)
    -   [How do I increase my vCPU-based quotas?](#section_u2j_bsw_7vd)
    -   [Can the instance type of a preemptible instance be changed?](#section_yae_a2y_k7c)
    -   [Which instance families support preemptible instances?](#section_8ws_4pm_9cc)
    -   [In which regions can I create preemptible instances?](#section_0zt_ehb_pts)
    -   [When I attempt to purchase an ECS instance, the Preemptible Instance option is unavailable on the instance buy page. Why?](#section_skn_5ct_zya)
    -   FAQ about preemptible instances without a protection period
        -   [Which is more cost-effective: a preemptible instance with a protection period or a preemptible instance without a protection period?](#section_8ph_ned_xbq)
        -   [Is the release rate of preemptible instances without a protection period higher than that of preemptible instances with a protection period?](#section_su1_6fg_q9h)
        -   [Are preemptible instances without a protection period prioritized for release over those with a protection period?](#section_ut8_cn4_od6)
        -   [If I have created a preemptible instance without a protection period, do subsequently created preemptible instances also not have a protection period?](#section_le8_fur_3cx)
        -   [Am I notified 5 minutes before a preemptible instance is released even if it does not have a protection period?](#section_sdq_k1m_i7w)
        -   [Are fewer resources provided for preemptible instances with a protection period than for those without a protection period?](#section_npx_jel_rj2)
        -   [Can I convert between preemptible instances with and without a protection period?](#section_0c7_5a0_glg)
-   FAQ about reserved instances
    -   [What are reserved instances?](#section_et2_64u_fmh)
    -   [Does a reserved instance provide a resource reservation?](#section_5g6_eu4_b0f)
    -   [What operating systems do reserved instances support?](#section_xoy_vzx_szv)
    -   [Which instance families do reserved instances support?](#section_j7h_12a_tuy)
    -   [Can reserved instances be applied to preemptible instances?](#section_m9r_qk6_39q)
    -   [Can the instance families of reserved instances be changed?](#section_uee_304_jt3)
    -   [To what scenarios are zonal reserved instances applicable?](#section_wcp_t5l_01b)
    -   [To what scenarios are regional reserved instances applicable?](#section_rym_4rw_cl5)
    -   [How is the zone flexibility of reserved instances applied?](#section_6vd_nvw_m73)
    -   [How is the instance size flexibility of reserved instances applied?](#section_i9g_3my_drv)
    -   [Do zonal reserved instances provide instance size flexibility?](#section_tpd_tx9_9ri)
    -   [Do zonal reserved instances provide zone flexibility?](#section_qdz_h5b_f91)
    -   [Can a zonal reserved instance be changed into a regional one?](#section_wry_8lc_jj4)
    -   [Can the scope of a reserved instance be changed from one region to another?](#section_m89_45m_v6k)
    -   [Can reserved instances be used across accounts?](#section_6ta_i2c_mga)
    -   [Can reserved instances be used to offset the storage and network bills of pay-as-you-go instances?](#section_prg_o9w_0de)
    -   [Can I configure a reserved instance to be applied to a specified pay-as-you-go instance?](#section_30a_ovt_uhz)
    -   [How am I billed for reserved instances?](#section_whe_bza_0u2)
    -   [When does a reserved instance take effect after it is purchased?](#section_cdy_tt0_n68)
    -   [After I modify, split, or merge a reserved instance, when does the operation take effect?](#section_kfw_q23_shl)
    -   [Why is the No Upfront payment option not displayed on the buy page?](#section_95a_y2p_hcl)
    -   [Can the payment option of a reserved instance be changed?](#section_1ps_ydr_o6o)
    -   [Can reserved instances be resold?](#section_j9e_1zq_35v)
    -   [Can I use reserved instances to offset the images bills of pay-as-you-go Windows instances?](#section_0w6_6mr_z27)
    -   [Can reserved instances be used to offset the image bills of pay-as-you-go Linux instances?](#section_wm8_tf8_rgx)
    -   [Are the consumption details of reserved instances refreshed every hour?](#section_q23_b4t_odg)
    -   [Can a reserved instance be applied to more than one pay-as-you-go instance at the same time?](#section_10f_gpz_w86)
-   FAQ about connecting to instances
    -   Virtual Network Computing \(VNC\)
        -   [Does a VNC management terminal allow multiple users to log on simultaneously?](#section_mdm_w4q_wgb)
        -   [What do I do if I forget the remote connection password?](#section_tym_x4q_wgb)
        -   [Why am I unable to connect to a VNC management terminal even after I reset my remote connection password?](#section_huk_e8x_b38)
        -   [I was prompted with an authentication failure when I attempted to connect to a VNC management terminal. What do I do?](#section_xl9_o6y_79k)
        -   [What do I do if a black screen appears while I am connected to a VNC management terminal?](#section_xrm_6sm_10m)
        -   [What do I do if a VNC management terminal cannot be accessed?](#section_65w_3px_xpu)
        -   [Why am I unable to use Internet Explorer 8 to access a VNC management terminal?](#section_82j_21b_xj0)
        -   [When I use Firefox to access a VNC management terminal, an error message is returned indicating that the secure connection has failed. What do I do?](#section_l6t_kik_vmy)
        -   [How do I remotely log on to a Linux instance?](#section_tkz_v77_wbf)
        -   [What are the default username and password for remote logon to the operating system of an ECS instance?](#section_u82_ecw_928)
        -   [How do I adjust the desktop resolution of a Windows instance?](#section_a4f_aqv_1fi)
        -   [Why do two cursors appear after I log on to a Windows instance by using VNC?](#section_jma_ml8_us3)
    -   FAQ about using third-party software
        -   [What do I do if I fail to deploy a Data Plane Development Kit \(DPDK\) application on an ECS instance?](#section_ybo_juh_0dk)
-   FAQ about upgrading and downgrading instances
    -   [Can I upgrade the instance types and other configurations of subscription instances?](#section_5ap_zkp_361)
    -   [Can I upgrade the instance types and other configurations of pay-as-you-go instances?](#section_472_rev_qvi)
    -   [How long does it take to upgrade the configurations of an instance?](#section_ju8_yai_0f9)
    -   [How is the fee for an instance configuration upgrade calculated?](#section_ckm_8hg_3uy)
    -   [Are my cloud service configurations affected if I upgrade the configurations of ECS instances?](#section_s9y_1yw_w5c)
    -   [How do I upgrade ECS resources?](#section_grz_gr2_rve)
    -   [I have upgraded the configurations of an instance but no changes have taken effect. Why?](#section_jsb_os8_bbb)
-   FAQ about managing instances
    -   [What do I do if I cannot access a website that runs on an ECS instance?](#section_ttr_ch3_ia1)
    -   [My ECS instance was stuck in the Starting state, and AliyunService was disabled or deleted. What do I do?](#section_3kd_bat_4p4)
    -   [How do I use f1 instances?](#section_ug1_lb2_d7l)
    -   [How do I upload files by using the FTP tool in macOS?](#section_39c_w47_rds)
    -   [How do I apply for an ICP filing for my domain name after I purchase an ECS instance?](#section_br4_f3k_1jw)
    -   [An ECS instance fails to load the kernel to start. What do I do?](#section_o58_xbc_j1a)
    -   [How do I change the logon password from within an instance?](#section_5dx_x72_cb8)
    -   [Why am I unable to add sound or video cards to ECS instances?](#section_lqe_uwn_har)
    -   [Can I transfer the unused time of an ECS instance to another ECS instance?](#section_nwm_uhx_s6y)
    -   [Do ECS instances provide databases by default?](#section_h97_kf4_xjp)
    -   [Can I build a database on an ECS instance?](#section_jli_u2y_g3m)
    -   [Do ECS instances support Oracle databases?](#section_j1b_acd_1f7)
    -   [Are public and private IP addresses independent? Can I specify or add IP addresses?](#section_dvt_enw_7gr)
    -   [Can load balancing be implemented for a single ECS instance?](#section_g6s_x91_9m2)
    -   [Can I change the region of an ECS instance?](#section_wm7_rby_mij)
    -   [Can I adjust the partition size of a purchased disk?](#section_nih_446_koq)
    -   [How do I view subscription ECS instances in all regions within my account?](#section_s5o_w6z_95z)
    -   [When can I forcibly stop an ECS instance? What are the consequences?](#section_nlp_9qg_6gq)
    -   [Why am I unable to reactivate my ECS instance?](#section_vk6_sjc_agd)
    -   [Why has an ECS instance with release protection enabled been automatically released from a scaling group?](#section_so8_gdz_2i5)
-   FAQ about instance security
    -   [What is the AliVulfix process in an ECS instance?](#section_4ek_d0m_191)
    -   [How do I protect ECS instances against attacks?](#section_t6g_7b5_165)
    -   [What security services does Alibaba Cloud provide?](#section_cxr_p7b_a9w)
-   FAQ about using Linux instances
    -   [I have already renewed an expired Linux instance but I am still unable to access the website hosted on it. What do I do?](#section_s8j_d1f_1u6)
    -   [How do I activate a Windows ECS instance in a VPC?](#section_d1i_rzd_0dd)
    -   [How do I query, partition, and format the disks of a Linux instance?](#section_csf_vvp_2z1)
    -   [How do I upload files to a Linux instance?](#section_861_wjj_km6)
    -   [How do I change the owner and owner group of directories and files on a Linux instance?](#section_kf0_kn1_74z)
    -   [How do I update the software repository for Linux instances?](#section_8jc_uw1_mjn)
-   FAQ about instance limits
    -   [What limits apply to the transfer and change of public IP addresses of ECS instances?](#section_y49_iww_fvq)
    -   [Can I access amazon.com from my ECS instance?](#section_q6i_bio_ba9)
    -   [Why am I unable to access a website hosted outside mainland China after I log on to my ECS instance?](#section_ags_ovh_bde)
    -   [I cannot purchase more pay-as-you-go instances. What do I do?](#section_xt4_ax4_x66)
    -   [How can I view the resource quota?](#section_0gj_n2c_pez)
-   FAQ about instance billing
    -   [Am I still charged for a pay-as-you-go instance after it is stopped either manually or due to an overdue payment?](#section_bll_9fl_9qs)
    -   [What do I do if an order cannot be placed to change the billing method of an instance from pay-as-you-go to subscription?](#section_ye3_pyk_bzl)
    -   [How long after an order is paid does it take to change the billing method of an instance from pay-as-you-go to subscription?](#section_07w_jp4_rlu)
    -   [What do I do if the billing method of an instance cannot be changed from pay-as-you-go to subscription?](#section_ulz_fn2_oxb)
    -   [When I change the billing method of an instance from pay-as-you-go to subscription, does the billing method for network usage of the instance also change?](#section_4lm_u5o_2my)
    -   [I have an unpaid order to change the billing method of an instance from pay-as-you-go to subscription. If I upgrade the configurations of the instance, is the order still valid?](#section_tih_umb_qaz)
    -   [What do I do if the billing method of an instance cannot be changed from subscription to pay-as-you-go?](#section_xqt_ua4_1cf)
    -   [When I attempt to change the billing method of a disk in an ECS instance, an error message is returned indicating that I have already changed the billing method three times. What does this mean?](#section_bxy_dkr_1f9)
    -   [Why am I unable to change a pay-as-you-go instance into a subscription one?](#section_vlz_58s_9es)
    -   [How do I view the expiration time of a subscription instance?](#section_8hf_t8x_5n3)

## How do I check which instance resources are available for purchase in a specific region or zone?

You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.

## What do I do if resources are sold out when I attempt to purchase an instance within a specific region or zone?

If the resources of a specific instance type are sold out when you attempt to purchase an instance of that instance type within a specific region or zone, take one of the following measures:

-   Select another region.
-   Select another zone.
-   Select another instance type.

If the resources that you want to purchase are still unavailable after you take all of the preceding measures, try again later. Instance resources are dynamic. When resources are insufficient, Alibaba Cloud replenishes them as soon as possible.

You can also use the arrival notice feature to receive notifications when resources become available.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2301359951/p48634.png)

## How do I select an instance type that is suitable for my business?

Consider the following factors when you select an instance type. For more information about how to select an instance type, see [Best practices for instance type selection](/intl.en-US/Best Practices/Best practices for instance type selection.md).

-   Your business needs
-   Your website type
-   The average number of page views per day on your website
-   The size of your homepage
-   The data capacity of your website

## How long does it take to create an ECS instance?

It takes a minute or two to create an ECS instance. After the instance is created:

-   For an ECS instance that runs a Linux operating system, you can connect to the instance without making any other configurations. For more information, see [Connect to an ECS instance]().
-   For an ECS instance that runs a Windows operating system, you must use the Sysprep tool to initialize the operating system. Do not restart the instance while the operating system is being initialized. After the operating system is initialized, you can connect to the instance. For more information, see [Connect to an ECS instance](). The amount of time required to initialize the operating system is determined by the type of the instance.
    -   For an I/O optimized instance that runs a Windows operating system, 2 to 3 minutes are required to initialize the operating system.
    -   For a non-I/O optimized instance that runs a Windows operating system, 10 minutes are required to initialize the operating system.

**Note:** If an error occurs while the instance is being created, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

## I paid for an ECS instance but no ECS instance was created. Why?

If resources within the specified zone are insufficient to create an instance of your selected instance type, the instance cannot be created. Your account is automatically refunded the cost of the instance. If you do not receive a refund within half an hour, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.

## What are enterprise-level instances? What are shared instances?

Enterprise-level instances belong to a series of instance families released by Alibaba Cloud in September 2016. Enterprise-level instances provide high performance, consistent computing power, and balanced network performance. Enterprise-level instances have exclusive and consistent computing, storage, and network resources, and are suitable for enterprise scenarios that require high business stability.

Shared instances belong to a series of instance families that are targeted at individuals or small and medium-sized websites. Shared instances share resources, in contrast with enterprise-level instances that each have their own resources exclusively. As a result, shared instances do not provide consistent computing performance, but cost less.

## What are the differences between enterprise-level and shared instances?

Enterprise-level instances use a CPU-bound scheduling scheme. Each vCPU is bound to a CPU hyperthread. Instances do not compete for CPU resources and do provide consistent computing performance as guaranteed in the service-level agreement \(SLA\).

Shared instances use a CPU-unbound scheduling scheme. Each vCPU is randomly allocated to an idle CPU hyperthread. vCPUs of different instances compete for CPU resources, which causes computing performance to fluctuate when traffic loads are heavy. Shared instances can guarantee only availability but cannot guarantee the performance that may be required in the SLA.

## Which instance families are enterprise-level instance families? Which instance families are shared instance families?

Among the [instance families](/intl.en-US/Instance/Instance families.md) that are available for purchase, t6, t5, s6, n4, mn4, xn4, and e4 are shared instance families, and the rest are enterprise-level instance families.

## In what business scenarios do I need to purchase enterprise-level instances?

For business scenarios to which different enterprise-level instances are applicable, see [Instance families](/intl.en-US/Instance/Instance families.md) and [Best practices for instance type selection](/intl.en-US/Best Practices/Best practices for instance type selection.md).

## How is the network performance of enterprise-level instances?

The network performance of enterprise-level instances depends on their specifications. The higher their specifications are, the higher network performance the instances can deliver. For more information about the network performance of different instance specifications, see [Instance families](/intl.en-US/Instance/Instance families.md).

## Which disk categories do enterprise-level instances support?

For the disk categories that enterprise-level instances support, see [Disk categories](/intl.en-US/Block Storage/Block Storage overview/Cloud disks.md).

## Which image types do enterprise-level instances support?

For the public images that enterprise-level instances support, see [Overview](/intl.en-US/Images/Public image/Overview.md).

You can also import custom images. For more information, see [Import custom images](/intl.en-US/Images/Custom image/Import images/Import custom images.md).

## What are the limits on changing the instance types of enterprise-level instances?

For the limits on changing the instance types of enterprise-level instances, see [Instance families that support instance type changes](/intl.en-US/Instance/Change configurations/Instance families that support instance type changes.md).

## Can I change a shared instance into an enterprise-level instance?

Yes, you can change a shared instance into an enterprise-level instance. For more information, see [Instance families that support instance type changes](/intl.en-US/Instance/Change configurations/Instance families that support instance type changes.md).

## What characteristics do persistent memory optimized instances have?

Persistent memory optimized instances use high-capacity persistent memory, and provide slower access and higher data durability than the instances that use regular memory do. When persistent memory optimized instances are stopped or restarted, data in their persistent memory is not lost. Persistent memory can be used as:

-   Memory: You can move some data from regular memory to persistent memory, such as non-hot data that does not require high-speed storage access. Persistent memory offers large capacity at a low price per GiB and can help reduce the total cost of ownership \(TCO\) per GiB of memory.
-   Local SSDs: Persistent memory can be used as ultra-high performance SSDs to offer a read/write latency as low as 400 nanoseconds. You can use persistent memory for core application databases that require consistent response time. You can also replace cache disks with persistent memory to achieve higher IOPS, higher bandwidth, and lower latency and improve the business performance of the entire cluster.

## What requirements do persistent memory optimized instances have for operating systems?

The following image versions can be used on persistent memory optimized instances:

-   Alibaba Cloud Linux 2
-   CentOS 7.6 or later
-   Ubuntu 18.10 or later
-   SUSE Linux 12 SP4 or later

Alibaba Cloud provides support for Alibaba Cloud Linux 2. Alibaba Cloud Linux 2 integrates tools for scenarios to which persistent memory is applicable to work out of the box. In some scenarios such as scenarios where Redis applications are used, Alibaba Cloud Linux 2 outperforms Linux community editions by 20%.

## After I purchase a persistent memory optimized instance, how do I configure its persistent memory as memory?

You can use tools to configure the persistent memory as memory. For more information, see [Configure the usage mode of persistent memory](/intl.en-US/Instance/Instance type families/Memory optimized instance families/Configure the usage mode of persistent memory.md).

## When persistent memory is used as memory on a persistent memory optimized instance, can I deploy and run Redis applications on the instance?

You can significantly reduce the TCO per GiB of memory for Redis applications by running them on persistent memory optimized instances. However, to ensure performance, we recommend that you modify the Redis applications by stratifying their data and storing the data in different places. You can store non-hot data in persistent memory and hot data in regular memory.

To reduce your modification costs, Alibaba Cloud provides re6p instance types for Redis applications. You can deploy Redis applications on instances of the re6p instance types by running several commands. For more information, see [Deploy Redis applications on re6p instances](/intl.en-US/Instance/Instance type families/Memory optimized instance families/Deploy Redis applications on re6p instances.md).

**Note:** When you purchase persistent memory optimized instances, select instance types named in the ecs.re6p-redis.<nx\>large format.

## I already have a Redis cluster based on regular memory and want to migrate business from this cluster to persistent memory optimized instances. How do I do this? What items do I need to take note of?

You must ensure business consistency and data reliability while you are migrating business from the Redis cluster to persistent memory optimized instances. We recommend that you first purchase a single persistent memory optimized instance and test it with a small amount of required business to check whether the basic performance and capacity model of the instance meet your business requirements. If the basic performance and capacity model of the instance meet your business requirements, you can scale out to more persistent memory optimized instances and take over business from the entire Redis cluster.

## Can I deploy and run a parameter server \(PS\) architecture on persistent memory optimized instances where persistent memory is used as memory?

Server nodes in a PS architecture store all training parameters of training clusters, traditionally in their memory. These parameters consume a large amount of memory and are expensive to store. When you run a PS architecture on persistent memory optimized instances where persistent memory is used as memory, we recommend that you store all parameters in persistent memory and only hash tables in regular memory. This way, the TCO of training clusters can be significantly reduced.

You can modify the applications to suit your business requirements,or [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm) to contact Alibaba Cloud for technical support.

## After I purchase a persistent memory optimized instance, how do I configure its persistent memory as local SSDs?

You can use tools to configure the persistent memory as local SSDs. For more information, see [Configure the usage mode of persistent memory](/intl.en-US/Instance/Instance type families/Memory optimized instance families/Configure the usage mode of persistent memory.md).

## To which applications are local SSDs that can deliver higher performance applicable?

To optimize performance or costs for I/O-intensive applications, you can select persistent memory optimized instances. You can use persistent memory optimized instances to solve common problems. Here are some of the problems:

-   The latency of single SQL queries is high or SQL queries require more consistent response time.
-   It takes too long to load resources on frontend servers of games, heavily loaded databases, and heavily loaded web servers.
-   You purchased large cloud disks or local disks for their high IOPS and bandwidth but now have unused capacity and unnecessary costs.

You can use persistent memory optimized instances in typical I/O-intensive scenarios such as:

-   Redis and other NoSQL databases such as Cassandra and MongoDB
-   Structured databases such as MySQL
-   I/O-intensive applications such as e-commerce, online games, and media applications
-   Elasticsearch
-   Live video streaming, instant messaging, and room-based online games that require persistent connections
-   High-performance relational databases and online transaction processing \(OLTP\) systems

## Can I deploy Redis or MySQL applications on persistent memory optimized instances where persistent memory is used as local SSDs? Do I need to modify the applications in the same way as I do when persistent memory is used as memory?

Yes, you can deploy Redis and MySQL applications on persistent memory optimized instances where persistent memory is used as local SSDs. You do not need to modify these applications before they can identify the persistent memory as standard SSDs.

## How is the performance of persistent memory used as local SSDs, compared with local NVMe SSDs and cloud disks?

The following table describes the performance comparison between local NVMe SSDs, enhanced SSDs \(ESSDs\), and persistent memory that is used as local SSDs.

**Note:** The performance levels \(PLs\) in the following table are only for reference. If you want to obtain details of a single test, the results of your own tests prevail.

|Item|Persistent memory of 128 GiB|NVMe SSD of 1,788 GiB|PL1 ESSD of 800 GiB|
|----|----------------------------|---------------------|-------------------|
|Read bandwidth|8-10 GB/s|2-3 GB/s|0.2-0.3 GB/s|
|Read/write bandwidth|8-10 GB/s|1-2 GB/s|0.2-0.3 GB/s|
|Write bandwidth|4-6 GB/s|1-2 GB/s|0.2-0.3 GB/s|
|Read IOPS|1,000,000|500,000|20,000-30,000|
|Read/write IOPS|1,000,000|300,000|20,000-30,000|
|Write IOPS|1,000,000|300,000|20,000-30,000|
|Read latency|300-400 nanoseconds|100,000 nanoseconds|250,000 nanoseconds|
|Write latency|300-400 nanoseconds|20,000 nanoseconds|150,000 nanoseconds|

You can perform the following steps to test the performance of the persistent memory when it is used as local SSDs:

1.  Configure persistent memory as local SSDs and attach the local SSDs to instances.

    For more information, see [Configure the usage mode of persistent memory](/intl.en-US/Instance/Instance type families/Memory optimized instance families/Configure the usage mode of persistent memory.md).

2.  Use disk performance test tools to test the performance of the local SSDs.

    For information about how to test disk performance by using fio in Linux systems, see the commands used in [Test the performance of Elastic Block Storage devices](/intl.en-US/Block Storage/Performance/Test the performance of Elastic Block Storage devices.md).


## How reliable is persistent memory?

The reliability of data stored in persistent memory depends on the reliability of persistent memory devices and the physical servers to which these devices are attached. This increases risks of single points of failure. To ensure the reliability of application data, we recommend that you implement data redundancy at the application layer and use cloud disks for long-term data storage.

When persistent memory optimized instances are released, data stored in their persistent memory is automatically cleared. We recommend that you back up data before you release the instances. It takes longer to release persistent memory optimized instances than to release other types of instances.

## After the NVIDIA driver was installed, nvidia-smi did not work and an error message was returned indicating that the NVIDIA driver had not been installed. Why?

Cause: The mismatch between the kernel and kernel-devel package versions resulted in a driver compilation error when the driver was installed from the .rpm file.

Solution: Check the kernel version and download the corresponding kernel-devel package version. Then, run the `rpm –qa | grep kernel` command on the instance to check whether the kernel-devel package version matches the kernel version. Make sure that they match and then install the driver again.

## Why does Windows Graphics not support DirectX-based features?

Problem description: On Windows instances where the installed GPU driver has taken effect, Windows Remote Desktop Protocol \(RDP\) may not support DirectX- or OpenGL-based applications.

Solution: Install the VNC service and client or use other protocols that support these applications, such as PC over IP \(PCoIP\) and XenDesktop HDX 3D.

## Do GPU-accelerated instances support Android emulators?

No, GPU-accelerated instances do not support Android emulators.

## Can I change the configurations of GPU-accelerated instances?

You cannot change the configurations of the following GPU-accelerated instances:

-   GPU-accelerated instances with local storage
-   vGPU-accelerated instances

For information about the GPU-accelerated instance families that support instance type changes, see [Instance families that support instance type changes](/intl.en-US/Instance/Change configurations/Instance families that support instance type changes.md).

## Do pay-as-you-go GPU-accelerated instances support the No Fees for Stopped Instances \(VPC-Connected\) feature?

Instance families such as gn5 that are equipped with local storage do not support the No Fees for Stopped Instances \(VPC-Connected\) feature. For more information, see [No Fees for Stopped Instances \(VPC-Connected\)](/intl.en-US/Pricing/Billing methods/No Fees for Stopped Instances (VPC-Connected).md).

## How do I view GPU monitoring data?

You can log on to the [CloudMonitor console](https://cloudmonitor.console.aliyun.com/) or call the [DescribeMetricList](/intl.en-US/API Reference/Cloud Products/DescribeMetricList.md) operation to view GPU monitoring data. For more information, see [GPU monitoring](/intl.en-US/Host monitoring/GPU monitoring.md).

## What are the differences between ECS bare metal instances, traditional cloud hosts \(virtual machines\), and traditional physical machines?

For information about the differences, see [Overview](/intl.en-US/Instance/Instance type families/ECS Bare Metal Instance types/Overview.md).

## How is the network performance of ECS bare metal instances?

The network performance of ECS bare metal instances depends on their specifications. The higher their specifications are, the higher network performance the instances can deliver. For more information about the network performance of different ECS bare metal instance specifications, see [Instance families](/intl.en-US/Instance/Instance families.md).

## Which disk categories do ECS bare metal instances support? How many data disks can be attached to a single ECS bare metal instance?

ECS bare metal instances support ultra disks, standard SSDs, and enhanced SSDs \(ESSDs\). Up to 16 data disks can be attached to a single ECS bare metal instance.

## Can ECS bare metal instances have their configurations upgraded or downgraded? Do they support failover?

ECS bare metal instances cannot have their configurations upgraded or downgraded. They do support failover. When the physical machine that hosts an ECS bare metal instance fails, the system fails the instance over to another physical machine. Data is retained in the data disks of the instance.

## How do I create an SCC instance?

You can create an SCC instance in one of the following ways:

-   If you only want to use the remote direct memory access \(RDMA\) feature, log on to the ECS console. Create an SCC instance as described in [Create an SCC instance](/intl.en-US/Instance/Instance type families/Super Computing Cluster instance type family/Create an SCC instance.md).
-   If you want to use the HPC scheduler and the cluster resizing service in addition to RDMA, log on to the [E-HPC console](https://ehpc.console.aliyun.com). Create an SCC and then create an SCC instance.

## How am I billed for SCC instances?

You are billed for SCC instances on a weekly, monthly, or yearly subscription basis.

## How do I create an SCC by using E-HPC?

You can log on to the [E-HPC console](https://ehpc.console.aliyun.com) or call the CreateCluster operation to create an SCC.

## How do I use SCC RDMA?

If you select an image that is customized for SCC and supports RDMA RoCE drivers and OFED stacks to create an SCC instance, you can use SCC RDMA by virtue of the IB verbs API or implement RDMA-based communication by using the MPI.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2301359951/p50536.png)

## I do not have overdue payments within my account. Why have my preemptible instances been released?

After the one-hour protection period of a preemptible instance expires, if the spot price \(the current price per hour of the preemptible instance\) exceeds the user-defined maximum hourly price or if resources are insufficient, the preemptible instance is automatically released.

## Am I notified when my preemptible instances are about to be released? How am I notified?

Yes, you are notified when your preemptible instances are about to be released. When your preemptible instance needs to be released due to a spot price change or insufficient resources, the instance first enters the To Be Released state and then is automatically released in 5 minutes.

You can use CloudMonitor to subscribe to notifications for interrupted preemptible instances. For more information, see [Set event notifications](/intl.en-US/Deployment & Maintenance/Event notifications/Set event notifications.md).

To check whether an instance is in the To Be Released state, you can view the [instance metadata](/intl.en-US/Instance/Manage instances/Manage instance metadata/Overview of ECS instance metadata.md), or call the [DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md) operation and view the returned OperationLocks data.

## Can the data of a preemptible instance be automatically retained when the instance is released?

No, the data of a preemptible instance cannot be automatically retained when the instance is released. When a preemptible instance is no longer needed, we recommend that you back up your data and environment by following the instructions in [Create a snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md) and then release the instance. You can purchase new preemptible instances at any time.

## Can I cancel or reschedule the automatic release of a preemptible instance?

Yes, you can cancel or reschedule the automatic release of your preemptible instance at any time.

## Can preemptible instances be converted into subscription instances?

No, preemptible instances cannot be converted into subscription instances.

## To what resources are the prices of preemptible instances applicable?

The prices of preemptible instances are applicable only to instance types. You are billed for other resources such as system disks, data disks, and network bandwidth at the same prices as those of pay-as-you-go instances.

## How do I bid for a preemptible instance?

To create a preemptible instance, you can specify a maximum hourly price to bid for an instance type. If the spot price does not exceed your specified maximum hourly price, the preemptible instance that you request is created, and you are billed based on the spot price. For more information, see [Create a preemptible instance](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Create a preemptible instance.md).

## What is the relationship between the user-defined maximum hourly price and the spot price of a preemptible instance?

If the spot price does not exceed the user-defined maximum hourly price, the preemptible instance is created, and you are billed based on the spot price. After a preemptible instance is created, it enters a protection period in which it cannot be automatically released due to insufficient resources or fluctuations in the spot price.

After the protection period expires, the system checks the spot price and resource availability of the instance type every 5 minutes. If the spot price exceeds the user-defined maximum hourly price or if resources of the instance type are insufficient, the preemptible instance that is in the Running state is released.

## Am I charged the same price for all preemptible instances started at the same time?

Yes, you are charged the same price for all preemptible instances started at the same time.

## For the first hour after a preemptible instance is created, am I charged at a price that fluctuates with the spot price?

No, the hourly price of the first instance hour for a preemptible instance is set at the start of the hour and remains in effect for the whole hour.

## Can I view the spot price of an instance type when I purchase a preemptible instance?

Yes, when you create a preemptible instance in the ECS console, you can view the spot price and historical prices of each selected instance type. The total instance price \(including the instance type, storage, and bandwidth fees\) is displayed in the lower part of the instance buy page. The instance type fee is the spot price of the selected instance type.

## Can I view the historical prices of a preemptible instance type? How?

Yes, you can select an instance type to view its historical prices when you attempt to create a preemptible instance in the ECS console. You can also call the [DescribeSpotPriceHistory](/intl.en-US/API Reference/Instances/DescribeSpotPriceHistory.md) operation to view the historical prices of a preemptible instance type.

## Do I continue to be billed for preemptible instances after they are stopped?

Yes, you continue to be billed after the preemptible instances are stopped. When a preemptible instance is no longer needed, we recommend that you back up your data and environment by following the instructions in [Create a snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md) and then release the instance. You can purchase new preemptible instances at any time.

**Note:** You continue to be billed for preemptible instances after you stop them by using the ECS console or by calling the StopInstance operation.

## How many preemptible instances can be purchased within a single account?

vCPU-based quotas apply to preemptible instances within each account, whereas instance count-based quotas do not. When you create a preemptible instance, you can view the available vCPU-based quota after you select an instance type. For more information, see the "Instance limits" section in [Limits](/intl.en-US/Product Introduction/Limits.mdsection_tbg_zdx_wdb).

## How do I increase my vCPU-based quotas?

To increase your vCPU-based quotas, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

## Can the instance type of a preemptible instance be changed?

No, the instance types of preemptible instances cannot be changed.

## Which instance families support preemptible instances?

Instance families that support the pay-as-you-go billing method also support preemptible instances. If a preemptible instance of a specific instance type cannot be created due to insufficient resources, try a different instance type.

## In which regions can I create preemptible instances?

Preemptible instances can be created within all Alibaba Cloud regions. If preemptible instances cannot be created within a specific region due to insufficient resources, try a different region.

## When I attempt to purchase an ECS instance, the Preemptible Instance option is unavailable on the instance buy page. Why?

Whether the Preemptible Instance option is available depends on your ECS usage.

## Which is more cost-effective: a preemptible instance with a protection period or a preemptible instance without a protection period?

Preemptible instances without a protection period are more cost-effective and have a discount of 10% off compared with preemptible instances with a protection period.

## Is the release rate of preemptible instances without a protection period higher than that of preemptible instances with a protection period?

You can check the release rate of each instance type on the instance buy page in the ECS console regardless of whether you attempt to create preemptible instances with or without a protection period. For each instance type, the release rate is determined by the bidding policy and the supply-demand relationships of resources.

![release-rate](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6554873061/p170286.png)

## Are preemptible instances without a protection period prioritized for release over those with a protection period?

No, preemptible instances without a protection period are not prioritized for release over those with a protection period.

## If I have created a preemptible instance without a protection period, do subsequently created preemptible instances also not have a protection period?

No, preemptible instances are created without a protection period only if you choose not to configure a protection period for them. By default, each preemptible instance is created with a protection period of one hour.

**Note:** The protection period of preemptible instances can be configured only when the instances are created by calling API operations. For more information, see the description of the SpotDuration parameter in [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) and [CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md).

## Am I notified 5 minutes before a preemptible instance is released even if it does not have a protection period?

Yes, you are notified 5 minutes before a preemptible instance is released even if it does not have a protection period.

## Are fewer resources provided for preemptible instances with a protection period than for those without a protection period?

No, the same amount of resources are provided for preemptible instances with and without a protection period.

## Can I convert between preemptible instances with and without a protection period?

No, you cannot convert between preemptible instances with and without a protection period. By default, each preemptible instance is created with a protection period of one hour. The protection period of preemptible instances can be configured only when the instances are created by calling API operations. The protection period settings of preemptible instances cannot be changed after the instances are created.

## What are reserved instances?

Reserved instances automatically match pay-as-you-go instances \(excluding preemptible instances\) within your account to provide a billing discount. Reserved instances can also be used to reserve instance resources. A combination of reserved instances and pay-as-you-go instances provides higher cost-effectiveness and a higher degree of flexibility as compared with subscription instances.

## Does a reserved instance provide a resource reservation?

Zonal reserved instances provide resource reservations, but regional reserved instances do not.

## What operating systems do reserved instances support?

Reserved instances support both Windows and Linux operating systems. For example, a reserved Linux instance can be applied to pay-as-you-go Linux instances that match its attributes regardless of the image type \(public images, custom images, shared images, or Alibaba Cloud Marketplace images\).

To apply a reserved instance to pay-as-you-go instances created from Bring Your Own License \(BYOL\) images, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

## Which instance families do reserved instances support?

Reserved instances support the following instance families:

-   General purpose instance families: g7, g6e, g6, g5, g5ne, and sn2ne
-   Compute optimized instance families: c7, c6e, c6, c5, ic5, and sn1ne
-   Memory optimized instance families: r7, r6e, r6, r5, re6, re4, and se1ne
-   Big data instance family: d2s
-   Instance families with local SSDs: i2 and i2g
-   Instance families with high clock speeds: hfc6, hfc5, hfg6, hfg5, and hfr6
-   GPU-accelerated compute optimized instance families: gn6i, gn6e, and gn6v
-   ECS Bare Metal Instance families: ebmc6, ebmg6, ebmr6, ebmhfc6, ebmhfg6, and ebmhfr6
-   Burstable instance families: t6 and t5

## Can reserved instances be applied to preemptible instances?

No, reserved instances cannot be applied to preemptible instances.

## Can the instance families of reserved instances be changed?

No, the instance families of reserved instances cannot be changed.

## To what scenarios are zonal reserved instances applicable?

We recommend that you purchase zonal reserved instances when you have clear requirements to reserve resources.

## To what scenarios are regional reserved instances applicable?

We recommend that you purchase regional reserved instances if you want to have a higher degree of zone flexibility or instance size flexibility.

## How is the zone flexibility of reserved instances applied?

Only regional reserved instances provide zone flexibility. Example:

You are running the following pay-as-you-go instance:

One ecs.c5.xlarge Linux instance in Qingdao Zone B. This instance is named C5PAYG-b.

You have purchased the following reserved instance:

One regional ecs.c5.xlarge reserved instance in the China \(Qingdao\) region. This instance is named C5RI.

C5RI is matched to C5PAYG-b.

You release C5PAYG-b and start another Linux instance of the same instance type named C5PAYG-c in Qingdao Zone C. C5RI is then matched to C5PAYG-c.

## How is the instance size flexibility of reserved instances applied?

Only regional reserved instances provide instance size flexibility. Example:

You have one regional ecs.g5.4xlarge reserved instance. It can be applied to one ecs.g5.4xlarge pay-as-you-go instance, two ecs.g5.2xlarge pay-as-you-go instances, or four ecs.g5.xlarge pay-as-you-go instances.

You have a one-year regional ecs.g5.xlarge reserved instance. It can be applied to offset the bills of an ecs.g5.xlarge pay-as-you-go instance or 50% of the bills of an ecs.g5.2xlarge pay-as-you-go instance by hour for one year.

## Do zonal reserved instances provide instance size flexibility?

No, zonal reserved instances do not provide instance size flexibility. A zonal reserved instance can be applied only to pay-as-you-go instances of the same instance type as it.

## Do zonal reserved instances provide zone flexibility?

No, zonal reserved instances do not provide zone flexibility. A zonal reserved instance can be applied only to pay-as-you-go instances in the same zone as it.

## Can a zonal reserved instance be changed into a regional one?

Yes, a zonal reserved instance can be changed into a regional one. You can change the scope of a reserved instance you purchased in the following ways:

-   From a zone to a region
-   From a region to a zone
-   From one zone to another within the same region for a zonal reserved instance

## Can the scope of a reserved instance be changed from one region to another?

No, the scope of a reserved instance cannot be changed from one region to another. For example, if you have a zonal reserved instance in Hangzhou Zone B, you can change the instance scope to another zone within the China \(Hangzhou\) region or change the instance into a regional reserved instance in the China \(Hangzhou\) region. However, you cannot change the scope of the zonal reserved instance to a zone of another region, or change the instance into a regional reserved instance in another region.

## Can reserved instances be used across accounts?

No, reserved instances cannot be used across accounts.

## Can reserved instances be used to offset the storage and network bills of pay-as-you-go instances?

No, reserved instances cannot be used to offset the storage and network bills of pay-as-you-go instances. Reserved instances can be used to offset the vCPU and memory bills of pay-as-you-go instances. For pay-as-you-go Windows instances, reserved instances can also be used to offset the image bills.

## Can I configure a reserved instance to be applied to a specified pay-as-you-go instance?

No, you cannot configure a reserved instance to be applied to a specified pay-as-you-go instance. When multiple pay-as-you-go instances match a reserved instance, the reserved instance is applied based on the optimized matching scheme.

## How am I billed for reserved instances?

You are separately billed for reserved instances. The All Upfront, Partial Upfront, and No Upfront payment options are supported.

The term of a reserved instance starts from when the instance is purchased. You are charged based on the payment option that you selected regardless of whether the reserved instance is matched to pay-as-you-go instances. The All Upfront option is most cost-effective.

## When does a reserved instance take effect after it is purchased?

A reserved instance takes effect and you are billed starting on the hour when the reserved instance is purchased. The reserved instance becomes invalid at 00:00:00 on the day after the reserved instance expires. For example, if you purchase a reserved instance with a term of one year at 13:45:00 on February 26, 2019, the reserved instance takes effect and you are billed starting from 13:00:00 on February 26, 2019. The reserved instance expires at 00:00:00 on February 27, 2020. If you already have eligible pay-as-you-go instances when you purchase a reserved instance, the reserved instance is applied to offset the bills generated by the pay-as-you-go instances starting from the hour of 13:00 to 14:00 on February 26, 2019 until the reserved instance expires.

## After I modify, split, or merge a reserved instance, when does the operation take effect?

When reserved instances are modified, split, or merged, new reserved instances are generated and the original ones become invalid. The new reserved instances take effect and the original ones become invalid. Both occur on the hours of the modification, splitting, or merging operations. You split one ecs.g5.2xlarge zonal reserved instance RI1 into two zonal ecs.g5.xlarge reserved instances RI2 and RI3 at 13:45:00 on February 26, 2019. At 13:00:00 on February 26, 2019, RI1 becomes invalid and RI2 and RI3 take effect. Starting from 13:00:00 on February 26, 2019, the instance type eligible for resource reservation and billing discounts is ecs.g5.xlarge, not ecs.g5.2xlarge any more. If RI2 and RI3 are matched to pay-as-you-go instances immediately after they take effect, RI2 and RI3 are also applied to offset the hourly bills of ecs.g5.xlarge pay-as-you-go instances starting from 13:00:00 on February 26, 2019.

## Why is the No Upfront payment option not displayed on the buy page?

The availability of this option depends on your ECS usage.

## Can the payment option of a reserved instance be changed?

No, the payment options of reserved instances cannot be changed.

## Can reserved instances be resold?

No, reserved instances cannot be resold.

## Can I use reserved instances to offset the images bills of pay-as-you-go Windows instances?

Yes, reserved instances can be used to offset the image bills of pay-as-you-go Windows instances. This is because reserved Windows instances already include Windows images at no additional cost.

## Can reserved instances be used to offset the image bills of pay-as-you-go Linux instances?

No, reserved instances cannot be used to offset the image bills of pay-as-you-go Linux instances.

## Are the consumption details of reserved instances refreshed every hour?

Yes, the consumption details of reserved instances are refreshed every hour.

## Can a reserved instance be applied to more than one pay-as-you-go instance at the same time?

Yes, a reserved instance can be applied to more than one pay-as-you-go instance at the same time. The reserved instance checks for eligible pay-as-you-go bills on an hourly basis and deducts fees based on its computing power.

**Note:** The computing power and term of each reserved instance are fixed. You cannot increase the computing power of a reserved instance by shortening its term.

You have a reserved instance with the following attributes:

-   c5.large instance type
-   Instances: 1 \(indicating that the reserved instance can match one pay-as-you-go instance of the specified instance type\)
-   One-year term

The following examples demonstrate how the reserved instance is applied based on the pay-as-you-go instances that exist:

-   Six c5.large pay-as-you-go instances exist for one hour each. Each of these pay-as-you-go instances consumes one hour of computing power equal to that delivered by the c5.large reserved instance every hour. The reserved instance is randomly applied to one of the pay-as-you-go instances. You cannot configure the reserved instance to be applied to all six pay-as-you-go instances by shortening the term of the reserved instance to two months.
-   Six c5.large pay-as-you-go instances exist for 10 minutes each. The six instances consume 10 minutes of computing power each and in total consume the amount of computing power that the c5.large reserved instance can deliver every hour. The reserved instance is applied to all six pay-as-you-go instances.
-   Six c5.large pay-as-you-go instances exist for 15 minutes each. The six instances consume 15 minutes of computing power each, in total exceeding the amount of computing power that the c5.large reserved instance can deliver every hour. The reserved instance is randomly applied to the pay-as-you-go instances to offset the charges for one hour of computing power.

## Does a VNC management terminal allow multiple users to log on simultaneously?

No, a VNC management terminal allows a single user to log on at a time.

## What do I do if I forget the remote connection password?

You can reset your remote connection password. For more information, see [Change the VNC password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

## Why am I unable to connect to a VNC management terminal even after I reset my remote connection password?

If the instance to which you are connecting is not I/O optimized, you must restart the instance by using the ECS console or by calling the RebootInstance operation for the new password to take effect.

**Note:** If you restart the instance from within the instance, the new password does not take effect.

## I was prompted with an authentication failure when I attempted to connect to a VNC management terminal. What do I do?

Authentication fails if the entered password is not correct. Perform the following troubleshooting operations:

1.  Enter the correct remote connection password.
2.  If you forget your password, you can reset it and try again. For more information, see [Change the VNC password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

    **Note:** If the instance to which you are connecting is not I/O optimized, you must restart the instance by using the ECS console or by calling the RebootInstance operation for the new password to take effect.


## What do I do if a black screen appears while I am connected to a VNC management terminal?

A black screen indicates that the instance is in sleep mode. Perform the following operations based on your operating system:

-   For a Linux instance, click your mouse or press any key to activate the instance.
-   For a Windows instance, you can choose **Send Remote Call** \> **CTRL+ALT+DELETE** in the upper-left corner to go to the logon interface.

## What do I do if a VNC management terminal cannot be accessed?

You can use a browser to access the VNC management terminal for troubleshooting. For example, use Google Chrome to access the VNC management terminal, and press the F12 key to open the developer tools panel. Then, click the **Console** tab and identify errors based on the information displayed.

## Why am I unable to use Internet Explorer 8 to access a VNC management terminal?

VNC management terminals support Internet Explorer 10 and later.

We recommend that you use Google Chrome because it is most compatible with the Alibaba Cloud Management Console.

## When I use Firefox to access a VNC management terminal, an error message is returned indicating that the secure connection has failed. What do I do?

This problem occurs if the encryption algorithm used by your version of Firefox is different from that used by the VNC management terminal.

We recommend that you use Google Chrome because it is most compatible with the Alibaba Cloud Management Console.

## How do I remotely log on to a Linux instance?

Linux instances support SSH for remote connection. You can use one of the following methods to remotely log on to a Linux instance:

-   [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).
-   [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).
-   [Connect to a Linux instance by using an SSH key pair](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using an SSH key pair.md).
-   [Connect to a Linux instance from a mobile device](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance from a mobile device.md).

## What are the default username and password for remote logon to the operating system of an ECS instance?

The default username varies by operating system.

-   For a Windows instance, the default username is `administrator`.
-   For a Linux instance, the default username is `root`.

The password for remote logon to the operating system of an instance is set by yourself when you create the instance. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md). If you forget the password, you can reset it. For more information, see [Reset the logon password of an instance](/intl.en-US/Instance/Manage instances/Reset the logon password of an instance.md).

**Note:** This password is used to remotely log on to the instance operating system, not to the VNC management terminal.

## How do I adjust the desktop resolution of a Windows instance?

You can use one of the following methods to adjust the desktop resolution of a Windows instance:

-   Connect to the instance by using a VNC management terminal and adjust the desktop resolution on the instance.

    The following example demonstrates how to adjust the desktop resolution of an instance that runs a `Windows Server 2019 Datacenter 64-bit` operating system:

    1.  Connect to the ECS instance by using a VNC management terminal in the ECS console. For more information, see [Connect to a Windows instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Windows instance by using password authentication.md).
    2.  On the Windows desktop, right-click a blank area and select **Display settings**.
    3.  In the **Scale and layout** section, adjust the resolution.
-   Use the Remote Desktop Connection \(RDC\) tool on your local computer.

    You cannot adjust the desktop resolution of a Windows instance after you connect to the instance from your local computer by using RDC. You must adjust the display settings in RDC on the local computer, and then connect to the instance by using RDC to apply the new display settings to the instance.

    ![windows](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2337034061/p175572.png)


## Why do two cursors appear after I log on to a Windows instance by using VNC?

If two cursors appear when you use VNC to log on to a Windows instance of the g7, c7, or r7 instance family, perform the following steps to modify mouse settings:

1.  Modify mouse-related settings in Control Panel.
    1.  Open Control Panel, set View by to **Small icons**, and then click **Mouse**.
    2.  In the **Mouse Properties** dialog box, click the **Pointer Options** tab, clear **Enhance pointer precision**, and then click **OK**.
2.  Modify mouse settings in the registry.

    **Note:** If two cursors do not appear when you log on to your Windows instance, skip this step because you do not need to modify the registry configurations.

    1.  Open Registry Editor.
    2.  In the left-side hierarchy tree, click **HKEY\_USERS** and choose **Edit** \> **Find** in the top navigation bar.
    3.  In the Find dialog box, enter MouseSpeed and click **Find Next**.
    4.  Double-click **MouseSpeed**. In the Edit String dialog box, set **Valid data** to **0** and click **OK**.
3.  Use VNC to log on to the Windows instance again.

## What do I do if I fail to deploy a Data Plane Development Kit \(DPDK\) application on an ECS instance?

We recommend that you deploy DPDK applications on g5ne instances. For more information about the g5ne instance types, see [Instance families](/intl.en-US/Instance/Instance families.md).

If you deploy DPDK applications on ECS instances of the sixth-generation and later instance types \(such as g6, c6, and r6 instance types\), the bound igb\_uio port may not be detected when you use Pktgen-DPDK to perform tests, and the following error is reported:

```
EAL: eal_parse_sysfs_value(): cannot open sysfs value /sys/bus/pci/devices/0000:00:09.0/uio/uio0/portio/port0/start
```

If you are using DPDK 19.05, you can troubleshoot the problem by installing patches. Youcan [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm) to obtain the patches and run the following commands to install them:

```
cd dpdk
copy virtio0.95_bar0_memebar.diff to dpdk
git apply virtio0.95_bar0_memebar.diff
```

## Can I upgrade the instance types and other configurations of subscription instances?

Yes, you can upgrade the instance types and other configurations of subscription instances. For more information, see [Upgrade the instance types of subscription instances](/intl.en-US/Instance/Change configurations/Change instance types/Upgrade the instance types of subscription instances.md).

## Can I upgrade the instance types and other configurations of pay-as-you-go instances?

Yes, but you must stop pay-as-you-go instances before you can upgrade their instance types and other configurations. You can upgrade the instance types and other configurations of pay-as-you-go instances by following the instructions in [Change the instance type of a pay-as-you-go instance](/intl.en-US/Instance/Change configurations/Change instance types/Change the instance type of a pay-as-you-go instance.md) or by calling the [ModifyInstanceSpec](/intl.en-US/API Reference/Instances/ModifyInstanceSpec.md) operation.

## How long does it take to upgrade the configurations of an instance?

-   Subscription instances do not need to be stopped for their instance types to be upgraded. It takes about 15 minutes to upgrade the instance type of a subscription instance.
-   Pay-as-you-go instances must be stopped for their instance types to be upgraded. It also takes about 15 minutes to upgrade the instance type of a pay-as-you-go instance.
-   You can upgrade the bandwidths of instances without stopping the instances. The upgrade process takes about 5 minutes.

## How is the fee for an instance configuration upgrade calculated?

The fee and its calculation method are displayed in the ECS console when you upgrade the instance type or other configurations of an instance. You can also view the billing details on the [Account Overview](https://expense.console.aliyun.com/) page.

## Are my cloud service configurations affected if I upgrade the configurations of ECS instances?

Pay-as-you-go instances must be stopped before their configurations can be upgraded. After you upgrade the configurations of a subscription instance, you must restart the instance for the new configurations to take effect. The upgrade operation interrupts the services that run on the instance for a short period of time. We recommend that you upgrade the configurations of instances during off-peak hours. Instances can seamlessly resume services after upgrades without environment reconfiguration.

## How do I upgrade ECS resources?

For information about how to upgrade ECS resources, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md).

-   ECS instances, except those that use local storage, can have their CPU and memory resources scaled and their bandwidths upgraded while the instances are running. You can also downgrade the configurations of ECS instances.
-   A maximum of 16 data disks can be attached to each ECS instance. You can extend a data disk but cannot shrink a data disk after it is extended.
-   The bandwidth of each ECS instance is measured in Mbit/s and can range from 0 Mbit/s to 200 Mbit/s. You can modify the bandwidth or change the billing method for network usage.

## I have upgraded the configurations of an instance but no changes have taken effect. Why?

After you upgrade the configurations of an instance, you must restart the instance by using the ECS console or by calling an API operation for the new configurations to take effect.

## What do I do if I cannot access a website that runs on an ECS instance?

For information about how to solve this problem,see [Unable to access the website running on ECS instances](https://www.alibabacloud.com/help/faq-detail/31710.htm).

If the problem persists, submit a ticket.

## My ECS instance was stuck in the Starting state, and AliyunService was disabled or deleted. What do I do?

Problem description: After an ECS instance was started, it stayed in the Starting state for an extended period of time and then automatically stopped. You logged on to the instance and found that AliyunService was deleted or disabled in the system services.

Solution:

-   If AliyunService was disabled:
    1.  Change the state of AliyunService to automatic.
    2.  Restart the instance.
-   If AliyunService was deleted:
    1.  Run the following command to add AliyunService to the instance:

        ```
        sc create AliyunService type= "own" start= "auto" binPath= "C:\Program Files\AliyunService\AliyunService.exe -d" tag= "no" DisplayName= "AliyunService"
        ```

        **Note:** Make sure that you leave a space after each equal sign `(=)`.

    2.  Find the registry key HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\AliyunService, and change `c:\Program Files\AliyunService\AliyunService.exe -d` to `"c:\Program Files\AliyunService\AliyunService.exe" -d`.
    3.  Restart the instance.

## How do I use f1 instances?

After you create an f1 instance, Alibaba Cloud shares an FPGA development image to you. Only CentOS 7u2 images are supported. The FPGA development image includes the complete Intel Quartus development suite and the f1 instance constraint files to provide a complete cloud development environment.

**Note:** You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.

The following section describes the basic workflow to use an f1 instance:

1.  After development is complete, you can generate an intermediate QAR file during the compilation stage and upload the file to an Object Storage Service \(OSS\) bucket. You can upload this file only to an OSS bucket within the China \(Hangzhou\) region. Then, you can register the QAR file information with Alibaba Cloud by calling an API operation.

    We recommend that you use the free Intel Quartus development suite to complete development, compilation, and simulation operations on the cloud.

2.  Alibaba Cloud verifies your registration request for the QAR file, and sends you an email that includes an FPGA image ID if the verification is successful.
3.  To deploy the image, you can call an API operation with the f1 instance ID and FPGA image ID specified to associate the instance with the image.

    You can initiate the association operation in all scenarios where ECS API is available.

    -   If the f1 instance has never been associated with any FPGA image, initiate the association operation.
    -   If the f1 instance was previously associated with an FPGA image and had the image loaded, erase the FPGA image from the f1 instance before you initiate the association operation.
4.  After you associate the FPGA image with the instance, call an API operation to load the image.

    You must initiate the load operation from the f1 instance. Then, the underlying service of Alibaba Cloud burns the associated FPGA image to the corresponding FPGA on the instance.


If you want to restore the f1 instance to its initial state, call an API operation to erase the burned FPGA image from the f1 instance.

For more information about how to manage f1 instances, see the following topics:

-   [Create an f1 instance](/intl.en-US/Instance/Instance type families/Compute optimized type family with FPGA/Create an f1 instance.md)
-   [Use OpenCL on an f1 instance](/intl.en-US/Best Practices/FaaS instances best practices/Use OpenCL on an f1 instance.md)
-   [Use RTL Compiler on an f1 instance](/intl.en-US/Best Practices/FaaS instances best practices/Use RTL Compiler on an f1 instance.md)

## How do I upload files by using the FTP tool in macOS?

Method 1: Upload files by using the Terminal of macOS

Open the Terminal in macOS or iTerm2 for Mac \(click [here](https://www.iterm2.com/) to download iTerm2\). Make sure that you select the correct destination path.

1.  Connect to the FTP server.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3301359951/p43224.png)

2.  Access the destination directory. In Windows, use the working directory as the destination directory. In Linux, switch to the htdocs directory and use it as the destination directory.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3301359951/p49119.png)

3.  Run the put command to upload files.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3301359951/p49120.png)


Method 2: Upload files by using a third-party tool

1.  Download Yummy FTP.
2.  Install Yummy FTP.
3.  Enter the server IP address, username, and password. Set Protocol to Standard \(FTP\). Set Port to 21 or a different port number that you are using, and leave the SSH key field unselected.
4.  Click **Connect**.
5.  In the right-side pane, select the destination directory. In Windows, use the current working directory. In Linux, select the htdocs directory. In the left-side pane, select files and click the Upload icon to upload the files.

    **Note:** If you attempt to install Yummy FTP and are prompted with a message similar to "Your security preferences only allow the installation of applications from the Mac App Store and authorized developers", perform the following steps:

    1.  Choose **System Preference** \> **Security and Privacy**.
    2.  Click the security lock in the lower-left corner of the window and enter the administrator password.
    3.  Set **Allow apps download from** to **Anywhere**.
    Then, you can upload files by using Yummy FTP.


If you have further questions, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

## How do I apply for an ICP filing for my domain name after I purchase an ECS instance?

For each ECS instance, you can apply for a limited quantity of service identification numbers for ICP filings. For more information, see [Prepare and check the instance and access information]().

## An ECS instance fails to load the kernel to start. What do I do?

Problem description: The system does not respond when you select an option from the GRUB menu on system startup. After you have mounted the LiveCD image to the ECS instance, you can log on to the instance and confirm that the file system privileges are correct and that the message logs show no exceptions.

Cause: The system has been attacked by ransomware.

Solution: Back up your data and re-initialize the system.

For more information, see [Recover from ransomware attacks](https://www.alibabacloud.com/help/faq-detail/50358.htm).

## How do I change the logon password from within an instance?

For information about how to change the logon password from within an instance, see [Change the logon password of an instance by connecting to the instance](/intl.en-US/Instance/Manage instances/Change the logon password of an instance by connecting to the instance.md).

## Why am I unable to add sound or video cards to ECS instances?

The servers that Alibaba Cloud ECS provides are not multimedia servers and do not provide sound or video card components. Sound or video cards cannot be added to ECS instances.

## Can I transfer the unused time of an ECS instance to another ECS instance?

No, the unused time of an ECS instance cannot be transferred to other ECS instances. If you want both higher flexibility and cost-effectiveness, we recommend that you use a combination of reserved instances and pay-as-you-go instances. For more information, see [Overview](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Overview.md).

## Do ECS instances provide databases by default?

No, ECS instances do not provide databases by default. To use database services, perform the following operations:

-   Deploy your own database.
-   Purchase [ApsaraDB RDS](https://rdsnext.console.aliyun.com/) provided by Alibaba Cloud.
-   Use a database image provided in Alibaba Cloud Marketplace.

## Can I build a database on an ECS instance?

Yes, you can install database software and configure a database environment on an ECS instance. You can also purchase [ApsaraDB RDS](https://rdsnext.console.aliyun.com/) separately.

## Do ECS instances support Oracle databases?

Yes, ECS instances support Oracle databases. Before you install an Oracle database, we recommend that you perform a performance stress test on the ECS instance to ensure that the instance satisfies the read/write requirements of the database.

## Are public and private IP addresses independent? Can I specify or add IP addresses?

In the classic network, public and private IP addresses are independent of each other. Private IP addresses in the classic network are used for communication between ECS instances and between ECS instances and OSS buckets or ApsaraDB RDS instances. If the public bandwidth of an ECS instance is set to 0 Mbit/s, no public IP address is assigned to the instance. In normal cases, public and private IP addresses in the classic network do not change. You cannot specify, select, or add IP addresses in the classic network.

In VPCs, NAT gateways map public IP addresses to private IP addresses. You can add IP addresses by specifying or automatically assigning secondary private IP addresses to ENIs.

## Can load balancing be implemented for a single ECS instance?

Both Linux and Windows ECS instances can be load-balanced. Make sure that the configurations of ECS instances used as web servers meet the requirements for website code to run. Load balancing can be implemented for as few as one ECS instance within an account. However, we recommend you implement load balancing for two or more ECS instances.

## Can I change the region of an ECS instance?

No, the regions of purchased ECS instances cannot be changed. To change the region of an ECS instance, you can use the`ACS-ECS-CloneInstancesAcrossRegion` public template provided by [Operation Orchestration Service \(OOS\)](https://www.alibabacloud.com/help/product/119529.htm) to copy the instance to another region. The new and original instances have identical disk data but different IP addresses.

## Can I adjust the partition size of a purchased disk?

For system security and stability purposes, system disks cannot be repartitioned on either Windows or Linux instances. If you use a third-party tool to repartition system disks, unknown exceptions such as system failures and data loss may occur.

If you repartition a data disk, data may be lost. We recommend that you do not repartition data disks.

## How do I replace the automatically assigned public IP address of an ECS instance with an elastic IP address \(EIP\)?

To replace the automatically assigned public IP address of an ECS instance with an EIP, make sure that the instance uses the pay-by-bandwidth billing method for network usage and that you have purchased an EIP. Then, use one of the following methods to do the replacement:

-   Method 1:
    1.  Change the billing method for network usage from pay-by-bandwidth to pay-by-traffic. For more information, see [Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md).
    2.  Convert the automatically assigned public IP address into an EIP. For more information, see [Convert the static public IP address of an ECS instance in a VPC to an EIP](/intl.en-US/User Guide/Create an EIP/Convert the static public IP address of an ECS instance in a VPC to an EIP.md).
    3.  Disassociate the EIP obtained in the previous step from the ECS instance. For more information, see [Disassociate an EIP from a cloud resource](/intl.en-US/User Guide/Disassociate an EIP from a cloud resource.md).
    4.  Associate the EIP that you purchased with the ECS instance. For more information, see [Associate an EIP with an ECS instance](/intl.en-US/User Guide/Associate an EIP with a cloud instance/Associate an EIP with an ECS instance.md).
-   Method 2

    In the OOS console, use the `ACS-ECS-ConvertsPublicIPToNewEIPByInstanceId` template to replace the automatically assigned public IP address of the ECS instance with an EIP. To perform this operation in the China \(Hangzhou\) region, access the [ACS-ECS-ConvertsPublicIPToNewEIPByInstanceId](https://oos.console.aliyun.com/cn-hangzhou/execution/create/ACS-ECS-ConvertsPublicIPToNewEIPByInstanceId) template in the OOS console by clicking the link, and select China \(Hangzhou\) from the drop-down region list in the top navigation bar.


## How do I view subscription ECS instances in all regions within my account?

You can go to the Renewal page to view subscription ECS instances within all regions within your account.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
2.  In the top navigation bar, choose **Expenses** \> **Renewal Management**.

## When can I forcibly stop an ECS instance? What are the consequences?

If an instance cannot be stopped by a proper shutdown procedure, you can forcibly stop the instance. A forced stop is equivalent to disconnecting the power from the instance, and can result in loss of unsaved data.

## Why am I unable to reactivate my ECS instance?

An instance may fail to be reactivated due to one of the following reasons:

-   You have overdue payments within your account. Pay the outstanding bills and try again.
-   System is busy. Try again later.
-   Resources of the specified instance type are sold out.

    **Note:** You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.


## Why has an ECS instance with release protection enabled been automatically released from a scaling group?

Auto Scaling can automatically release an ECS instance created by a scale-out event even if you have enabled release protection for the instance by using the ECS console or by calling the [ModifyInstanceAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAttribute.md) operation.

To prevent the ECS instance from being automatically released, you must change its status to Protected in the Auto Scaling console. For more information, see [Put an ECS instance into the Protected state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Protected state.md).

## What is the AliVulfix process in an ECS instance?

The AliVulfix process is an Alibaba Cloud Security program that scans ECS instances for vulnerabilities.

## How do I protect ECS instances against attacks?

ECS instances use Alibaba Cloud Security to defend against DDoS attacks. CloudMonitor deployed on ECS instances can automatically detect network attacks and scrub suspicious traffic. Alibaba Cloud implements black hole filtering to protect ECS instances against high-volume attacks. To strengthen security protection, we recommend that you install security software and disable ports that are not commonly used.

## What security services does Alibaba Cloud provide?

Alibaba Cloud Security is powered by the robust data analysis capabilities of the Alibaba Cloud cloud computing platform to provide a comprehensive set of security services such as security vulnerability detection, website trojan detection, host intrusion detection, and anti-DDoS protection.

For information about more security services, see [Alibaba Cloud Security Services](https://www.alibabacloud.com/product/security).

## I have already renewed an expired Linux instance but I am still unable to access the website hosted on it. What do I do?

Problem description: A Linux ECS instance is in the Stopped state after it has expired. After you have renewed and restarted the instance, you still cannot access the website hosted on it.

Cause: This may be because the website service has not been started.

Solution:

1.  Connect to the instance and run the following command to check whether the website service has been started:

    ```
    # netstat -nltp //Check whether port 80 on the instance is being listened on.
    ```

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3301359951/p41861.png)

2.  If no information about port 80 is displayed in the command output, the website service has not been started. Run a command to manually start the website service and relevant services.

    In Linux, websites are typically developed based on PHP and MySQL.

    -   In Apache, you only need to start the website service and MySQL.

        ```
        #/etc/init.d/httpd start          //Start the website service. This command is applicable to Apache.
        #/etc/init.d/mysqld start         //Start MySQL.
        ```

    -   In NGINX, you must start the website service, PHP, and MySQL.

        ```
        #/etc/init.d/nginx start          //Start the website service. This command is applicable to NGINX.
        #/etc/init.d/php-fpm start        //Start PHP.
        #/etc/init.d/mysqld start         //Start MySQL.
        ```

3.  Check again whether the website service has been started.

    ```
    #netstat -nltp //Check whether port 80 on the instance is being listened on.
    ```

4.  After the website service has been started, access the website again.

If the problem persists, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

## How do I activate a Windows ECS instance in a VPC?

To activate a Windows ECS instance in a VPC, you must use a specific KMS domain name. For more information, see [How to activate the VPC-Connected Windows instances using KMS servers](https://www.alibabacloud.com/help/doc-detail/41056.html).

## How do I query, partition, and format the disks of a Linux instance?

You can run the df –h command to check the capacity and usage of disks, and run the fdisk –l command to view disk information. For information about how to partition and format the disks of Linux instances, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md).

## How do I upload files to a Linux instance?

You can use the FTP service to upload files to a Linux instance.

## How do I change the owner and owner group of directories and files on a Linux instance?

If the file or directory permissions are not correctly configured on the web server, a 403 error is reported when you access a website hosted on the instance. Before you adjust a file or directory, you must identify the identity under which the file or directory process is running.

You can run the ps and grep commands to query the identities under which processes are running.

You can run the ls –l command to query the owners and owner groups of files and directories.

To change the owners and owner groups, run the chown command. For example, you can run the chown -R www.www /alidata/www/phpwind/ command to change the owners and owner groups of all files and directories under the /alidata/www/phpwind directory to the www account.

## How do I update the software repository for Linux instances?

You can use an automatic tool to update the software repository for Linux instances. For more information, see [Automatic source updating tool for Linux ECS](https://www.alibabacloud.com/help/faq-detail/41177.htm).

## What limits apply to the transfer and change of public IP addresses of ECS instances?

The following limits apply to the transfer and change of public IP addresses of ECS instances:

-   In the classic network:
    -   You cannot transfer public IP addresses across accounts.
    -   The public IP address of an ECS instance can be changed within 6 hours after the instance is created, and can be changed a maximum of three times. For more information, see [Change the public IP address of an ECS instance](/intl.en-US/Network/Change IPv4 addresses/Change the public IP address of an ECS instance.md).
    -   If Anti-DDoS Pro is deployed, you can change the IP address of an ECS instance a maximum of 10 times by using the Anti-DDoS Pro console. For more information, see the [Change ECS IP](/intl.en-US/Anti-DDoS Pro Service (Old)/User Guide/Instance management/Change ECS IP.md) section in Anti-DDoS Pro User Guide.
-   In VPCs:
    -   You cannot transfer public IP addresses or EIPs across accounts.
    -   If no public IP address is assigned to your instance, you can associate an EIP with the instance. You can replace the public IP address of your instance with an EIP.
    -   If a public IP address is assigned to your instance while the instance is being created:
        -   This public IP address can be changed within 6 hours after the instance is created, and can be changed a maximum of three times. For more information, see [Change the public IP address of an ECS instance](/intl.en-US/Network/Change IPv4 addresses/Change the public IP address of an ECS instance.md).
        -   You can convert this public IP address to an EIP and then replace the EIP. For more information, see [Convert the public IP address of a VPC-type instance to an Elastic IP address](/intl.en-US/Network/Change IPv4 addresses/Convert the public IP address of a VPC-type instance to an Elastic IP address.md).

If you have further questions, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

## Can I access amazon.com from my ECS instance?

You can access amazon.com from your ECS instance if the instance can connect to the Internet properly.

## Why am I unable to access a website hosted outside mainland China after I log on to my ECS instance?

You can access a website hosted outside mainland China from your ECS instance only when the website complies with the laws, regulations, and regulatory requirements of the country or region where your instance is located. Make sure that your ECS instance can properly connect to the Internet and that the website complies with the preceding laws, regulations, and regulatory requirements.

## I cannot purchase more pay-as-you-go instances. What do I do?

If you have reached the maximum number of pay-as-you-go instances that you can purchase, you cannot purchase more pay-as-you-go instances. For more information, see the "Instance limits" section in [Limits](/intl.en-US/Product Introduction/Limits.mdsection_tbg_zdx_wdb). You can log on to the ECS console and click Privileges in the upper-right corner of the Overview page to view your resource quotas. For more information, see [View quotas \(old version\)]().

## How can I view the resource quota?

For more information about how to view the limits and quotas of resources, see [Limits](/intl.en-US/Product Introduction/Limits.md).

## Am I still charged for a pay-as-you-go instance after it is stopped either manually or due to an overdue payment?

**Stopped due to an overdue payment**: When a payment becomes overdue within your account, your pay-as-you-go instance is automatically stopped and billing for the instance stops. Instances do not always stay in the Stopped state after they are stopped due to overdue payments. For more information, see [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md).

**Manually stopped**: You can stop a running pay-as-you-go instance by using the ECS console or by calling the StopInstance operation. When the instance is stopped, its status changes to **Stopped**. Billing for stopped pay-as-you-go instances is based on their network types.

-   VPC: You can enable the No Fees for Stopped Instances \(VPC-Connected\) feature.
    -   After the feature is enabled, billing for pay-as-you-go instances in VPCs starts when the instances are created, stops when the instances enter the **Stopped** state, and resumes when the instances are started. When a pay-as-you-go instance enters the Stopped state, the No Fees for Stopped Instances \(VPC-Connected\) feature stops billing only for the vCPUs, memory, and public IP address of the instance. You continue to be billed for other resources such as disks and EIPs of the instance. For more information, see [No Fees for Stopped Instances \(VPC-Connected\)](/intl.en-US/Pricing/Billing methods/No Fees for Stopped Instances (VPC-Connected).md).
    -   After the feature is disabled, billing for pay-as-you-go instances continues when they are stopped.
-   Classic network: You are billed for ECS instances in the classic network regardless of whether they are in the **Stopped** state.

## What do I do if an order cannot be placed to change the billing method of an instance from pay-as-you-go to subscription?

You may be unable to place the order due to one of the following reasons:

-   The instance is in a state that does not support changes to the billing method. For example, you have an unpaid order for the instance.
-   Changes to the billing method are not allowed due to an upcoming scheduled automatic release.
-   Changes to the billing method are not allowed because the instance information has changed.
-   A previous order to change the billing method of the instance has not been paid.

If one of the preceding errors is reported, adjust the instance accordingly.

## How long after an order is paid does it take to change the billing method of an instance from pay-as-you-go to subscription?

The billing method of your ECS instance is changed after the order is paid. It can take up to 4 seconds to change the billing method of 20 instances. After the change is complete, you can see that the billing method of your instance has been changed to **Subscription** in the ECS console.

## What do I do if the billing method of an instance cannot be changed from pay-as-you-go to subscription?

[Submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

## When I change the billing method of an instance from pay-as-you-go to subscription, does the billing method for network usage of the instance also change?

No, the billing method for network usage of the instance does not change. Only the billing method of instances and disks can be changed from pay-as-you-go to subscription. For information about how to change the billing method for network usage, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md).

## I have an unpaid order to change the billing method of an instance from pay-as-you-go to subscription. If I upgrade the configurations of the instance, is the order still valid?

An order is created when you change the billing method of your instance from pay-as-you-go to subscription. You must pay for the order to complete the change. If you upgrade the configurations of the instance before the order is paid, the order payment cannot be completed because the instance components are different and the original order no longer matches. If you still want to change the billing method of your instance, you must cancel the unpaid order and place a new order.

## What do I do if the billing method of an instance cannot be changed from subscription to pay-as-you-go?

You may be unable to change the billing method of an instance from subscription to pay-as-you-go due to one of the following reasons:

-   The instance is in a state that does not support changes to the billing method. For example, you have an unpaid order for the instance.
-   The instance is in the **Expired** state.
-   The instance information has changed. For example, the bandwidth of the instance has been temporarily upgraded.

If one of the preceding errors is reported, adjust the instance accordingly. If the problem persists, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

## When I attempt to change the billing method of a disk in an ECS instance, an error message is returned indicating that I have already changed the billing method three times. What does this mean?

Each ECS instance can have its configurations downgraded a maximum of three times. Downgrade operations include downgrades of instance specifications, bandwidth downgrades, and the change of the disk billing method from subscription to pay-as-you-go.

## Why am I unable to change a pay-as-you-go instance into a subscription one?

The pay-as-you-go instance whose billing method you want to change must meet the following requirements:

-   The instance type of the instance is not retired. For more information, see [Retired instance types](/intl.en-US/Instance/Instance type families/Retired instance types.md).
-   The instance is not a preemptible instance.
-   No unpaid orders related to the instance exist.

    If unpaid orders related to the instance exist, you must pay for the orders or cancel the orders before you change the billing method of the instance.

-   Automatic release time is not configured for the instance.

    If automatic release time is set for the instance, you must disable the automatic release configuration before you change the billing method. For more information, see [Disable automatic release](/intl.en-US/Instance/Manage instances/Release an instance.md).

-   The instance is in the **Running** or **Stopped** state.

    Example: An order to change the billing method was placed while the ECS instance is in the Running or Stopped state. However, the instance status changes before the payment was attempted. The order fails and the billing method does not change. You can go to the Billing Management console and pay for the order when the instance is in the Running or Stopped state again.


## How do I view the expiration time of a subscription instance?

You can log on to the ECS console and go to the Instances page to view the expiration time of your subscription instance in the **Billing Method** column.

**Note:** If the **Billing Method** column is not displayed, click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3301359951/p53726.png) icon in the upper-right corner. In the Column Filters dialog box, select **Billing Method** and click **OK**.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3301359951/p53728.png)

