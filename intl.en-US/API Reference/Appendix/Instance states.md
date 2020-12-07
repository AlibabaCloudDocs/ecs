# Instance states

This topic describes the possible states of ECS instances.

|State|Description|
|:----|:----------|
|Pending|The initial state of an ECS instance when you create the ECS instance in the ECS console or by calling the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) operation. Instances are only in the Pending state only during the creation process, and this state lasts for a few seconds. **Note:** If the instance is being created by calling [CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md), you must then call [t9858.md\#](/intl.en-US/API Reference/Instances/StartInstance.md) to manually change the instance state from Pending to Starting. If the instance is being created by calling [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md), the instance automatically enters the Starting state. |
|Starting|The transient state when an instance is enabled in the ECS console or by calling [StartInstance](/intl.en-US/API Reference/Instances/StartInstance.md).|
|Running|The stable state after an instance is enabled in the ECS console or by calling [StartInstance](/intl.en-US/API Reference/Instances/StartInstance.md). The instance owner can use, manage, and modify business and applications on an instance when the instance is in this state.|
|Stopping|The transient state when an instance is stopped in the ECS console or by calling [StopInstance](/intl.en-US/API Reference/Instances/StopInstance.md).|
|Stopped|The stable state after an instance has been stopped.|

