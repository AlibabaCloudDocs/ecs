# 基于YUM的安全更新操作

本文主要介绍如何使用yum查询、检查以及安装Alibaba Cloud Linux 3操作系统的安全更新。

已创建了操作系统为Alibaba Cloud Linux 3的ECS实例。具体操作，请参见[创建方式导航](/intl.zh-CN/实例/创建实例/创建方式导航.md)。

## 背景信息

Alibaba Cloud Linux 3发行版为保障系统的安全性，会紧密跟进业界与社区发现的软件问题及安全漏洞（CVE），及时更新包括内核在内的软件包、修复软件缺陷、修补安全漏洞以及增强安全功能。关于Alibaba Cloud Linux 3安全更新记录，请参见[Alibaba Cloud Linux 3安全公告](http://mirrors.aliyun.com/alinux/3/cve/alinux3.xml)。

Alibaba Cloud Linux 3安全更新根据CVE的通用漏洞评估方法（CVSS3）的评分，将安全更新分为以下四个等级：

-   Critical：高风险，必须更新
-   Important：较高风险，强烈建议更新
-   Moderate：中等风险，推荐更新
-   Low：低风险，可选更新

## 查询安全更新

查询安全更新的yum命令格式如下。

```
yum updateinfo <command\> \[option\]
```

命令内参数的取值说明如下。

|变量名称|取值|
|----|--|
|<command\>|-   `list`：查询可用的安全更新列表。
-   `info <update\_id\>`：查询指定的安全更新详情。其中参数<update\_id\>的取值为Alibaba Cloud Linux 3安全公告中的Advisory ID。 |
|\[option\]|-   `--sec-severity=<SEVS\>`：指定安全更新级别，参数<SEVS\>为指定的安全更新级别。

**说明：** 您可以指定多个安全更新的级别，以半角逗号（,）分隔，区分大小写。

格式说明：

    -   如果只指定一个安全更新级别进行查询，示例格式为`--sec-severity=Moderate`。
    -   如果同时指定多个安全更新级别进行查询，示例格式为`--sec-severity={Moderate,Important}`。
-   `--cve=<SEVS\>`：指定CVE ID。CVE ID可从Alibaba Cloud Linux 3安全公告中获取。 |

查询安全更新的命令使用示例如下。

-   运行yum updateinfo --help命令可以获取命令的帮助信息。
-   运行以下命令，查询当前全部可用的安全更新信息。

    ```
    yum updateinfo
    ```

    查询结果示例如下所示：

    ```
    Last metadata expiration check: 0:06:42 ago on Wed 02 Jun 2021 03:05:30 AM EDT.
    Updates Information Summary: available
        3 Security notice(s)
            2 Important Security notice(s)
            1 Moderate Security notice(s)
    ```

-   运行以下命令，查询当前可用的安全更新列表。

    ```
    yum updateinfo list
    ```

    查询结果示例如下所示：

    ```
    Last metadata expiration check: 0:09:05 ago on Wed 02 Jun 2021 03:05:30 AM EDT.
    ALINUX3-SA-2021:0008 Moderate/Sec.  gnutls-3.6.14-7.1.al8.x86_64
    ALINUX3-SA-2021:0029 Important/Sec. gnutls-3.6.14-8.1.al8.x86_64
    ALINUX3-SA-2021:0028 Important/Sec. libldb-2.1.3-3.1.al8.x86_64
    ALINUX3-SA-2021:0029 Important/Sec. nettle-3.4.1-4.1.al8.x86_64
    ```

-   命令`yum updateinfo info <update\_id\>`可以查询指定安全更新的内容，使用示例如下。

    例如，<update\_id\>的取值为`ALINUX3-SA-2021:0008`，则需要运行以下命令。

    ```
    yum updateinfo info ALINUX3-SA-2021:0008
    ```

    查询结果示例如下所示：

    ```
    Last metadata expiration check: 0:11:58 ago on Wed 02 Jun 2021 03:05:30 AM EDT.
    ===============================================================================
      ALINUX3-SA-2021:0008: gnutls security and bug fix update (Moderate)
    ===============================================================================
      Update ID: ALINUX3-SA-2021:0008
           Type: security
        Updated: 1969-12-31 19:00:00
           CVEs: CVE-2020-24659
    Description: Package updates are available for Alibaba Cloud Linux 3 that fix the following vulnerabilities:
               :
               : CVE-2020-24659:
               : An issue was discovered in GnuTLS before 3.6.15. A server can trigger a NULL pointer dereference in a TLS 1.3 client if a no_renegotiation alert is sent with unexpected timing, and then an invalid second handshake occurs. The crash happens in the application's error handling path, where the gnutls_deinit function is called after detecting a handshake failure.
               :
       Severity: Moderate
    ```

-   运行以下命令，指定安全更新级别进行查询。

    ```
    yum updateinfo list --sec-severity=Moderate
    ```

    查询结果示例如下所示：

    ```
    Last metadata expiration check: 0:05:25 ago on Mon 07 Jun 2021 09:08:25 AM EDT.
    ALINUX3-SA-2021:0008 Moderate/Sec. gnutls-3.6.14-7.1.al8.x86_64
    ```


## 检查安全更新

命令`yum check-update --security`可以检查系统当前可用的安全更新信息。可以在命令后追加参数`--sec-severity=<SEVS\>`来检查指定级别的安全更新，参数<SEVS\>为指定的安全更新级别。

**说明：** 您可以指定多个安全更新的级别，以半角逗号（,）分隔，区分大小写。

检查安全更新的使用示例如下。

-   示例一：运行以下命令，检查所有安全更新信息。

    ```
    yum check-update --security
    ```

    查询结果示例如下所示：

    ```
    Last metadata expiration check: 0:08:41 ago on Wed 02 Jun 2021 05:24:55 PM CST.
    
    nss.x86_64                        3.53.1-17.1.al8                 alinux3-updates
    nss-softokn.x86_64                3.53.1-17.1.al8                 alinux3-updates
    nss-softokn-freebl.x86_64         3.53.1-17.1.al8                 alinux3-updates
    nss-sysinit.x86_64                3.53.1-17.1.al8                 alinux3-updates
    nss-util.x86_64                   3.53.1-17.1.al8                 alinux3-updates
    perl-Errno.x86_64                 1.28-417.2.al8                  alinux3-updates
    perl-IO.x86_64                    1.38-417.2.al8                  alinux3-updates
    ```

-   示例二：运行以下命令，检查高风险和较高风险的安全更新信息。

    ```
    yum check-update --security  --sec-severity={Critical,Important}
    ```

    查询结果示例如下所示：

    ```
    Last metadata expiration check: 0:10:23 ago on Wed 02 Jun 2021 05:24:55 PM CST.
    
    gnutls.x86_64                      3.6.14-8.2.al8              alinux3-updates
    nss.x86_64                         3.53.1-17.1.al8             alinux3-updates
    nss-softokn.x86_64                 3.53.1-17.1.al8             alinux3-updates
    nss-softokn-freebl.x86_64          3.53.1-17.1.al8             alinux3-updates
    nss-sysinit.x86_64                 3.53.1-17.1.al8             alinux3-updates
    nss-util.x86_64                    3.53.1-17.1.al8             alinux3-updates
    perl-Errno.x86_64                  1.28-417.2.al8              alinux3-updates
    perl-IO.x86_64                     1.38-417.2.al8              alinux3-updates
    ```


## 安装安全更新

您可以通过命令`yum upgrade`指定安全更新级别或者CVE ID，安装安全更新。

-   命令`yum upgrade --security`可以安装安全更新，可在该命令后追加参数`--sec-severity=<SEVS\>`来安装指定级别的安全更新，参数<SEVS\>为指定的安全更新级别。

    **说明：** 您可以指定多个安全更新的级别，以半角逗号（,）分隔，区分大小写。

    操作示例：

    运行以下命令，安装高风险和较高风险的安全更新。

    ```
    yum upgrade --security --sec-severity={Critical,Important}
    ```

    安装过程中的回显信息示例如下所示：

    ```
    Last metadata expiration check: 0:06:43 ago on Wed 02 Jun 2021 03:51:48 AM EDT.
    Dependencies resolved.
    ================================================================================
     Package              Arch       Version              Repository           Size
    ================================================================================
    Upgrading:
    ...
    Transaction Summary
    ================================================================================
    Upgrade  12 Packages
    
    Total download size: 3.9 M
    Is this ok [y/N]:
    ```

-   命令`yum upgrade -cves=<SEVS\>`可以安装指定CVE的安全更新，参数<SEVS\>为指定的CVE ID。

    **说明：** 您可以指定多个CVE ID，以半角逗号（,）分隔，区分大小写。

    操作示例：

    运行以下命令，安装`yum upgrade --cve=CVE-2020-24659`安全更新。

    ```
    yum upgrade --cve=CVE-2020-24659
    ```

    安装过程中的回显信息示例如下所示：

    ```
    Last metadata expiration check: 0:02:44 ago on Wed 02 Jun 2021 04:17:27 AM EDT.
    Dependencies resolved.
    =====================================================================================
     Package        Architecture   Version                 Repository               Size
    =====================================================================================
    Upgrading:
    ...
    Transaction Summary
    =====================================================================================
    Upgrade  1 Package
    
    Total download size: 1.0 M
    Is this ok [y/N]
    ```


