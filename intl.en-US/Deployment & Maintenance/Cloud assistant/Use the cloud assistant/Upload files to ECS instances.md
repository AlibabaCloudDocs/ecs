Upload files to ECS instances 
==================================================

This topic describes how to use the Cloud Assistant client to upload files such as configuration files and scripts to Elastic Compute Service (ECS) instances. 

Prerequisites 
----------------------------------

* The ECS instances are in the **Running** (Running) state.

  

* The Cloud Assistant client is installed on the instances. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).

  

* You can call an operation to send a file to a maximum of 50 instances at a time.

  

* The file to send cannot exceed 32 KB in size after it is encoded in Base64.

  




Procedure 
------------------------------

1. Log on to the [ECS console](https://ecs.console.aliyun.com).

   

2. In the left-side navigation pane, choose **Maintenance \& Monitoring** \> **ECS Cloud Assistant** .

   

3. In the upper-left corner of the top navigation bar, select a region.

   

4. Click **Send File** .

   

5. In the **Command Information** section, configure the parameters described in the following table. 

   

   |     Parameter      |                                                                                                                                                                                                             Description                                                                                                                                                                                                              |
   |--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | Destination System | The operating system of the ECS instances. Valid values: * **Linux**   * **Windows**                                                                                                                                                                                                                                              |
   | Upload File        | The method used to upload the file. Valid values: * **Upload File** : You can click the upload section and select a file, or drag a file to the upload section.   * **Paste File Content** : You can paste the file content to the field.    **Note** The file to send cannot exceed 32 KB in size after it is encoded in Base64. |
   | File Name          | The name of the file.  **Note** If you turn off **Overwrite** , make sure that the file name is unique within the destination path of the ECS instance.                                                                                                                                                                                                                                                              |
   | Destination Path   | The path to save the file. The following path is used by default: * Default value when Destination System is set to Linux: `/root`   * Default value when Destination System is set to Windows: `C:/Users/Administrator/Documents`                                                                                                |
   | File Description   | The description of the file.                                                                                                                                                                                                                                                                                                                                                                                                         |
   | User               | The user to which the file belongs.  This parameter is required only for Linux instances.                                                                                                                                                                                                                                                                                                                            |
   | User Group         | The user group to which the file belongs.  This parameter is required only for Linux instances.                                                                                                                                                                                                                                                                                                                      |
   | Permission         | The permissions on the file.  Default value: `0644`. This value indicates that the file owner has read and write permissions on the file, and other users in the same user group as the file owner and public users have read permissions on the file.  This parameter is required only for Linux instances.                                                                                         |
   | Overwrite          | Specifies whether to overwrite the file that has the same name as the sent file in the destination path.                                                                                                                                                                                                                                                                                                                             |
   | Timeout Period     | The timeout period for the file sending task. When the file sending task times out, Cloud Assistant forcibly stops the task process.  Valid values: 10 to 86400. Unit: seconds. Default value: 60.                                                                                                                                                                                                                   |

   

   

6. In the **Select Instances** section, select one or more instances.

   

7. Click **Create Task** .

   

8. In the panel that appears, view the execution result of the file sending task. 

   ![File sent](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5690372061/p168938.png)
   




View file sending results 
----------------------------------------------

1. In the left-side navigation pane, choose **Maintenance \& Monitoring** \> **ECS Cloud Assistant** .

   

2. Click the **File Sending Result** tab.

   

3. In the task list, view the execution status, execution ID, and destination path of the task. 

   You can also click buttons in the Actions column to perform the following operations:
   * Click **View** to view the task execution result on each ECS instance.

     
   
   * Click **Export** to export the task execution results.

     
   
   * Click **Send Again** to execute this task again.

     
   

   




References 
-------------------------------

* [SendFile](/intl.en-US/API Reference/Cloud assistant/SendFile.md)

  

* [DescribeSendFileResults](/intl.en-US/API Reference/Cloud assistant/DescribeSendFileResults.md)

  



