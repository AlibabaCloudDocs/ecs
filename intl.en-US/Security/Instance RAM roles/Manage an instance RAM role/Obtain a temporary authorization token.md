# Obtain a temporary authorization token

You can obtain a temporary authorization token for an instance RAM role. The token is updated on a regular basis and allows you to use the permissions and resources granted to the RAM role.

1.  Connect to an ECS instance from a remote client. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Obtain a temporary authorization token for an instance RAM role. The name of the instance RAM role is `EcsRamRoleDocumentTesting`.

    -   For Linux instances, run the following command:

        ```
        curl http://100.100.100.200/latest/meta-data/Ram/security-credentials/EcsRamRoleDocumentTesting
        ```

    -   For Linux instances, run the following PowerShell command:

        ```
        Invoke-RestMethod http://100.100.100.200/latest/meta-data/Ram/security-credentials/EcsRamRoleDocumentTesting
        ```

    Example of a temporary authorization token obtained:

    ```
    {
       "AccessKeyId" : "<yourAccessKeyId>",
       "AccessKeySecret" : "<yourAccessKeySecret>",
       "Expiration" : "2017-11-01T05:20:01Z",
       "SecurityToken" : "<yourSecurityToken>",
       "LastUpdated" : "2017-10-31T23:20:01Z",
       "Code" : "Success"
    }
    ```


**Related topics**  


[Overview](/intl.en-US/Instance/Manage instances/Metadata/Overview.md)

