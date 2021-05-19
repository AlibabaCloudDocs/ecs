# Database overview

A database is a collection of data that is stored together in a specific manner. Databases are independent of applications. Data in databases is least redundant and can be shared. A database can be regarded as an electronic filing cabinet on which you can perform operations such as add, query, update, and delete.

## Common databases

Alibaba Cloud provides the high-availability ApsaraDB RDS database architecture. However, ApsaraDB RDS may not meet the requirements of some production environments, such as the scenarios that require Oracle and SQL Server databases. In this case, you can build a database on an Elastic Compute Service \(ECS\) instance.

Typically, three types of databases are used:

-   Oracle
    -   Oracle provides a high degree of hardware stability. It can run on a variety of hardware and operating system platforms, from desktop computers to mainframes and supercomputers. Oracle supports symmetric multiprocessors, cluster multiprocessors, and large-scale processors, and works with multiple languages.
    -   Oracle is a multi-user system that can automatically recover from system failures in batch processing or online environments. Oracle provides a complete software development tool Oracle Developer/2000 that consists of an interactive application generator, report printing software, word processing software, and a centralized data dictionary. You can use these components to generate your own applications.
    -   Oracle presents data in two-dimensional tables, and provides Structured Query Language \(SQL\) to implement basic database management functions such as data query, modification, definition, and control.
    -   Data in Oracle databases can be smoothly migrated. The communication feature provided by Oracle allows programs on microcomputers to receive data from or transfer data to Oracle databases on minicomputers and mainframes.
    -   Oracle is a large-scale database system. It is suitable for small, medium, and large application systems and can serve both the client and server sides of server systems.
-   SQL Server

    SQL Server is a relational database system provided by Microsoft. It is a scalable, high-performance database management system and designed for distributed clients and server computing. SQL Server works with Windows New Technology \(Windows NT\) to provide a transaction-based enterprise-level information management solution. Versions earlier than SQL Server 2016 can run only on Windows.

-   MySQL

    MySQL is an open source relational database management system \(RDBMS\) and uses the most common database management language SQL. MySQL databases can be used across platforms such as Linux and Windows.


## Deployment methods

You can manually deploy a MySQL database.

-   [Manually deploy a MySQL database on Windows](/intl.en-US/Tutorials/Build an application/Deploy databases based on ECS/Manually deploy a MySQL database on Windows.md)
-   [Manually deploy a MySQL database on an ECS instance that runs Alibaba Cloud Linux 2](/intl.en-US/Tutorials/Build an application/Deploy databases based on ECS/Manually deploy a MySQL database on an ECS instance that runs Alibaba Cloud Linux
         2.md)
-   [Manually deploy a MySQL database on an ECS instance that runs CentOS 8](/intl.en-US/Tutorials/Build an application/Deploy databases based on ECS/Manually deploy a MySQL database on an ECS instance that runs CentOS 8.md)
-   [Manually deploy a MySQL database on an instance running CentOS 7](/intl.en-US/Tutorials/Build an application/Deploy databases based on ECS/Manually deploy a MySQL database on an instance running CentOS 7.md)

## Back up databases

You can use Hybrid Backup Recovery \(HBR\) to back up databases from ECS instances and restore the files based on your requirements. References:

-   [Information about the versions and features of various databases](/intl.en-US/Back up ECS/ECS database backup/Overview.md)
-   [Prepare for a MySQL data backup](/intl.en-US/Back up ECS/ECS database backup/MySQL backup/Prepare for a data backup.md)
-   [Prepare for an Oracle data backup](/intl.en-US/Back up ECS/ECS database backup/Oracle backup/Prepare for a data backup.md)
-   [Prepare for a SQL Server data backup](/intl.en-US/Back up ECS/ECS database backup/SQL Server backup/Prepare for a data backup.md)

