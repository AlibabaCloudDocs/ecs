---
keyword: [secure logon, SSH logon, SSH logon, log on to a Linux instance, ECS, SSH key]
---

# Create an SSH key pair

This topic describes how to create an SSH key pair in the ECS console. After a key pair is created, its private key is automatically downloaded. You must securely lock away the private key. To log on to an ECS instance that is bound with an SSH key pair, you must have the private key. You can have a maximum of 500 key pairs within a region.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **SSH Key Pairs**.

3.  In the top navigation bar, select a region.

4.  Click **Create SSH Key Pair**.

5.  On the **Create SSH Key Pair** page, configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**SSH Key Pair Name**|The key pair name must be unique. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), hyphens \(-\), and colons \(:\). It cannot start with a digit or special character.|
    |**Creation Type**|The method to create the SSH key pair. We recommend that you select **Auto-create** and save the private key in a timely manner.     -   **Auto-create**: The system automatically creates a key pair for you. The private key is automatically downloaded after the key pair is created. You must securely lock away the private key.
    -   **Import**: You can import a Base64-encoded public key. |
    |**Tag**|The tag bound to the SSH key pair. You can bind one or more tags to a key pair to facilitate resource search and aggregation. For more information, see [Overview](/intl.en-US/Tag & Resource/Tags/Overview.md).|

6.  Click **OK**.


After the key pair is created, your browser downloads the private key file \(<Key pair name\>.pem\) to your computer.

**Note:** Private key files are downloaded to the computer only when Auto-create is selected. Private key files are not saved in the ECS console and cannot be recovered once lost. We recommend that you securely lock away your private key files.

After you create the SSH key pair, you must bind it to an ECS instance before you can use the SSH key pair to log on to the instance. For more information, see [Bind an SSH key pair to an instance](/intl.en-US/Security/Key pairs/Use an SSH key pair/Bind an SSH key pair to an instance.md).

**Related topics**  


[CreateKeyPair](/intl.en-US/API Reference/SSH key pairs/CreateKeyPair.md)

