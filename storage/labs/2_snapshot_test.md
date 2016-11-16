HDFS Lab: Test HDFS Snapshots

# List the commands and output for each step below in storage/labs/2_snapshot_test.md.
#    Create a precious directory in HDFS; copy the ZIP course file into it.
[ec2-user@ip-172-31-21-227 ~]$ sudo -u hdfs hdfs dfs -mkdir /opt/precious
[ec2-user@ip-172-31-21-227 ~]$ sudo -u hdfs hdfs dfs -put /opt/SEBC-master.zip /opt/precious/
[ec2-user@ip-172-31-21-227 ~]$ sudo -u hdfs hadoop fs -ls /opt/precious
Found 1 items
-rw-r--r--   3 hdfs supergroup     410158 2016-11-16 18:10 /opt/precious/SEBC-master.zip
#
#    Enable snapshots for precious
[ec2-user@ip-172-31-21-227 ~]$ sudo -u hdfs hdfs dfsadmin -allowSnapshot /opt/precious
Allowing snaphot on /opt/precious succeeded
#
#    Create a snapshot called sebc-hdfs-test
[ec2-user@ip-172-31-21-227 ~]$ sudo -u hdfs hdfs dfs -createSnapshot /opt/precious/ sebc-hdfs-test
Created snapshot /opt/precious/.snapshot/sebc-hdfs-test
#
#    Delete the ZIP file
[ec2-user@ip-172-31-21-227 ~]$ sudo -u hdfs hdfs dfs -rm -r -f -skipTrash /opt/precious/SEBC-master.zip
Deleted /opt/precious/SEBC-master.zip

#    Delete the directory
[ec2-user@ip-172-31-21-227 ~]$ sudo -u hdfs hdfs dfs -rm -r -f -skipTrash /opt/precious/
rm: The directory /opt/precious cannot be deleted since /opt/precious is snapshottable and already has snapshots

[ec2-user@ip-172-31-21-227 ~]$ sudo -u hdfs hdfs dfs -ls /opt/precious/.snapshot
Found 1 items
drwxr-xr-x   - hdfs supergroup          0 2016-11-16 18:13 /opt/precious/.snapshot/sebc-hdfs-test

#    Restore the deleted file
[ec2-user@ip-172-31-21-227 ~]$ sudo -u hdfs hdfs dfs -cp -ptopax /opt/precious/.snapshot/sebc-hdfs-test /user/ec2-user
[ec2-user@ip-172-31-21-227 ~]$ sudo -u hdfs hdfs dfs -ls /user/ec2-user
Found 1 items
-rw-r--r--   3 hdfs supergroup     410158 2016-11-16 18:10 /user/ec2-user/SEBC-master.zip

#    Capture the NameNode web UI screen that lists snapshots in storage/labs/2_snapshot_list.png.

    
    
    
HDFS Lab: Enable HDFS HA

    Use the Cloudera Manager wizard to enable HA
        Once configured, get a screenshot of the HDFS Instances tab
            Name the file storage/3_HDFS_HA.png
    Add a CM user and name it with your GitHub handle
        Assign the Full Administrator role to this user
        Assign the password cloudera to this user
        Re-assign the admin user to the Limited Operator role
        Take a screenshot of your users page; save it to storage/labs/4_CM_users.png
        In an Issue comment, post the URL to your Cloudera Manager instance
