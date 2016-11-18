# Adapt repository 
wget http://archive.cloudera.com/cm5/redhat/6/x86_64/cm/cloudera-manager.repo -O /etc/yum.repos.d/cloudera-manager.repo
>> change in "baseurl" 5 -> 5.7.4
sudo cp cloudera-manager.repo /etc/yum.repos.d/cloudera-manager.repo
sudo yum update yum
sudo yum install oracle-j2sdk1.7
sudo ln -s /usr/share/java/mysql-connector-java-5.1.40-bin.jar /usr/java/jdk1.7.0_67-cloudera/lib/mysql-connector.jar
sudo yum install cloudera-manager-daemons cloudera-manager-server

export JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera/
export PATH="$PATH:/usr/java/jdk1.7.0_67-cloudera/bin"

[ec2-user@ip-172-31-23-171 ~]$ ll /etc/yum.repos.d
total 36
-rw-r--r--. 1 root root  294 Nov 18 04:03 cloudera-manager.repo
-rw-r--r--. 1 root root 1414 Sep 12 06:32 mysql-community.repo
-rw-r--r--. 1 root root 1440 Sep 12 06:32 mysql-community-source.repo
-rw-r--r--. 1 root root  358 Jul 14  2015 redhat.repo
-rw-r--r--. 1 root root  606 Nov 18 01:33 redhat-rhui-client-config.repo
-rw-r--r--. 1 root root 6300 Nov 18 01:33 redhat-rhui.repo
-rw-r--r--. 1 root root  529 Jun 12  2015 rhel-source.repo
-rw-r--r--. 1 root root   86 Nov 18 01:33 rhui-load-balancers.conf


# Configure Cloudera Manager

## Grant scm access to your MySQL server only from the CM node (no host wildcard)    
GRANT ALL PRIVILEGES ON scm.* TO 'scm'@'ip-172-31-23-171.eu-central-1.compute.internal';
mysql> show grants for scm@'ip-172-31-23-171.eu-central-1.compute.internal';
+-------------------------------------------------------------------------------------------+
| Grants for scm@ip-172-31-23-171.eu-central-1.compute.internal                             |
+-------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'scm'@'ip-172-31-23-171.eu-central-1.compute.internal'              |
| GRANT ALL PRIVILEGES ON `scm`.* TO 'scm'@'ip-172-31-23-171.eu-central-1.compute.internal' |
+-------------------------------------------------------------------------------------------+

## Copy your full scm_prepare_database.sh command and output into the same file
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
sudo /usr/share/cmf/schema/scm_prepare_database.sh -u root -p -h ip-172-31-23-172.eu-central-1.compute.internal mysql scm scm scm

[ec2-user@ip-172-31-23-172 ~]$ sudo /usr/share/cmf/schema/scm_prepare_database.sh -u root -p mysql scm scm scm
Enter database password:
JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.7.0_67-cloudera/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
2016-11-18 05:13:00,581 [main] INFO  com.cloudera.enterprise.dbutil.DbCommandExecutor  - Successfully connected to database.
All done, your SCM database is configured correctly!

sudo service cloudera-scm-server start
vi /var/log/cloudera-scm-server/cloudera-scm-server.log -> Started Jetty server

[ec2-user@ip-172-31-23-172 ~]$ sudo cat /var/log/cloudera-scm-server/cloudera-scm-server.log | grep Jetty
2016-11-18 05:14:35,057 INFO WebServerImpl:com.cloudera.server.cmf.WebServerImpl: Started Jetty server.

