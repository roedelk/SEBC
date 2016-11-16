# MySQL installation
# http://www.cloudera.com/documentation/enterprise/5-8-x/topics/cm_ig_mysql.html

wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
sudo rpm -ivh mysql-community-release-el6-5.noarch.rpm
yum update yum
sudo yum install mysql-server
sudo service mysqld start

sudo service mysqld status

# Just have a look:
vi /etc/my.cnf

Use /usr/bin/mysql_secure_installation to:
a. Set password protection for the server
b. Revoke permissions for anonymous users
c. Permit remote privileged login
d. Remove test databases
e. Refresh privileges in memory
f. Refreshes the mysqld service

[root@ip-172-31-21-228 ~]# /usr/bin/mysql_secure_installation
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MySQL
root user without the proper authorisation.

Set root password? [Y/n] Y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!

By default, a MySQL installation has an anonymous user, allowing anyone
to log into MySQL without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.
Remove anonymous users? [Y/n] Y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.
Disallow root login remotely? [Y/n] n
 ... skipping.

By default, MySQL comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.
Remove test database and access to it? [Y/n] Y
 - Dropping test database...
ERROR 1008 (HY000) at line 1: Can't drop database 'test'; database doesn't exist
 ... Failed!  Not critical, keep moving...
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.
Reload privilege tables now? [Y/n] Y
 ... Success!

All done!  If you've completed all of the above steps, your MySQL
installation should now be secure.
Thanks for using MySQL!
Cleaning up...

[root@ip-172-31-21-228 ~]# sudo service mysqld restart
Stopping mysqld:                                           [  OK  ]
Starting mysqld:                                           [  OK  ]

[root@ip-172-31-21-228 ~]# wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz
[root@ip-172-31-21-228 ~]# gunzip mysql-connector-java-5.1.40.tar.gz
[root@ip-172-31-21-228 ~]# tar -xvf mysql-connector-java-5.1.40.tar
[root@ip-172-31-21-228 ~]# sudo mkdir -p /usr/share/java/
[root@ip-172-31-21-228 ~]# sudo cp mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/
[root@ip-172-31-21-228 ~]# ln -s /usr/share/java/mysql-connector-java-5.1.40-bin.jar /usr/share/java/mysql-connector.jar
 
(all nodes) 
[root@ip-172-31-21-228 ~]# sudo service mysqld stop
[root@ip-172-31-21-228 ~]# sudo vi /etc/my.cnf
[mysqld]
log_bin=mysql-bin
server_id=1 (n0)
server_id=2 (n1)
[root@ip-172-31-21-228 ~]# sudo service mysqld start

(master node) 
mysql -u root -p
mysql> GRANT REPLICATION SLAVE ON *.* TO 'slave'@'ec2-35-156-18-128.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'pwd';
Query OK, 0 rows affected (0.01 sec)
mysql>  SET GLOBAL binlog_format = 'ROW';
Query OK, 0 rows affected (0.00 sec)
mysql> FLUSH TABLES WITH READ LOCK;
Query OK, 0 rows affected (0.00 sec)

(2nd master session)
mysql> SHOW MASTER STATUS;
+------------------+----------+--------------+------------------+-------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+------------------+----------+--------------+------------------+-------------------+
| mysql-bin.000002 |      370 |              |                  |                   |
+------------------+----------+--------------+------------------+-------------------+
1 row in set (0.00 sec)

(slave node) # http://dev.mysql.com/doc/refman/5.7/en/replication-setup-slaves.html
CHANGE MASTER TO MASTER_HOST='ec2-35-156-75-11.eu-central-1.compute.amazonaws.com', MASTER_USER='slave', MASTER_PASSWORD='pwd', 
MASTER_LOG_FILE='mysql-bin.000002', MASTER_LOG_POS=370;
Query OK, 0 rows affected, 2 warnings (0.03 sec)

mysql> START SLAVE;
mysql> SHOW SLAVE STATUS \G
*************************** 1. row ***************************
               Slave_IO_State: Connecting to master
                  Master_Host: ec2-35-156-86-130.eu-central-1.compute.amazonaws.com
                  Master_User: slave
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mysql-bin.000001
          Read_Master_Log_Pos: 369
               Relay_Log_File: mysqld-relay-bin.000001
                Relay_Log_Pos: 4
        Relay_Master_Log_File: mysql-bin.000001
             Slave_IO_Running: Connecting
            Slave_SQL_Running: Yes
              Replicate_Do_DB:
          Replicate_Ignore_DB:
           Replicate_Do_Table:
       Replicate_Ignore_Table:
      Replicate_Wild_Do_Table:
  Replicate_Wild_Ignore_Table:
                   Last_Errno: 0
                   Last_Error:
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 369
              Relay_Log_Space: 120
              Until_Condition: None
               Until_Log_File:
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File:
           Master_SSL_CA_Path:
              Master_SSL_Cert:
            Master_SSL_Cipher:
               Master_SSL_Key:
        Seconds_Behind_Master: NULL
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 2003
                Last_IO_Error: error connecting to master 'slave@ec2-35-156-86-130.eu-central-1.compute.amazonaws.com:3306' - retry-time: 60  retries: 38
               Last_SQL_Errno: 0
               Last_SQL_Error:
  Replicate_Ignore_Server_Ids:
             Master_Server_Id: 0
                  Master_UUID:
             Master_Info_File: /var/lib/mysql/master.info
                    SQL_Delay: 0
          SQL_Remaining_Delay: NULL
      Slave_SQL_Running_State: Slave has read all relay log; waiting for the slave I/O thread to update it
           Master_Retry_Count: 86400
                  Master_Bind:
      Last_IO_Error_Timestamp: 161115 10:41:13
     Last_SQL_Error_Timestamp:
               Master_SSL_Crl:
           Master_SSL_Crlpath:
           Retrieved_Gtid_Set:
            Executed_Gtid_Set:
                Auto_Position: 0
1 row in set (0.00 sec)


[root@ip-172-31-21-228 ~]# mysql -u root -p -h ec2-35-156-18-128.eu-central-1.compute.amazonaws.com
Enter password:
ERROR 1130 (HY000): Host 'ip-172-31-21-228.eu-central-1.compute.internal' is not allowed to connect to this MySQL server
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'pwd'
[root@ip-172-31-21-228 ~]# mysql -u root -p -h ec2-35-156-75-11.eu-central-1.compute.amazonaws.com  

==> not working