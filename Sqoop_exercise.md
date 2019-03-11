<Exercise 1. list-tables>
-------------------------
**1. MySQL DB에 존재하는 table list를 Sqoop을 통해 조회**

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
[training@localhost ~]$ `


<Exercise 2. import>
-------------------------
**1. MySQL DB에 존재하는 특정 table data를 Sqoop을 통해 HDFS로 import**

`[training@localhost ~]$ sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training --table basestations --target-dir /loudacre/basestations_import --null-non-string '\\N'
19/03/10 21:13:40 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0
19/03/10 21:13:40 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/03/10 21:13:40 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
19/03/10 21:13:40 INFO tool.CodeGenTool: Beginning code generation
19/03/10 21:13:41 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `basestations` AS t LIMIT 1
19/03/10 21:13:41 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `basestations` AS t LIMIT 1
19/03/10 21:13:41 INFO orm.CompilationManager: HADOOP_MAPRED_HOME is /usr/lib/hadoop-mapreduce
Note: /tmp/sqoop-training/compile/119e1dfd8dc96d3ae36bb2beee92fbdb/basestations.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
19/03/10 21:13:44 INFO orm.CompilationManager: Writing jar file: /tmp/sqoop-training/compile/119e1dfd8dc96d3ae36bb2beee92fbdb/basestations.jar
19/03/10 21:13:44 WARN manager.MySQLManager: It looks like you are importing from mysql.
19/03/10 21:13:44 WARN manager.MySQLManager: This transfer can be faster! Use the --direct
19/03/10 21:13:44 WARN manager.MySQLManager: option to exercise a MySQL-specific fast path.
19/03/10 21:13:44 INFO manager.MySQLManager: Setting zero DATETIME behavior to convertToNull (mysql)
19/03/10 21:13:44 INFO mapreduce.ImportJobBase: Beginning import of basestations
19/03/10 21:13:44 INFO Configuration.deprecation: mapred.job.tracker is deprecated. Instead, use mapreduce.jobtracker.address
19/03/10 21:13:44 INFO Configuration.deprecation: mapred.jar is deprecated. Instead, use mapreduce.job.jar
19/03/10 21:13:45 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
19/03/10 21:13:45 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
19/03/10 21:13:49 INFO db.DBInputFormat: Using read commited transaction isolation
19/03/10 21:13:49 INFO db.DataDrivenDBInputFormat: BoundingValsQuery: SELECT MIN(`station_num`), MAX(`station_num`) FROM `basestations`
19/03/10 21:13:49 INFO db.IntegerSplitter: Split size: 94; Num splits: 4 from: 1 to: 377
19/03/10 21:13:49 INFO mapreduce.JobSubmitter: number of splits:4
19/03/10 21:13:49 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1552277124392_0001
19/03/10 21:13:50 INFO impl.YarnClientImpl: Submitted application application_1552277124392_0001
19/03/10 21:13:50 INFO mapreduce.Job: The url to track the job: http://localhost:8088/proxy/application_1552277124392_0001/
19/03/10 21:13:50 INFO mapreduce.Job: Running job: job_1552277124392_0001
19/03/10 21:14:09 INFO mapreduce.Job: Job job_1552277124392_0001 running in uber mode : false
19/03/10 21:14:09 INFO mapreduce.Job:  map 0% reduce 0%
19/03/10 21:14:23 INFO mapreduce.Job:  map 25% reduce 0%
19/03/10 21:14:29 INFO mapreduce.Job:  map 50% reduce 0%
19/03/10 21:14:36 INFO mapreduce.Job:  map 75% reduce 0%
19/03/10 21:14:41 INFO mapreduce.Job:  map 100% reduce 0%
19/03/10 21:14:41 INFO mapreduce.Job: Job job_1552277124392_0001 completed successfully
19/03/10 21:14:41 INFO mapreduce.Job: Counters: 30
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=560556
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=477
		HDFS: Number of bytes written=14845
		HDFS: Number of read operations=16
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=8
	Job Counters 
		Launched map tasks=4
		Other local map tasks=4
		Total time spent by all maps in occupied slots (ms)=0
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=23299
		Total vcore-seconds taken by all map tasks=23299
		Total megabyte-seconds taken by all map tasks=5964544
	Map-Reduce Framework
		Map input records=377
		Map output records=377
		Input split bytes=477
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=407
		CPU time spent (ms)=2930
		Physical memory (bytes) snapshot=494170112
		Virtual memory (bytes) snapshot=8248905728
		Total committed heap usage (bytes)=251920384
	File Input Format Counters 
		Bytes Read=0
	File Output Format Counters 
		Bytes Written=14845
