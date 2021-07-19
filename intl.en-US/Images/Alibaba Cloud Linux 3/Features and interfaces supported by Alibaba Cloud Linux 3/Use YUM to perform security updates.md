# Use YUM to perform security updates

This topic describes how to use YUM to query, check, and install security updates for Alibaba Cloud Linux 3.

An Elastic Compute Service \(ECS\) instance that runs Alibaba Cloud Linux 3 is created. For more information, see [Creation method overview](/intl.en-US/Instance/Create an instance/Creation method overview.md).

## Background information

To ensure system security, Alibaba Cloud Linux 3 stays up to date on Common Vulnerabilities and Exposures \(CVE\) through a community-based effort supported by the industry. Alibaba Cloud Linux 3 updates software packages including the kernel, fixes software defects and security vulnerabilities, and enhances security features in a timely manner. For information about Alibaba Cloud Linux 3 security updates, see [Alibaba Cloud Linux 3 Security Advisories](http://mirrors.aliyun.com/alinux/3/cve/alinux3.xml).

Alibaba Cloud Linux 3 security updates are classified into the following severity levels based on the Common Vulnerability Scoring System 3 \(CVSS3\) for CVE:

-   Critical: High-risk vulnerabilities exist and the security update is required.
-   Important: Relatively high-risk vulnerabilities exist and the security update is strongly recommended.
-   Moderate: Medium-risk vulnerabilities exist and the security update is recommended.
-   Low: Low-risk vulnerabilities exist and the security update is optional.

## Query security updates

You can run the following command to query security updates:

```
yum updateinfo <command\> \[option\]
```

The following table describes the variables of the command.

|Variable|Valid value|
|--------|-----------|
|<command\>|-   `list`: queries the list of available security updates.
-   `info <update\_id\>`: queries the details of a specific security update. The value of the <update\_id\> parameter is an advisory ID in Alibaba Cloud Linux 3 security advisories. |
|\[option\]|-   `--sec-severity=<SEVS\>`: specifies the security update severity level. The <SEVS\> value is the specified security level.

**Note:** You can specify multiple security update severity levels and separate them with commas \(,\). The values of security update severity levels are case-sensitive.

Format description:

    -   Specify a single security update severity level in the `--sec-severity=Moderate` format.
    -   Specify multiple security update severity levels in the `--sec-severity={Moderate,Important}` format.
-   `--cve=<CVE ID\>`: specifies one or more CVE IDs. You can obtain CVE IDs from Alibaba Cloud Linux 3 security advisories. |

This section provides examples of the commands that you can run to query security updates.

-   Run the yum updateinfo --help command to obtain the help information about the command.
-   Run the following command to query all available security updates:

    ```
    yum updateinfo
    ```

    A command output similar to the following one is returned:

    ```
    Last metadata expiration check: 0:06:42 ago on Wed 02 Jun 2021 03:05:30 AM EDT.
    Updates Information Summary: available
        3 Security notice(s)
            2 Important Security notice(s)
            1 Moderate Security notice(s)
    ```

-   Run the following command to query available security updates:

    ```
    yum updateinfo list
    ```

    A command output similar to the following one is returned:

    ```
    Last metadata expiration check: 0:09:05 ago on Wed 02 Jun 2021 03:05:30 AM EDT.
    ALINUX3-SA-2021:0008 Moderate/Sec.  gnutls-3.6.14-7.1.al8.x86_64
    ALINUX3-SA-2021:0029 Important/Sec. gnutls-3.6.14-8.1.al8.x86_64
    ALINUX3-SA-2021:0028 Important/Sec. libldb-2.1.3-3.1.al8.x86_64
    ALINUX3-SA-2021:0029 Important/Sec. nettle-3.4.1-4.1.al8.x86_64
    ```

-   Run the `yum updateinfo info <update\_id\>` command to query the details of a specific security update.

    For example, if the <update\_id\> parameter is set to `ALINUX3-SA-2021:0008`, run the following command:

    ```
    yum updateinfo info ALINUX3-SA-2021:0008
    ```

    A command output similar to the following one is returned:

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

-   Run the following command to specify a security update severity level to query the security updates:

    ```
    yum updateinfo list --sec-severity=Moderate
    ```

    A command output similar to the following one is returned:

    ```
    Last metadata expiration check: 0:05:25 ago on Mon 07 Jun 2021 09:08:25 AM EDT.
    ALINUX3-SA-2021:0008 Moderate/Sec. gnutls-3.6.14-7.1.al8.x86_64
    ```


## Check for security updates

You can run the `yum check-update --security` command to check for security updates available for the system. You can append `--sec-severity=<SEVS\>` to the command to check for security updates of a specific severity level. The <SEVS\> value is the security update severity level.

**Note:** You can specify multiple security update severity levels and separate them with commas \(,\). The values of security update severity levels are case-sensitive.

The following examples demonstrate how to check for security updates:

-   Example 1: Run the following command to check the details of all security updates.

    ```
    yum check-update --security
    ```

    A command output similar to the following one is returned:

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

-   Example 2: Run the following command to check the details of security updates of the critical and important security levels.

    ```
    yum check-update --security  --sec-severity={Critical,Important}
    ```

    A command output similar to the following one is returned:

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


## Install security updates

You can run the `yum upgrade` command to specify security update severity levels or CVE IDs and then install security updates.

-   You can run the `yum upgrade --security` command to install security updates. You can append `--sec-severity=<SEVS\>` to the command to install security updates of a specific severity level. The <SEVS\> value is the security update severity level.

    **Note:** You can specify multiple security update severity levels and separate them with commas \(,\). The values of security update severity levels are case-sensitive.

    Example:

    Run the following command to install security updates of the critical and important security levels.

    ```
    yum upgrade --security --sec-severity={Critical,Important}
    ```

    A command output similar to the following one is returned:

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

-   You can run the `yum upgrade --cves=<CVE ID\>` command to install security updates for specific CVEs. The --cve=<CVE ID\> parameter specifies the CVE IDs.

    **Note:** You can specify multiple CVE IDs and separate them with commas \(,\). The values of CVE IDs are case-sensitive.

    Example:

    Run the following command to install `CVE-2020-24659` security updates:

    ```
    yum upgrade --cve=CVE-2020-24659
    ```

    A command output similar to the following one is returned:

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


