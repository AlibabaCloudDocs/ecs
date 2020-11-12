# Known issues in Alibaba Cloud Linux 2

This topic describes known issues in Alibaba Cloud Linux 2 images, the scope of these issues, and their corresponding solutions.

## Performance issues may occur if you enable the CONFIG\_PARAVIRT\_SPINLOCK kernel feature

-   Problem description: After you enable the CONFIG\_PARAVIRT\_SPINLOCK kernel feature, application performance is significantly affected if an ECS instance has a large number of vCPUs and a large number of lock contentions exist in applications. For example, an NGINX application experiences a significant performance decrease when it processes short-lived connections.
-   Solution: We recommend that you keep the CONFIG\_PARAVIRT\_SPINLOCK kernel feature disabled in Alibaba Cloud Linux 2. By default, this feature is disabled. If you are unsure about how to resolve this kernel problem, do not enable CONFIG\_PARAVIRT\_SPINLOCK.

## The system may become unstable and performance issues may occur if you enable the THP kernel feature

-   Problem description: After you enable the Transparent Huge Pages \(THP\) kernel feature by setting the transparent\_hugepage/enabled option to always in your production environment, the system becomes unstable and its performance deteriorates.
-   Solution: For information about how to optimize THP-related performance, see [THP-related performance optimization in Alibaba Cloud Linux 2](https://www.alibabacloud.com/help/doc-detail/161963.htm).

## A delegation conflict occurs in NFS v4.0

-   Problem description: A delegation conflict occurs in NFS v4.0. For more information, visit [Delegation in NFS Version 4](https://docs.oracle.com/cd/E19253-01/816-4555/rfsrefer-140/index.html).
-   Solution: We recommend that you disable the delegation feature when you use NFS v4.0. For information about how to disable this feature on the server side, visit [How to Select Different Versions of NFS on a Server](https://docs.oracle.com/cd/E19253-01/816-4555/rfsadmin-965/index.html).

## Defects in NFS v4.1 or v4.2 cause applications not to exit

-   Problem description: In NFS v4.1 or v4.2, if you use asynchronous I/O \(AIO\) in applications to send requests and then close the corresponding file descriptors before I/O responses are returned, a livelock may be triggered. This causes a failure in which the corresponding process exits.
-   Solution: This problem is fixed in kernel versions 4.19.30-10.al7 and later. Application exit failure is not likely to occur. Decide whether to upgrade the kernel to fix this problem. To upgrade the kernel, run the sudo yum update kernel -y command.

    **Note:**

    -   The kernel upgrade may result in a system boot failure. Exercise caution when you perform this action.
    -   Before you upgrade the kernel, make sure that you have created a snapshot or a custom image to back up data. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md) or [Create a custom image from an instance](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from an instance.md).

## System performance is affected after security vulnerabilities such as Meltdown and Spectre are fixed

-   Problem description: In the kernel of Alibaba Cloud Linux 2, the repair of important security vulnerabilities such as Meltdown or Spectre in processors is enabled by default. This affects system performance. Performance may be deteriorated during performance benchmark testing.
-   Solution: Meltdown and Spectre are two important vulnerabilities discovered in Intel chips. Attackers can exploit these vulnerabilities to steal sensitive application data from the system memory. We recommend that you enable the repair feature. However, if you want to maximize system performance, you can disable the repair feature. For more information, see [How to fix CPU vulnerabilities in the Alibaba Cloud Linux 2 system](https://www.alibabacloud.com/help/doc-detail/154567.htm).

