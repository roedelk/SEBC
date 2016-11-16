# Name a source directory after your GitHub handle
[ec2-user@ip-172-31-21-231]$ sudo mkdir /opt/data_exch
[ec2-user@ip-172-31-21-231]$ sudo chmod 777 /opt/data_exch/

# Name a target directory after your partner's GitHub handle

# Use teragen to create a 500 MB file
[ec2-user@ip-172-31-21-231]$ cd /opt/cloudera/parcels/CDH/jars
[ec2-user@ip-172-31-21-231]$ sudo -u hdfs /usr/bin/hadoop jar hadoop-examples.jar teragen 5000000 /opt/data_exch/

[ec2-user@ip-172-31-21-231 jars]$ sudo -u hdfs hadoop fs -ls /opt/data_exch/
Found 3 items
-rw-r--r--   3 hdfs supergroup         0 2016-11-16 05:17 /opt/data_exch/_SUCCESS
-rw-r--r--   3 hdfs supergroup 250000000 2016-11-16 05:17 /opt/data_exch/part-m-00000
-rw-r--r--   3 hdfs supergroup 250000000 2016-11-16 05:17 /opt/data_exch/part-m-00001

Username	Role					User Type
roedelk 	User Administrator 		Cloudera Manager 

# Copy your partner's file to your target directory
#    Let one partner use distCp on the command line
#    Let the other use BDR
    
[root@ip-172-31-21-228 ~]# sudo -u hdfs /usr/bin/hadoop distcp hdfs://52.59.219.89:8020/user/gioconte/terag_data /opt/incoming/terag_data
16/11/16 05:50:59 INFO tools.DistCp: Input Options: DistCpOptions{atomicCommit=false, syncFolder=false, deleteMissing=false, ignoreFailures=false, overwrite=false, skipCRC=false, blocking=true, numListstatusThreads=0, maxMaps=20, mapBandwidth=100, sslConfigurationFile='null', copyStrategy='uniformsize', preserveStatus=[], preserveRawXattrs=false, atomicWorkPath=null, logPath=null, sourceFileListing=null, sourcePaths=[hdfs://52.59.219.89:8020/user/gioconte/terag_data], targetPath=/opt/incoming/terag_data, targetPathExists=false, filtersFile='null'}
16/11/16 05:50:59 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-21-227.eu-central-1.compute.internal/172.31.21.227:8032
16/11/16 05:51:00 INFO tools.SimpleCopyListing: Paths (files+dirs) cnt = 3; dirCnt = 1
16/11/16 05:51:00 INFO tools.SimpleCopyListing: Build file listing completed.
16/11/16 05:51:00 INFO Configuration.deprecation: io.sort.mb is deprecated. Instead, use mapreduce.task.io.sort.mb
16/11/16 05:51:00 INFO Configuration.deprecation: io.sort.factor is deprecated. Instead, use mapreduce.task.io.sort.factor
16/11/16 05:51:00 INFO tools.DistCp: Number of paths in the copy list: 3
16/11/16 05:51:00 INFO tools.DistCp: Number of paths in the copy list: 3
16/11/16 05:51:00 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-21-227.eu-central-1.compute.internal/172.31.21.227:8032
16/11/16 05:51:00 INFO mapreduce.JobSubmitter: number of splits:2
16/11/16 05:51:01 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1479284596614_0003
16/11/16 05:51:01 INFO impl.YarnClientImpl: Submitted application application_1479284596614_0003
16/11/16 05:51:01 INFO mapreduce.Job: The url to track the job: http://ip-172-31-21-227.eu-central-1.compute.internal:8088/proxy/application_1479284596614_0003/
16/11/16 05:51:01 INFO tools.DistCp: DistCp job-id: job_1479284596614_0003
16/11/16 05:51:01 INFO mapreduce.Job: Running job: job_1479284596614_0003
16/11/16 05:51:08 INFO mapreduce.Job: Job job_1479284596614_0003 running in uber mode : false
16/11/16 05:51:08 INFO mapreduce.Job:  map 0% reduce 0%
16/11/16 05:51:16 INFO mapreduce.Job:  map 50% reduce 0%
16/11/16 05:51:21 INFO mapreduce.Job:  map 100% reduce 0%

# Activated
sudo -u hdfs /usr/bin/hadoop distcp webhdfs://52.59.219.89:14000/user/gioconte/terag_data /opt/incoming/terag_data

# Browse the results
[root@ip-172-31-21-228 ~]# sudo -u hdfs hadoop fs -ls /opt/incoming/terag_data/terag_data
Found 2 items
-rw-r--r--   3 hdfs supergroup          0 2016-11-16 09:44 /opt/incoming/terag_data/terag_data/_SUCCESS
-rw-r--r--   3 hdfs supergroup  500000000 2016-11-16 09:44 /opt/incoming/terag_data/terag_data/part-m-00000

# Use hdfs fsck <path> -files -blocks on your source and target directories
[root@ip-172-31-21-228 ~]# sudo -u hdfs hdfs fsck /opt/incoming/terag_data/terag_data/ -files -blocks
Connecting to namenode via http://ip-172-31-21-227.eu-central-1.compute.internal:50070
FSCK started by hdfs (auth:SIMPLE) from /172.31.21.228 for path /opt/incoming/terag_data/terag_data/ at Wed Nov 16 10:06:01 EST 2016
/opt/incoming/terag_data/terag_data/ <dir>
/opt/incoming/terag_data/terag_data/_SUCCESS 0 bytes, 0 block(s):  OK

/opt/incoming/terag_data/terag_data/part-m-00000 500000000 bytes, 4 block(s):  OK
0. BP-661477297-172.31.21.227-1479284537975:blk_1073743322_2498 len=134217728 Live_repl=3
1. BP-661477297-172.31.21.227-1479284537975:blk_1073743324_2500 len=134217728 Live_repl=3
2. BP-661477297-172.31.21.227-1479284537975:blk_1073743325_2501 len=134217728 Live_repl=3
3. BP-661477297-172.31.21.227-1479284537975:blk_1073743326_2502 len=97346816 Live_repl=3

Status: HEALTHY
 Total size:    500000000 B
 Total dirs:    1
 Total files:   2
 Total symlinks:                0
 Total blocks (validated):      4 (avg. block size 125000000 B)
 Minimally replicated blocks:   4 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          4
 Number of racks:               1
FSCK ended at Wed Nov 16 10:06:01 EST 2016 in 2 milliseconds

The filesystem under path '/opt/incoming/terag_data/terag_data/' is HEALTHY
