# Access mode of instance metadata

The metadata of ECS instances can be accessed in normal or security-enhanced mode. In security-enhanced mode, ECS instances access instance metadata by using token-based authentication. Compared with the normal mode, the security-enhanced mode provides better protection against Server-Side Request Forgery \(SSRF\) attacks.

## Overview

An SSRF is an attack in which an attacker takes advantage of vulnerabilities in a server to send crafted resource requests to the server and access resources located within the same internal network. When a request for instance metadata is received, the instance metadata server shares the requested metadata in URLs. These URLs are vulnerable to tampering and may be used to attack internal systems that are not accessible to external networks. To prevent SSRF attacks, we recommend that you access instance metadata in security-enhanced mode.

The following table compares the normal and security-enhanced modes.

|Comparison item|Normal mode|Security-enhanced mode|
|---------------|-----------|----------------------|
|Interaction mode|Interact with requests and responses.|Interact in sessions.|
|Security verification|Verify source IP addresses within the same VPC.|Verify tokens for authentication.|
|Access method|Use cURL commands to access the endpoint.|Use cURL commands to access the endpoint. Requests must include token headers.|

In normal mode, a new connection is established with each request to access instance metadata, and the connection is released immediately after the request is complete. This mode uses a simple verification method. If the instance metadata server is attacked and sensitive data such as RAM roles is leaked, your data and assets are under threats.

In security-enhanced mode, you can establish a session between an ECS instance and the instance metadata server. When you access instance metadata by using the ECS instance, the instance metadata server authenticates your identity based on a token. When the token expires, the instance metadata server closes the session and deletes the token. For more information about the access process, see [Procedure to access instance metadata in security-enhanced mode](#section_o7b_wye_3ok). The following limits apply to tokens:

-   Each token can be used only for a single ECS instance. If you copy the token file of one ECS instance to another ECS instance, the instance metadata server denies access from the ECS instance by using the copied token file.
-   Each token must have a defined validity period that ranges from 1 to 21,600 seconds \(six hours\). Tokens can be repeatedly used until they expire. This helps achieve a good balance between security and user experience.
-   Proxy access is not supported. If a request used to create a token contains the `X-Forwarded-For` header, the instance metadata server refuses to issue the token.
-   An unlimited number of tokens can be issued to each ECS instance.

## Scenarios of the security-enhanced mode

In the following scenarios, we recommend that you access instance metadata in security-enhanced mode to prevent SSRF attacks and improve the security of applications:

-   Access self-managed network firewall applications.
-   Access self-managed reverse proxy applications.
-   Access self-managed web applications that provide transcoding and download services.

## Procedure to access instance metadata in security-enhanced mode

This section describes how to run a cURL command to create and use a token to access instance metadata in security-enhanced mode.

1.  Use the PUT method to initiate a request to create a token.

    You must specify the token validity period in the header in the following format: `X-aliyun-ecs-metadata-token-ttl-seconds:<token validity period>`.

2.  The instance metadata server issues the token.
3.  When you access instance metadata, enter the endpoint of the instance metadata server and the token header.

    Token header format: `x-aliyun-ecs-metadata-token: $TOKEN`.

4.  When authentication succeeds, the instance metadata server returns the requested instance metadata.

The following command is a sample command to create and use a token:

```
TOKEN=`curl -X PUT "http://100.100.100.200/latest/api/token" -H "X-aliyun-ecs-metadata-token-ttl-seconds: 21600"` \
&& curl -H "X-aliyun-ecs-metadata-token: $TOKEN"  http://100.100.100.200/latest/meta-data/instance-id
```

The preceding sample command involves the following steps:

-   Use the PUT method to create a token with a validity period of 21,600 seconds \(6 hours\).
-   Use the TOKEN variable to store the token.
-   Access the instance ID in instance metadata and include the $TOKEN variable in the request.

Tokens can be repeatedly used until they expire. The following command is a sample command to use an existing token:

```
curl -H "X-aliyun-ecs-metadata-token: $TOKEN"  http://100.100.100.200/latest/meta-data/instance-id
```

Error examples:

-   The validity period exceeds the allowed maximum length.

    ```
    curl -X PUT "http://100.100.100.200/latest/api/token" -H "X-aliyun-ecs-metadata-token-ttl-seconds: 21700"
    ```

-   The request used to create a token contains the X-Forwarded-For header.

    ```
    curl -X PUT "http://100.100.100.200/latest/api/token" -H "X-Forwarded-For: www.ba****.com"
    ```

-   The token specified for access to instance metadata is invalid.

    ```
    curl -H "X-aliyun-ecs-metadata-token: aaa" -v http://100.100.100.200/latest/meta-data/
    ```


