MySQL installation

wget https://dev.mysql.com/get/mysql-apt-config_0.8.0-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.0-1_all.deb
>> Choosing mysql-5.6.34
sudo apt-get update
sudo apt-get install mysql-server
>> Choosing root password "pwd"
sudo service mysql status

# Just have a look:
vi /etc/mysql/my.cnf

# wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz
# gunzip mysql-connector-java-5.1.40.tar.gz | tar -xvf
# tar -xvf mysql-connector-java-5.1.40.tar
# sudo cp mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/
# alternative (easier & right version for OS):
sudo apt-get install libmysql-java

Use /usr/bin/mysql_secure_installation to:
a. Set password protection for the server
b. Revoke permissions for anonymous users
c. Permit remote privileged login
d. Remove test databases
e. Refresh privileges in memory
f. Refreshes the mysqld service

sudo /usr/bin/mysql_secure_installation
--
Change the root password? [Y/n] n
 ... skipping.
By default, a MySQL installation has an anonymous user, allowing anyone to log into MySQL without having to have a user account created for them.  This is intended only for testing, and to make the installation go a bit smoother.  You should remove them before moving into a production environment.

Remove anonymous users? [Y/n] Y
 ... Success!
Normally, root should only be allowed to connect from 'localhost'.  This ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] n
 ... skipping.
By default, MySQL comes with a database named 'test' that anyone can access.  This is also intended only for testing, and should be removed before moving into a production environment.

Remove test database and access to it? [Y/n] Y
 - Dropping test database...
ERROR 1008 (HY000) at line 1: Can't drop database 'test'; database doesn't exist
 ... Failed!  Not critical, keep moving...
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far will take effect immediately.
Reload privilege tables now? [Y/n] Y
 ... Success!

All done!  If you've completed all of the above steps, your MySQL installation should now be secure.

Thanks for using MySQL!
Cleaning up...

sudo service mysql restart
 * Stopping MySQL Community Server 5.6.34
..cat: /var/run/mysqld/mysqld.pid: No such file or directory
..
 * MySQL Community Server 5.6.34 is stopped
 * Re-starting MySQL Community Server 5.6.34
......
 * MySQL Community Server 5.6.34 is started

mysql -u root -p
> GRANT REPLICATION SLAVE ON *.* TO 'root'@'localhost' IDENTIFIED BY 'pwd';
> SET GLOBAL binlog_format = 'ROW';
> FLUSH TABLES WITH READ LOCK;

Note the FQDN of your replica host (fully qualified domain name).
GRANT REPLICATION SLAVE ON *.* TO 'root'@'FQDN' IDENTIFIED BY 'pwd'; 



