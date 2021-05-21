---
keyword: ECS
---

# View instance metadata

This topic describes the difference between viewing instance metadata in normal mode and that in security hardening mode. This topic also demonstrates how to view the metadata of an instance.

-   The instance resides in a virtual private cloud \(VPC\).
-   You are connected to the instance. For more information, see [Guidelines on instance connection](/intl.en-US/Instance/Connect to instances/Overview.md).

You can view instance metadata by using an endpoint in the `http://100.100.100.200/latest/[metadata]` format. Replace \[metadata\] with the instance metadata item. For more information, see [t2078137.md\#]().

You can access the endpoint in normal or security hardening mode. The following table compares the two modes.

|Comparison item|Normal mode|Security hardening mode|
|---------------|-----------|-----------------------|
|Interaction mode|Interacts with requests and responses.|Interacts in sessions.|
|Security verification|Verifies source IP addresses within the same VPC.|Verifies tokens for authentication.|
|Access method|Uses cURL commands to access the endpoint.|Uses cURL commands to access the endpoint. Requests must include token headers.|

In normal mode, a new connection is established with each request to view instance metadata, and the connection is immediately released after the request is complete. This mode uses a simple verification method. If the instance metadata server is attacked and sensitive data such as RAM roles is leaked, your data and assets are at risk.

A server-side request forgery \(SSRF\) is an attack in which an attacker exploits vulnerabilities in a server to send forged resource requests to the server and access resources located within the same internal network. When a request for instance metadata is received, the instance metadata server shares the requested metadata in URLs. These URLs are vulnerable to tampering and may be used to attack internal systems that are inaccessible to external networks. In security hardening mode, instance metadata is restricted and can be viewed only by using token-based authentication. The security hardening mode provides better protection against SSRF attacks than the normal mode. In scenarios such as self-managed network firewall applications, self-managed reverse proxy applications, and self-managed web applications that provide transcoding and download services, we recommend that you view instance metadata in security hardening mode to prevent SSRF attacks and improve the security of applications.

## View instance metadata in normal mode

The following section provides examples of the shell commands that you can run to view the metadata of Linux instances.

-   View the root directory of instance metadata:

    ```
    curl http://100.100.100.200/latest/meta-data
    ```

-   View the instance ID:

    ```
    curl http://100.100.100.200/latest/meta-data/instance-id
    ```

-   View the active system events:

    ```
    curl http://100.100.100.200/latest/maintenance/active-system-events
    ```

-   View the instance identity document:

    ```
    curl http://100.100.100.200/latest/dynamic/instance-identity/document
    ```

-   View the user data of the instance:

    ```
    curl http://100.100.100.200/latest/user-data
    ```


The following section provides examples of the PowerShell commands that you can run to view the metadata of Windows instances.

-   View the root directory of instance metadata:

    ```
    Invoke-RestMethod http://100.100.100.200/latest/meta-data
    ```

-   View the instance ID:

    ```
    Invoke-RestMethod http://100.100.100.200/latest/meta-data/instance-id
    ```

-   View the active system events:

    ```
    Invoke-RestMethod http://100.100.100.200/latest/maintenance/active-system-events
    ```

-   View the instance identity document:

    ```
    Invoke-RestMethod http://100.100.100.200/latest/dynamic/instance-identity/document
    ```

-   View the user data of the instance:

    ```
    Invoke-RestMethod http://100.100.100.200/latest/user-data
    ```


## View instance metadata in security hardening mode

In security hardening mode, you can establish a session between the Elastic Compute Service \(ECS\) instance and the instance metadata server. When you attempt to view instance metadata, the instance metadata server authenticates your identity based on a token. When the token expires, the instance metadata server closes the session and deletes the token. The following limits apply to tokens:

-   Each token can be used only for a single ECS instance. If you attempt to use the token of one instance to access a different instance, you are denied access.
-   Each token must have a validity period that ranges from 1 to 21,600 seconds \(6 hours\). Tokens can be repeatedly used until they expire. This helps implement a balance between security and user experience.
-   Proxy access is not supported. If a request used to create a token contains the `X-Forwarded-For` header, the instance metadata server refuses to issue the token.
-   An unlimited number of tokens can be issued to each instance.

Perform the following steps to view instance metadata in security hardening mode:

1.  Use the PUT method to initiate a request to create a token. You must specify the token validity period in the header in the following format: `X-aliyun-ecs-metadata-token-ttl-seconds:<Token validity period>`.
2.  The instance metadata server issues the token.
3.  Enter the endpoint of the instance metadata server and the token header. Enter the token header in the following format: `X-aliyun-ecs-metadata-token: $TOKEN`.
4.  After successful authentication, the instance metadata server returns the requested instance metadata.

The following section provides examples of the commands that you can run to view instance metadata:

-   Linux instance:

    ```
    TOKEN=`curl -X PUT "http://100.100.100.200/latest/api/token" -H "X-aliyun-ecs-metadata-token-ttl-seconds: 21600"` \
    && curl -H "X-aliyun-ecs-metadata-token: $TOKEN"  http://100.100.100.200/latest/meta-data/instance-id
    ```

-   Windows instance:

    ```
    $token = Invoke-RestMethod -Headers @{"X-aliyun-ecs-metadata-token-ttl-seconds" = "21600"} -Method PUT –Uri http://100.100.100.200/latest/api/token
    Invoke-RestMethod -Headers @{"X-aliyun-ecs-metadata-token" = $token} -Method GET -Uri http://100.100.100.200/latest/meta-data/instance-id
    ```


The preceding sample commands involve the following steps:

-   Use the PUT method to create a token that has a validity period of 21,600 seconds \(6 hours\).
-   Use the TOKEN variable to store the token.
-   View the instance ID in the instance metadata and include the $TOKEN variable in the request.

Tokens can be repeatedly used until they expire. The following section provides examples of the commands that you can run to use an existing token:

-   Linux instance:

    ```
    curl -H "X-aliyun-ecs-metadata-token: $TOKEN"  http://100.100.100.200/latest/meta-data/instance-id
    ```

-   Windows instance:

    ```
    Invoke-RestMethod -Headers @{"X-aliyun-ecs-metadata-token" = $token} -Method GET -Uri http://100.100.100.200/latest/meta-data/instance-id
    ```


Error examples:

-   The validity period is 21,700 seconds, which exceeds the maximum allowed length.

    ```
    curl -X PUT "http://100.100.100.200/latest/api/token" -H "X-aliyun-ecs-metadata-token-ttl-seconds: 21700"
    ```

-   The request used to create a token contains the X-Forwarded-For header.

    ```
    curl -X PUT "http://100.100.100.200/latest/api/token" -H "X-Forwarded-For: www.ba****.com"
    ```

-   The specified token to use to view the instance metadata is invalid.

    ```
    curl -H "X-aliyun-ecs-metadata-token: aaa" -v http://100.100.100.200/latest/meta-data/
    ```


