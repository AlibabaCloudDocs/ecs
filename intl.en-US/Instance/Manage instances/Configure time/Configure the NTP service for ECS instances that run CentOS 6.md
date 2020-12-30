---
keyword: [Alibaba Cloud, ECS, time calibration, time zone]
---

# Configure the NTP service for ECS instances that run CentOS 6

This topic describes how to change the time zone of a Linux instance, and how to enable and configure the Network Time Protocol \(NTP\) service to ensure that the local time for ECS instances is precisely synchronized. CentOS 6.5 is used in this topic.

The NTP service uses UDP port 123 for communication. Before you configure the NTP service, make sure that UDP port 123 is enabled. You can run the `netstat -nupl` command to check whether UDP port 123 is enabled. For more information about how to allow traffic on UDP port 123, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

By default, ECS instances in all Alibaba Cloud regions use UTC+8. You can configure or change time zones for your instances.

The NTP service ensures that the local time for ECS instances is synchronized with the standard time. In Linux, you can run the ntpdate or ntpd command to synchronize the system clock to an NTP server. This topic describes the standard and custom NTP service configurations. You can choose one based on your requirements. For more information, see the "Internal and public NTP servers" section in [Alibaba Cloud NTP server](/intl.en-US/Instance/Manage instances/Configure time/Alibaba Cloud NTP server.md).

-   `ntpdate` performs a one-time-only update to the system clock. For newly purchased instances, you can use `ntpdate` to synchronize time.
-   `ntpd` adjusts the system clock in small steps. For instances with running workloads, we recommend that you use `ntpd` to synchronize time.

## Modify the time zone of a Linux instance

1.  Connect to the Linux instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

    **Note:** You must open and edit the time zone configuration file as a root user. The `sudo` command is used in this example.

2.  Run the `sudo rm /etc/localtime` command to delete the local time URL in the system.

3.  Run the `sudo vi /etc/sysconfig/clock` command to use vim to open and edit the /etc/sysconfig/clock configuration file.

4.  Enter `i` to add a time zone city. For example, you can add `Zone=Asia/Shanghai`, press the Esc key to exit the edit mode, and then enter `:wq` to save and exit.

    You can run the `ls /usr/share/zoneinfo` command to query the list of time zones. `Shanghai` is included in the list of time zones.

5.  Run the `sudo ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime` command to update the time zone change.

6.  Run the `hwclock -w` command to update the real-time clock \(RTC\).

7.  Run the `sudo reboot` command to restart the instance.

8.  Run the `date -R` command to check whether the time zone change takes effect. If the change does not take effect, repeat the preceding operations.


## Enable the standard NTP service

1.  Connect to the Linux instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the `sudo service ntpd start` command to enable the NTP service.

3.  Run the `chkconfig ntpd on` command to enable the NTP service to run upon startup.

4.  Run the `ntpstat` command to check whether the NTP service is enabled.

5.  Run the `ntpq -p` command to view the list of NTP peers and run the `sudo chkconfig --list ntpd` command to view the run level for the NTP service.


## Configure the custom NTP service

1.  Connect to the Linux instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the `sudo vi /etc/ntp.conf` command to use vim to open and edit the configuration file of the NTP service.

3.  Find the `server ntp server iburst` information and enter `i` to start to edit the file. For NTP servers that you do not need, you can add a number sign \(`#`\) at the beginning of the lines to hide the servers.

4.  Add a new line of NTP server information in the following format: `server <the NTP server that you want to add> iburst`. After you edit the file, press the Esc key and enter `:wq` to save the file and exit.

5.  Run the `sudo service ntpd start` command to enable the custom NTP service.

6.  Run the `chkconfig ntpd on` command to enable the custom NTP service to run upon startup.

7.  Run the `ntpstat` command to check whether the NTP service is enabled.


**Related topics**  


[Alibaba Cloud NTP server](/intl.en-US/Instance/Manage instances/Configure time/Alibaba Cloud NTP server.md)

[Configure the NTP service for Windows instances](/intl.en-US/Instance/Manage instances/Configure time/Configure the NTP service for Windows instances.md)

