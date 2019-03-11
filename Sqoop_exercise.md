<Exercise 1. list-tables>
-------------------------
1. MySQL DB에 존재하는 table list를 Sqoop을 통해 조회

`[training@localhost ~]$ sqoop list-tables --connect jdbc:mysql://localhost/loudacre --username training --password training
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
`

<Exercise 2. import>
[training@localhost ~]$ sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training --table basestations --target-dir /loudacre/basestations_import --null-non-string '\\N'
.....
19/03/10 21:14:41 INFO mapreduce.ImportJobBase: Transferred 14.4971 KB in 56.0631 seconds (264.791 bytes/sec)
19/03/10 21:14:41 INFO mapreduce.ImportJobBase: Retrieved 377 records.
.....
[training@localhost ~]$ hdfs dfs -ls /loudacre/basestations_import
Found 5 items
-rw-rw-rw-   1 training supergroup          0 2019-03-10 21:14 /loudacre/basestations_import/_SUCCESS
-rw-rw-rw-   1 training supergroup       3639 2019-03-10 21:14 /loudacre/basestations_import/part-m-00000
-rw-rw-rw-   1 training supergroup       3791 2019-03-10 21:14 /loudacre/basestations_import/part-m-00001
-rw-rw-rw-   1 training supergroup       3681 2019-03-10 21:14 /loudacre/basestations_import/part-m-00002
-rw-rw-rw-   1 training supergroup       3734 2019-03-10 21:14 /loudacre/basestations_import/part-m-00003
.....
[training@localhost ~]$ hdfs dfs -cat /loudacre/basestations_import/part-m-00000
1,86502,Chambers,AZ,35.2375,-109.523
2,86514,Teec Nos Pos,AZ,36.7797,-109.359
3,85602,Benson,AZ,31.9883,-110.294
4,86011,Flagstaff,AZ,35.6308,-112.052
5,86016,Gray Mountain,AZ,35.6308,-112.052
6,86018,Parks,AZ,35.2563,-111.95
.....
[training@localhost ~]$ hdfs dfs -getmerge /loudacre/basestations_import/ ./temp_file.txt
[training@localhost ~]$ ll
total 80
-rw-rw-r-- 1 training training 19261 Mar 10 21:13 basestations.java
drwxr-xr-x 2 training training  4096 Nov 14  2016 Desktop
drwxr-xr-x 2 training training  4096 Sep 22  2016 Documents
drwxr-xr-x 2 training training  4096 Sep 22  2016 Downloads
drwxr-xr-x 8 training training  4096 May 25  2015 eclipse
drwxr-xr-x 2 training training  4096 Sep 22  2016 Music
drwxr-xr-x 2 training training  4096 Sep 22  2016 Pictures
drwxr-xr-x 2 training training  4096 Sep 22  2016 Public
-rw-rw-rw- 1 training training 14845 Mar 10 21:22 temp_file.txt
drwxr-xr-x 2 training training  4096 Sep 22  2016 Templates
drwxr-xr-x 4 training training  4096 Nov 14  2016 training_materials
drwxr-xr-x 2 training training  4096 Sep 22  2016 Videos
drwxr-xr-x 9 training training  4096 Oct 27  2016 workspace



