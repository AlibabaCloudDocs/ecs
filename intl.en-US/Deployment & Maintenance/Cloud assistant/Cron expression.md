---
keyword: [Cloud Assistant, remote command, O&M plug-in, Alibaba Cloud, ECS]
---

# Cron expression

When you run a Cloud Assistant command, you can call an API operation and use the Timed and Frequency parameters to set when to run the Cloud Assistant command. The value of the Frequency parameter is a cron expression. This parameter specifies the frequency of scheduled invocations, frequency of routine maintenance, and the point in time at which to complete a one-time invocation.

## Introduction to cron expressions

A cron expression is a string that represents time. The string consists of five spaces and six fields, in the `X X X X X X` format. `X` is a placeholder of a field. If a field contains multiple values, the values are separated by commas \(`,`\). Each field can be a specific value or special characters that have logical representations.

## Values for fields

The following table lists valid values and supported special characters for each field in cron expressions.

|Field|Required|Valid value|Special character|
|-----|--------|-----------|-----------------|
|Second|Yes|\[0, 59\]|\* , - /|
|Minute|Yes|\[0, 59\]|\* , - /|
|Hour|Yes|\[0, 23\]|\* , - /|
|Day|Yes|\[1, 31\]|\* , - / ? L W|
|Month|Yes|\[1, 12\] or \[JAN, DEC\]|\* , - /|
|Week|Yes|\[1, 7\] or \[MON, SUN\]. If you use the \[1, 7\] format, `1` indicates Monday and `7` indicates Sunday.|\* , - / ? L \#|

## Special characters

Each field in a cron expression can contain a specific number of special characters. Each special character represents a logical argument.

|Special character|Description|Example|
|-----------------|-----------|-------|
|`*`|Indicates all possible values.|In the Month field, an asterisk \(`*`\) indicates any month. In the Week field, an asterisk \(`*`\) indicates any day of a week.|
|`,`|Lists enumerated values.|In the Minute field, `5,20` indicates that the task is triggered once at both the 5th and 20th minutes.|
|`-`|Indicates a range.|In the Minute field, `5-20` indicates that the task is triggered once every minute from the 5th to 20th minute.|
|`/`|Indicates increments.|In the Minute field, `0/15` indicates that the task is triggered once every 15 minutes from the beginning of an hour. In the Minute field, `3/20` indicates that the task is triggered once every 20 minutes from the 3rd minute of an hour.|
|`?`|Indicates an unspecified value. Only the Day and Week fields support this character.|If either one of the Day and Week fields is specified, the other field must be set to a question mark \(`?`\) to avoid conflicts.|
|`L`|Indicates last. Only the Day of a month and Day of a week fields support this character. **Note:** Do not specify a list or range when you use the `L` character to avoid a logic error.

|-   In the Day of a month field, `L` indicates the last day of the month. In the Day of a week field, `L` indicates the last day of a week, which is Sunday \(`SUN`\).
-   `L` can be preceded by a value. For example, `6L` in the Day of a week field indicates the last Saturday of a month. |
|`W`|The weekday nearest to the specified day of the month. The weekday that the `W` character finalizes on is in the same month as the given day. `LW` indicates the last weekday of the specified month.|If `5W` is specified in the Day of a month field and the 5th day of the month falls on Saturday, the task is triggered on the nearest weekday Friday, which is the 4th day of the month. If the 5th day of the month falls on Sunday, the task is triggered on the nearest weekday Monday, which is the 6th day of the month. If the 5th day of the month falls on a weekday, the task is triggered on the 5th day of the month.|
|`#`|A specific day of a specific week in every month. Only the Day of a week field supports this character.|In the Day of a week field, `4#2` indicates the 2nd Thursday of a month.|

## Examples

The following table lists some sample values of cron expressions.

|Example|Description|
|-------|-----------|
|`0 15 10 ? * *`|Performs the task at 10:15 every day.|
|`0 15 10 * * ?`|Performs the task at 10:15 every day.|
|`0 0 12 * * ?`|Performs the task at 12:00 every day.|
|`0 0 10,14,16 * * ?`|Performs the task at 10:00, 14:00, and 16:00 every day.|
|`0 0/30 9-17 * * ?`|Performs the task once every half an hour between 09:00 and 17:00 every day.|
|`0 * 14 * * ?`|Performs the task once every minute between 14:00 and 14:59 every day.|
|`0 0-5 14 * * ?`|Performs the task once every minute between 14:00 and 14:05 every day.|
|`0 0/5 14 * * ?`|Performs the task once every five minutes between 14:00 and 14:55 every day.|
|`0 0/5 14,18 * * ?`|Performs the task once every five minutes between 14:00 and 14:55 and between 18:00 and 18:55 every day.|
|`0 0 12 ? * WED`|Performs the task at 12:00 every Wednesday.|
|`0 15 10 15 * ?`|Performs the task at 10:15 on the 15th day of every month.|
|`0 15 10 L * ?`|Performs the task at 10:15 on the last day of every month.|
|`0 15 10 ? * 6L`|Perform the task at 10:15 on the last Saturday of every month.|
|`0 15 10 ? * 6#3`|Perform the task at 10:15 on the third Saturday of every month.|
|`0 10,44 14 ? 3 WED`|Performs the task between 14:10 and 14:44 every Wednesday in March every year.|

**Related topics**  


[InvokeCommand](/intl.en-US/API Reference/Cloud assistant/InvokeCommand.md)

[RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md)

