# Overview

An SSH key pair is a secure and convenient authentication method provided by Alibaba Cloud for instance logon. An SSH key pair consists of a public key and a private key. You can use SSH key pairs to log on to only Linux instances.

## Introduction

An SSH key pair is a pair of public and private keys that are generated based on an encryption algorithm. By default, 2048-bit RSA key pairs are used. Before you log on to a Linux instance by using an SSH key pair, you must first create the SSH key pair. You can specify an SSH key pair when you create an instance, or bind an SSH key pair to an instance after the instance is created. Then, you can use the private key to connect to the instance.

After you create an SSH key pair, take note of the following items:

-   Alibaba Cloud stores the public key of the SSH key pair. After an SSH key pair is bound to a Linux instance, the public key of the key pair is stored in the ~/.ssh/authorized\_keys file.
-   You must download and securely lock away the private key. The private key is unencrypted. It is in the `PKCS#8` format and Privacy-Enhanced Mail \(PEM\) encoded.

## Benefits

Compared with username and password authentication, SSH key authentication has the following benefits:

-   Security: SSH key pairs provide higher security and reliability for logons.
    -   SSH key pairs are more secure than general user passwords against brute-force attacks.
    -   Private keys cannot be deduced even if the public keys are maliciously acquired.
-   Ease of use:
    -   If you configure a public key on a Linux instance, you can use the corresponding private key to run SSH commands or other tools for passwordless logons to the instance.
    -   You can log on to a large number of Linux instances at the same time. If you want to manage multiple Linux instances, we recommend that you use this method.

## Limits

SSH key pairs have the following limits:

-   If you use an SSH key pair to log on to a Linux instance, the password logon method is disabled for higher security.
-   SSH key pairs apply only to Linux instances.
-   Currently, only RSA 2048-bit key pairs can be created in the ECS console.
-   An Alibaba Cloud account can have a maximum of 500 SSH key pairs in a region.
-   When you bind SSH key pairs to Linux instances in the ECS console, you can bind a single SSH key pair to a Linux instance. If the instance already has a key pair bound, the new key pair replaces the original one. If you want to use multiple key pairs to log on to a Linux instance, you can manually modify the ~/.ssh/authorized\_keys file from within the instance to add multiple key pairs.
-   Instances of retired instance types do not support logons based on SSH key pairs. For more information, see [Retired instance types](/intl.en-US/Instance/Retired instance types.md).
-   If you bind an SSH key pair to or unbind an SSH key pair from an instance in the **Running** \(`Running`\) state, you must restart the instance for the operation to take effect. This enhances data security.

## Creation methods

You can use one of the following methods to create an SSH key pair:

-   Create an SSH key pair in the ECS console. By default, the key pair is generated in the RSA 2048-bit format. For more information, see [Create an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Create an SSH key pair.md).

    **Note:** If you create a key pair in the ECS console, you must download and securely lock away the private key. After the key pair is bound to an instance, you cannot log on to the instance if you do not have the private key.

-   Create an SSH key pair by using a key pair generator and then import the key pair to the ECS console. The imported key pair must support one of the following encryption methods:
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

