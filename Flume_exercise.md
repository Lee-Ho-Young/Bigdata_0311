**통신QM Unit 이호영 선임(09340)**

<Exercise>
-------------------------
**1. Create a new flume configuration file with the following**

 - Source
    - Type : Netcat
    - Bind : localhost
    - Port : 44444
 - Channel
    - Type : Memory
    - Capacity : 1000
    - transactionCapacity : 100
 - Sink
    - logger
   
```

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
```