19/03/10 21:14:41 INFO mapreduce.ImportJobBase: Transferred 14.4971 KB in 56.0631 seconds (264.791 bytes/sec)
19/03/10 21:14:41 INFO mapreduce.ImportJobBase: Retrieved 377 records.
[training@localhost ~]$ 
`

**2. Import받은 테이블 데이터를 HDFS상에서 조회**

`[training@localhost ~]$ hdfs dfs -ls /loudacre/basestations_import
Found 5 items
-rw-rw-rw-   1 training supergroup          0 2019-03-10 21:14 /loudacre/basestations_import/_SUCCESS
-rw-rw-rw-   1 training supergroup       3639 2019-03-10 21:14 /loudacre/basestations_import/part-m-00000
-rw-rw-rw-   1 training supergroup       3791 2019-03-10 21:14 /loudacre/basestations_import/part-m-00001
-rw-rw-rw-   1 training supergroup       3681 2019-03-10 21:14 /loudacre/basestations_import/part-m-00002
-rw-rw-rw-   1 training supergroup       3734 2019-03-10 21:14 /loudacre/basestations_import/part-m-00003
`

**3. Import받은 테이블 정보에 대한 개별파일 내용조회**

`[training@localhost ~]$ hdfs dfs -cat /loudacre/basestations_import/part-m-00000
1,86502,Chambers,AZ,35.2375,-109.523
2,86514,Teec Nos Pos,AZ,36.7797,-109.359
3,85602,Benson,AZ,31.9883,-110.294
4,86011,Flagstaff,AZ,35.6308,-112.052
5,86016,Gray Mountain,AZ,35.6308,-112.052
6,86018,Parks,AZ,35.2563,-111.95
.....
`

**4. Import받은 테이블 정보를 Linux시스템으로 가져오기**

`[training@localhost ~]$ hdfs dfs -getmerge /loudacre/basestations_import/ ./temp_file.txt
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
`

**5. Import table using an alternate file format(Parquet)**

`
[training@localhost ~]$ sqoop import \
> --connect jdbc:mysql://localhost/loudacre \
> --username training --password training \
> --table basestations \
> --target-dir /loudacre/basestations_import_parquet \
> --as-parquetfile
19/03/10 21:26:20 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0
19/03/10 21:26:20 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/03/10 21:26:20 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
19/03/10 21:26:20 INFO tool.CodeGenTool: Beginning code generation
19/03/10 21:26:20 INFO tool.CodeGenTool: Will generate java class as codegen_basestations
19/03/10 21:26:21 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `basestations` AS t LIMIT 1
19/03/10 21:26:21 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `basestations` AS t LIMIT 1
19/03/10 21:26:21 INFO orm.CompilationManager: HADOOP_MAPRED_HOME is /usr/lib/hadoop-mapreduce
Note: /tmp/sqoop-training/compile/041269c8f87f45f59ddfcab7b929c4c2/codegen_basestations.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
19/03/10 21:26:23 INFO orm.CompilationManager: Writing jar file: /tmp/sqoop-training/compile/041269c8f87f45f59ddfcab7b929c4c2/codegen_basestations.jar
19/03/10 21:26:23 WARN manager.MySQLManager: It looks like you are importing from mysql.
19/03/10 21:26:23 WARN manager.MySQLManager: This transfer can be faster! Use the --direct
19/03/10 21:26:23 WARN manager.MySQLManager: option to exercise a MySQL-specific fast path.
19/03/10 21:26:23 INFO manager.MySQLManager: Setting zero DATETIME behavior to convertToNull (mysql)
19/03/10 21:26:23 INFO mapreduce.ImportJobBase: Beginning import of basestations
19/03/10 21:26:23 INFO Configuration.deprecation: mapred.job.tracker is deprecated. Instead, use mapreduce.jobtracker.address
19/03/10 21:26:24 INFO Configuration.deprecation: mapred.jar is deprecated. Instead, use mapreduce.job.jar
19/03/10 21:26:25 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `basestations` AS t LIMIT 1
19/03/10 21:26:25 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `basestations` AS t LIMIT 1
19/03/10 21:26:26 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
19/03/10 21:26:26 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
19/03/10 21:26:29 INFO db.DBInputFormat: Using read commited transaction isolation
19/03/10 21:26:29 INFO db.DataDrivenDBInputFormat: BoundingValsQuery: SELECT MIN(`station_num`), MAX(`station_num`) FROM `basestations`
19/03/10 21:26:29 INFO db.IntegerSplitter: Split size: 94; Num splits: 4 from: 1 to: 377
19/03/10 21:26:29 INFO mapreduce.JobSubmitter: number of splits:4
19/03/10 21:26:29 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1552277124392_0002
19/03/10 21:26:29 INFO impl.YarnClientImpl: Submitted application application_1552277124392_0002
19/03/10 21:26:29 INFO mapreduce.Job: The url to track the job: http://localhost:8088/proxy/application_1552277124392_0002/
19/03/10 21:26:29 INFO mapreduce.Job: Running job: job_1552277124392_0002
19/03/10 21:26:39 INFO mapreduce.Job: Job job_1552277124392_0002 running in uber mode : false
19/03/10 21:26:39 INFO mapreduce.Job:  map 0% reduce 0%
19/03/10 21:26:47 INFO mapreduce.Job:  map 25% reduce 0%
19/03/10 21:26:54 INFO mapreduce.Job:  map 50% reduce 0%
19/03/10 21:27:00 INFO mapreduce.Job:  map 75% reduce 0%
19/03/10 21:27:07 INFO mapreduce.Job:  map 100% reduce 0%
19/03/10 21:27:07 INFO mapreduce.Job: Job job_1552277124392_0002 completed successfully
19/03/10 21:27:08 INFO mapreduce.Job: Counters: 30
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=565464
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=38777
		HDFS: Number of bytes written=24593
		HDFS: Number of read operations=272
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=40
	Job Counters 
		Launched map tasks=4
		Other local map tasks=4
		Total time spent by all maps in occupied slots (ms)=0
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=21496
		Total vcore-seconds taken by all map tasks=21496
		Total megabyte-seconds taken by all map tasks=5502976
	Map-Reduce Framework
		Map input records=377
		Map output records=377
		Input split bytes=477
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=395
		CPU time spent (ms)=5580
		Physical memory (bytes) snapshot=668753920
		Virtual memory (bytes) snapshot=8298037248
		Total committed heap usage (bytes)=251920384
	File Input Format Counters 
		Bytes Read=0
	File Output Format Counters 
		Bytes Written=0
