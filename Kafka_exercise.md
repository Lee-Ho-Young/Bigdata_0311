**통신QM Unit 이호영 선임(09340)**

<Exercise 1. list-tables>
-------------------------
**1. MySQL DB에 존재하는 table list를 Sqoop을 통해 조회**

```
[training@localhost ~]$ sqoop list-tables \
--connect jdbc:mysql://localhost/loudacre \
--username training --password training
19/03/10 21:08:51 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0
19/03/10 21:08:51 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/03/10 21:08:52 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
accountdevice
accounts
basestations
customerservicerep
device
knowledgebase
mostactivestations
webpage
[training@localhost ~]$
```

<Exercise 2. import>
-------------------------
**1. MySQL DB에 존재하는 특정 table data를 Sqoop을 통해 HDFS로 import**

```
[training@localhost ~]$ sqoop import \
--connect jdbc:mysql://localhost/loudacre \
--username training --password training \
--table basestations \
--target-dir /loudacre/basestations_import \
--null-non-string '\\N'
```
