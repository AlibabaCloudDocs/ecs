# Overview of ECS instance user data

The user data of Elastic Compute Service \(ECS\) instances can be used to manage startups of the instances or pass data into the instances.

## Introduction

Both Linux and Windows instances support the user data feature. User data can be used in the following ways:

-   User data can be run as scripts on instance startup to automate instance configurations such as automatically obtaining software resource packages, enabling services, printing logs, installing dependencies, and initializing web environments.
-   User data can be used as common data and passed into instances for use.

You can prepare user data by using different types of scripts. After you prepare the user data, you can pass it into an instance by entering the script content when you create the instance. For more information, see [Manage user data of Linux instances](/intl.en-US/Instance/Manage instances/User data/Configure user data.md) and [Manage user data of Windows instances](/intl.en-US/Instance/Manage instances/User data/Modify user data.md).

You can view the user data that has been passed into an instance by using the metadata of the instance. For more information, see [Retrieve instance metadata](/intl.en-US/Instance/Manage instances/Metadata/Retrieve instance metadata.md).

## Limits

-   The user data feature is supported only for instances that reside in virtual private clouds \(VPCs\).
-   The instances must be created from the following public images or custom images derived from public images:
    -   Alibaba Cloud Linux, CentOS, Ubuntu, SUSE Linux Enterprise, OpenSUSE, and Debian
    -   Windows Server 2008 R2 and later
-   The user data feature is supported for all available instance types. For retired instance types, the user data feature is supported only for I/O-optimized instances. For more information, see [Retired instance types](/intl.en-US/Instance/Instance type families/Retired instance types.md).
-   The user data that you want to run must be encoded in Base64. The size of the user data cannot exceed 16 KB before it is encoded.

    **Note:** You can enter the user data that has not been encoded in Base64 in the console. The console automatically encodes the user data in Base64. If you do not want to enter the user data in the console, you must encode it in Base64 on your own.


