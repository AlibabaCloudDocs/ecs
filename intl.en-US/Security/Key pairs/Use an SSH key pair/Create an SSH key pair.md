---
keyword: [secure logon, SSH logon, ssh logon, logon to a Linux instance, ECS, SSH key]
---

# Create an SSH key pair

This topic describes how to create an SSH key pair in the ECS console. After a key pair is created, you must immediately download and securely lock its private key away. To log on to an ECS instance that is bound with an SSH key pair, you must have the private key. You can have a maximum of 500 key pairs in a region.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **SSH Key Pairs**.

3.  In the top navigation bar, select a region.

4.  Click **Create SSH Key Pair**.

5.  On the **Create SSH Key Pair** page, configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**SSH Key Pair Name**|The key pair name must be unique. The name must be 2 to 128 characters in length and can contain letters, digits, and the following special characters: periods \(.\), underscores \(\_\), hyphens \(-\), and colons \(:\). It must start with a letter.|
    |**Creation Type**|You can select one of the following methods of creating SSH key pairs: We recommend that you select **Auto-create** and save the private key in a timely manner.     -   **Auto-create**: The system automatically creates a key pair for you. Download the private key immediately after it is created. You cannot download the private key at any time afterwards.
    -   **Import**: You can import a Base64-encoded public key. |
    |**Tag**|You can bind one or more tags to a key pair to facilitate resource search and aggregation. For more information, see [Overview](/intl.en-US/Tag & Resource/Tags/Overview.md).|

6.  Click **OK**.


After the key pair is created, your browser automatically downloads the private key file \(<key pair name\>.pem\) to your local computer.

**Note:** Private key files are automatically downloaded to the local computer only when the key pairs are created. Private key files are not saved in the ECS console. Private key files cannot be recovered once lost. We recommend that you securely lock away your private key files.

[Bind an SSH key pair to an instance](/intl.en-US/Security/Key pairs/Use an SSH key pair/Bind an SSH key pair to an instance.md)

**Related topics**  


[CreateKeyPair](/intl.en-US/API Reference/SSH key pairs/CreateKeyPair.md)