19/03/10 21:27:08 INFO mapreduce.ImportJobBase: Transferred 24.0166 KB in 41.1801 seconds (597.206 bytes/sec)
19/03/10 21:27:08 INFO mapreduce.ImportJobBase: Retrieved 377 records.
`

**6. Check the contents of Parquet file using parquet-tools**

`[training@localhost ~]$ hdfs dfs -ls /loudacre/basestations_import_parquet/
Found 6 items
drwxrwxrwx   - training supergroup          0 2019-03-10 21:26 /loudacre/basestations_import_parquet/.metadata
drwxrwxrwx   - training supergroup          0 2019-03-10 21:27 /loudacre/basestations_import_parquet/.signals
-rw-rw-rw-   1 training supergroup       3828 2019-03-10 21:26 /loudacre/basestations_import_parquet/44044162-fea6-4b1b-b650-d5c191e0ea53.parquet
-rw-rw-rw-   1 training supergroup       3893 2019-03-10 21:27 /loudacre/basestations_import_parquet/5a9e87cc-6a67-46ed-8a9c-7cb1804bc29e.parquet
-rw-rw-rw-   1 training supergroup       3933 2019-03-10 21:26 /loudacre/basestations_import_parquet/907d2adc-e750-47d8-ad4f-510830089754.parquet
-rw-rw-rw-   1 training supergroup       4015 2019-03-10 21:26 /loudacre/basestations_import_parquet/dd0a8b52-3868-4416-bc89-57d2efe726bb.parquet`


`[training@localhost ~]$ parquet-tools head hdfs://localhost/loudacre/basestations_import_parquet/
station_num = 95
zipcode = 91311
city = Chatsworth
state = CA
latitude = 34.2583
longitude = -118.591

station_num = 96
zipcode = 91330
city = Northridge
state = CA
latitude = 33.7866
longitude = -118.299

station_num = 97
zipcode = 91351
city = Canyon Country
state = CA
latitude = 34.4262
longitude = -118.449

station_num = 98
zipcode = 91352
city = Sun Valley
state = CA
latitude = 34.2209
longitude = -118.37

station_num = 99
zipcode = 91355
city = Valencia
state = CA
latitude = 34.3985
longitude = -118.553`
