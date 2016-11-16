# Create an end-user Linux account named with your GitHub handle
# Create a home HDFS directory for this user as well

[ec2-user@ip-172-31-21-229 ~]$ sudo ls /home/roedelk/
[ec2-user@ip-172-31-21-229 ~]$ sudo -u hdfs hadoop fs -ls /user
[ec2-user@ip-172-31-21-229 ~]$ sudo -u hdfs hadoop fs -mkdir /user/roedelk
[ec2-user@ip-172-31-21-229 ~]$ sudo su - roedelk

# Delete the output directory
hadoop fs -rm -r -f -skipTrash /benchmarks/streaming-21/hduser1/terasort/terasort-input

# Run teragen
time hadoop jar \
/usr/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar \
teragen \
-Ddfs.blocksize=512M \
-Dio.file.buffer.size=131072 \
-Dmapreduce.map.java.opts=-Xmx1536m \
-Dmapreduce.map.memory.mb=2048 \
-Dmapreduce.task.io.sort.mb=256 \
-Dyarn.app.mapreduce.am.resource.mb=1024 \
-Dmapred.map.tasks=64 \
10000000000  \
/benchmarks/streaming-21/hduser1/terasort/terasort-input

# Create a 10 GB file using teragen
#        Set the number of mappers to four
#        Limit the block size to 32 MB
#        Land the result under your user's home directory
#        Use the time command to report the job's duration

[ec2-user@ip-172-31-21-227 jars]$ time sudo -u hdfs /usr/bin/hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -Ddfs.blocksize=32M -Dmapred.map.tasks=4 100000000 /opt/tera_bench/

16/11/16 10:33:15 INFO mapreduce.Job: Job job_1479307032108_0002 completed successfully
16/11/16 10:33:15 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=486228
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=344
                HDFS: Number of bytes written=10000000000
                HDFS: Number of read operations=16
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=8
        Job Counters
                Launched map tasks=4
                Other local map tasks=4
                Total time spent by all maps in occupied slots (ms)=469729
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=469729
                Total vcore-seconds taken by all map tasks=469729
                Total megabyte-seconds taken by all map tasks=481002496
        Map-Reduce Framework
                Map input records=100000000
                Map output records=100000000
                Input split bytes=344
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=1062
                CPU time spent (ms)=151810
                Physical memory (bytes) snapshot=1097105408
                Virtual memory (bytes) snapshot=6238437376
                Total committed heap usage (bytes)=868220928
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=214760662691937609
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=10000000000

real    2m11.980s
user    0m6.040s
sys     0m0.451s


#    Run the terasort command on this file
#        Use the time command to report the job's duration
#        Land the result under your user's home directory

[ec2-user@ip-172-31-21-227 jars]$ time sudo -u hdfs /usr/bin/hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar terasort /opt/tera_bench /opt/tera_sort

16/11/16 10:43:16 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=4475232458
                FILE: Number of bytes written=8888336552
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=10000045300
                HDFS: Number of bytes written=10000000000
                HDFS: Number of read operations=924
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=16
        Job Counters
                Launched map tasks=300
                Launched reduce tasks=8
                Data-local map tasks=300
                Total time spent by all maps in occupied slots (ms)=2766667
                Total time spent by all reduces in occupied slots (ms)=673435
                Total time spent by all map tasks (ms)=2766667
                Total time spent by all reduce tasks (ms)=673435
                Total vcore-seconds taken by all map tasks=2766667
                Total vcore-seconds taken by all reduce tasks=673435
                Total megabyte-seconds taken by all map tasks=2833067008
                Total megabyte-seconds taken by all reduce tasks=689597440
        Map-Reduce Framework
                Map input records=100000000
                Map output records=100000000
                Map output bytes=10200000000
                Map output materialized bytes=4375203216
                Input split bytes=45300
                Combine input records=0
                Combine output records=0
                Reduce input groups=100000000
                Reduce shuffle bytes=4375203216
                Reduce input records=100000000
                Reduce output records=100000000
                Spilled Records=200000000
                Shuffled Maps =2400
                Failed Shuffles=0
                Merged Map outputs=2400
                GC time elapsed (ms)=33720
                CPU time spent (ms)=1440600
                Physical memory (bytes) snapshot=146792189952
                Virtual memory (bytes) snapshot=482213564416
                Total committed heap usage (bytes)=174872068096
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=10000000000
        File Output Format Counters
                Bytes Written=10000000000
16/11/16 10:43:16 INFO terasort.TeraSort: done

real    5m20.999s
user    0m9.543s
sys     0m0.407s


#    Report your work in storage/labs/1_terasort_tests.md, including:
#        The full teragen and terasort commands you used
#        The time result of each job

hadoop jar /usr/lib/gphd/hadoop-mapreduce/hadoop-mapreduce-examples.jar teravalidate -D mapred.reduce.tasks=8 /teraOutput /teraValidate


[roedelk@ip-172-31-21-227 ~]$ time /usr/bin/hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -Ddfs.blocksize=32M -Dmapred.map.tasks=4 100000 /user/roedelk/tera_gen/
