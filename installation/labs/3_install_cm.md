
sudo apt-get update
sudo wget 'https://archive.cloudera.com/cm5/ubuntu/trusty/amd64/cm/cloudera.list' -O /etc/apt/sources.list.d/cloudera-manager.list
sudo apt-get update
sudo apt-get install oracle-j2sdk1.7
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following NEW packages will be installed:
  oracle-j2sdk1.7
0 upgraded, 1 newly installed, 0 to remove and 21 not upgraded.
Need to get 142 MB of archives.
After this operation, 292 MB of additional disk space will be used.
WARNING: The following packages cannot be authenticated!
  oracle-j2sdk1.7
Install these packages without verification? [y/N] y
Get:1 http://archive.cloudera.com/cm5/ubuntu/trusty/amd64/cm/ trusty-cm5/contrib oracle-j2sdk1.7 amd64 1.7.0+update67-1 [142 MB]
Fetched 142 MB in 3s (42.0 MB/s)
Selecting previously unselected package oracle-j2sdk1.7.
(Reading database ... 51513 files and directories currently installed.)
Preparing to unpack .../oracle-j2sdk1.7_1.7.0+update67-1_amd64.deb ...
Unpacking oracle-j2sdk1.7 (1.7.0+update67-1) ...
Setting up oracle-j2sdk1.7 (1.7.0+update67-1) ...

ubuntu@ip-172-31-17-139:~$ sudo apt-get install cloudera-manager-daemons cloudera-manager-server
Fetched 567 MB in 15s (37.2 MB/s)
Selecting previously unselected package cloudera-manager-daemons.
(Reading database ... 53639 files and directories currently installed.)
Preparing to unpack .../cloudera-manager-daemons_5.9.0-1.cm590.p0.249~trusty-cm5_all.deb ...
Unpacking cloudera-manager-daemons (5.9.0-1.cm590.p0.249~trusty-cm5) ...
Selecting previously unselected package cloudera-manager-server.
Preparing to unpack .../cloudera-manager-server_5.9.0-1.cm590.p0.249~trusty-cm5_all.deb ...
Unpacking cloudera-manager-server (5.9.0-1.cm590.p0.249~trusty-cm5) ...
Processing triggers for ureadahead (0.100.0-16) ...
Setting up cloudera-manager-daemons (5.9.0-1.cm590.p0.249~trusty-cm5) ...
Setting up cloudera-manager-server (5.9.0-1.cm590.p0.249~trusty-cm5) ...
 Adding system startup for /etc/init.d/cloudera-scm-server ...
   /etc/rc0.d/K10cloudera-scm-server -> ../init.d/cloudera-scm-server
   /etc/rc1.d/K10cloudera-scm-server -> ../init.d/cloudera-scm-server
   /etc/rc6.d/K10cloudera-scm-server -> ../init.d/cloudera-scm-server
   /etc/rc2.d/S90cloudera-scm-server -> ../init.d/cloudera-scm-server
   /etc/rc3.d/S90cloudera-scm-server -> ../init.d/cloudera-scm-server
   /etc/rc4.d/S90cloudera-scm-server -> ../init.d/cloudera-scm-server
   /etc/rc5.d/S90cloudera-scm-server -> ../init.d/cloudera-scm-server
Processing triggers for ureadahead (0.100.0-16) ...

ubuntu@ip-172-31-17-139:~$ sudo service cloudera-scm-server start
Starting cloudera-scm-server:  * cloudera-scm-server started



# Additional step for Ubuntu 14.04
sudo vi /etc/apt/preferences.d/cloudera.pref
"""
Package: *
Pin: release o=Cloudera, l=Cloudera
Pin-Priority: 501
"""

# Cloudera Repository key
wget https://archive.cloudera.com/cdh5/ubuntu/trusty/amd64/cdh/archive.key -O archive.key 
sudo apt-key add archive.key