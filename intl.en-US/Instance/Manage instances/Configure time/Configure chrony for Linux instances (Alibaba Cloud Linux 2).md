# Configure chrony for Linux instances \(Alibaba Cloud Linux 2\)

This topic describes how to modify the time zone of a Linux instance and how to enable, configure, and use chrony to ensure that the local system time of the instance is synchronized precisely with the standard time. An instance that runs an Alibaba Cloud Linux 2.1903 LTS 64-bit operating system is used in the examples.

An inbound rule is added to a security group of the ECS instance to allow traffic on UDP port 123. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

Alibaba Cloud Linux 2 uses chrony to synchronize local system time with the standard time. chrony consists of the following core programs:

-   chronyd is a daemon process that runs in the background. chronyd is used to adjust the system clock that runs in the kernel to synchronize with the clock server. chronyd calculates the offset of the system time relative to the standard time, and adjusts the system time accordingly.
-   chronyc provides a user interface to monitor the performance of chronyd and fine-tunes parameters in chronyd. chronyc can run on a server controlled by chronyd or a different remote server.

For more information, visit [Chrony](https://chrony.tuxfamily.org/index.html).

## Modify the time zone of a Linux instance

1.  Connect to the instance. For more information,see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

2.  Run the following command to view the time zone list:

    ```
    ls /usr/share/zoneinfo/<Name of the time zone folder>
    ```

    For example, you can run the following command to view the `Hong_Kong` time zone in the list:

    ```
    ls /usr/share/zoneinfo/Asia
    ```

3.  Run the following command to modify the time zone:

    ```
    ln -sf /usr/share/zoneinfo/Asia/Hong-Kong /etc/localtime
    ```

4.  Run the following command to update the real-time clock \(RTC\):

    ```
    hwclock -w
    ```

5.  Run the following command to check the time zone:

    ```
    timedatectl status
    ```

    If a command output similar to the following one is displayed, the time zone is changed to `Hong_Kong`:

    ```
          Local time: -- 2020-09-14 08:00:04 UTC
      Universal time:-- 2020-09-14 08:00:04 UTC
            RTC time: -- 2020-09-14 08:00:04
           Time zone: Asia/Hong-Kong (UTC, +0000)
    ```


## Enable chrony

1.  Connect to the instance. For more information,see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

2.  Run the following commands to start the chronyd service and configure it to run on system startup:

    ```
    systemctl start chronyd.service
    systemctl enable chronyd.service
    ```

3.  Run the following command to view the time synchronization status of the instance to check whether the service is started:

    ```
    chronyc tracking
    ```

4.  Run the following command to view the list of servers that have chrony enabled:

    ```
    chronyc -n sources -v
    ```


## Configure chrony

1.  Connect to the instance. For more information,see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

2.  Run the following command to open the configuration file of chrony:

    ```
    vim /etc/chrony.conf
    ```

3.  Find `server <NTP server> minpoll 4 maxpoll 10 iburst` and press the I key to edit the file. Add `#` at the beginnings of sentences that contain the NTP servers that you want to hide.

4.  Add a row of NTP server information in the `server <Required NTP server> minpoll 4 maxpoll 10 iburst` format. Then, press the Esc key and enter `:wq` to save the file and exit.

    For more information about NTP servers, see [Alibaba Cloud NTP server](/intl.en-US/Instance/Manage instances/Configure time/Alibaba Cloud NTP server.md).

5.  Run the following commands to start the chronyd service and configure it to run on system startup:

    ```
    systemctl start chronyd.service
    systemctl enable chronyd.service
    ```

6.  Run the following command to view the list of servers that have chrony enabled:

    ```
    chronyc -n sources -v
    ```


## Manually synchronize the clock by using chrony

1.  Run the following command to access chrony:

    ```
    chronyc
    ```

2.  In chrony, run the following command to synchronize the clock:

    ```
    makestep
    ```

    **Note:** You can run the help command to obtain help about common chrony commands.


