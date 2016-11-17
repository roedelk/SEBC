
wget https://archive.cloudera.com/cm5/redhat/6/x86_64/cm/cloudera-manager.repo -O  /etc/yum.repos.d/cloudera-manager.repo 
yum update yum
sudo yum install oracle-j2sdk1.7
ln -s /usr/share/java/mysql-connector-java-5.1.40-bin.jar /usr/java/jdk1.7.0_67-cloudera/lib/mysql-connector.jar
sudo yum install cloudera-manager-daemons cloudera-manager-server


# rpm -ql oracle-j2sdk1.7
export JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera/
export PATH="$PATH:/usr/java/jdk1.7.0_67-cloudera/bin"
# sudo vi /etc/environment

# http://www.cloudera.com/documentation/enterprise/5-8-x/topics/cm_ig_installing_configuring_dbs.html#concept_i2r_m3m_hn
mysql -u root -p
GRANT ALL PRIVILEGES ON *.* TO 'scm'@'%' IDENTIFIED BY 'scm';

[root@ip-172-31-21-228 java]# sudo /usr/share/cmf/schema/scm_prepare_database.sh -u root -p mysql scm scm scm
JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.7.0_67-cloudera/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
2016-11-15 17:22:39,145 [main] INFO  com.cloudera.enterprise.dbutil.DbCommandExecutor  - Successfully connected to database.
All done, your SCM database is configured correctly!

# Creating Databases for Activity Monitor, Reports Manager, Hive Metastore Server, Sentry Server, 
# Cloudera Navigator Audit Server, and Cloudera Navigator Metadata Server

# Activity Monitor                    amon        amon    amon_password
# Reports Manager                     rman        rman    rman_password
# Hive Metastore Server               metastore   hive    hive_password
# Sentry Server                       sentry      sentry  sentry_password
# Cloudera Navigator Audit Server     nav         nav     nav_password
# Cloudera Navigator Metadata Server  navms       navms   navms_password

mysql -u root -p

mysql> create database amon DEFAULT CHARACTER SET utf8;
mysql> grant all on amon.* TO 'amon'@'%' IDENTIFIED BY 'amon_password';

mysql> create database rman DEFAULT CHARACTER SET utf8;
mysql> grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'rman_password';

mysql> create database metastore DEFAULT CHARACTER SET utf8;
mysql> grant all on metastore.* TO 'hive'@'%' IDENTIFIED BY 'hive_password';

mysql> create database sentry DEFAULT CHARACTER SET utf8;
mysql> grant all on sentry.* TO 'sentry'@'%' IDENTIFIED BY 'sentry_password';

mysql> create database nav DEFAULT CHARACTER SET utf8;
mysql> grant all on nav.* TO 'nav'@'%' IDENTIFIED BY 'nav_password';

mysql> create database navms DEFAULT CHARACTER SET utf8;
mysql> grant all on navms.* TO 'navms'@'%' IDENTIFIED BY 'navms_password';

#sudo vi /etc/cloudera-scm-server/db.properties

[root@ip-172-31-21-228 java]# sudo service cloudera-scm-server start
Starting cloudera-scm-server:                              [  OK  ]
[root@ip-172-31-21-228 java]# sudo service cloudera-scm-server status
cloudera-scm-server (pid  27429) is running...

[added to /etc/my.cnf, correct?]
binlog_format=mixed

vi /var/log/cloudera-scm-server/cloudera-scm-server.log
>> Started Jetty server

mysql -u root -p
mysql> create database hue;
mysql> grant all privileges on hue.* to 'hue'@'%' identified by 'pwd';
mysql> grant all on hue.* to 'hue'@'%' identified by 'pwd';

mysql> create database oozie;
mysql> grant all privileges on oozie.* to 'oozie'@'localhost' identified by 'oozie';
mysql> grant all privileges on oozie.* to 'oozie'@'%' identified by 'oozie';

