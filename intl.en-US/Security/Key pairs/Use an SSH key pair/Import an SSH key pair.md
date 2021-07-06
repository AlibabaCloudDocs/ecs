---
keyword: [upload public key, import public key]
---

# Import an SSH key pair

You can create an SSH key pair in the ECS console. You can also use a tool to generate a key pair and import its public key to Alibaba Cloud.

The public key information of the key pair to be imported is obtained. For information about how to obtain public key information of key pairs, see [View public key information](/intl.en-US/Security/Key pairs/Use an SSH key pair/View public key information.md).

**Note:**

-   Do not import the private key. You must keep the private key safe. To log on to an ECS instance that is bound with a key pair, you must have the private key.
-   Only one public key can be imported into an ECS instance.

An Alibaba Cloud account can have a maximum of 500 key pairs within a region. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).

An imported public key must be encoded in `Base64` and support one of the following encryption methods:

-   rsa
-   dsa
-   ssh-rsa
-   ssh-dss
-   ecdsa
-   ssh-rsa-cert-v00@openssh.com
-   ssh-dss-cert-v00@openssh.com
-   ssh-rsa-cert-v01@openssh.com
-   ssh-dss-cert-v01@openssh.com
-   ecdsa-sha2-nistp256-cert-v01@openssh.com
-   ecdsa-sha2-nistp384-cert-v01@openssh.com
-   ecdsa-sha2-nistp521-cert-v01@openssh.com

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **SSH Key Pairs**.

3.  In the top navigation bar, select a region.

4.  Click **Create SSH Key Pair**.

5.  Enter a key pair name and set Creation Type to **Import**.

    **Note:** The name of the SSH key pair must be unique. Otherwise, you will be prompted that the name is already in use.

6.  In the **Public Key** field, enter the public key to be imported.

7.  Click **OK**.


[Bind an SSH key pair to an instance](/intl.en-US/Security/Key pairs/Use an SSH key pair/Bind an SSH key pair to an instance.md)

**Related topics**  


[ImportKeyPair](/intl.en-US/API Reference/SSH key pairs/ImportKeyPair.md)

