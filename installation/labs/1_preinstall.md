# 1a. Check vm.swappiness on all your nodes: http://askubuntu.com/questions/103915/how-do-i-configure-swappiness 
[ec2-user@ip-172-31-27-82 ~]$ cat /proc/sys/vm/swappiness
60
# 1b. Set the value to 1 if necessary
[ec2-user@ip-172-31-27-82 ~]$ sudo sysctl vm.swappiness=1
[ec2-user@ip-172-31-27-82 ~]$ cat /proc/sys/vm/swappiness
1
#
# 2. Show the mount attributes of all volumes
[ec2-user@ip-172-31-27-82 ~]$ lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0  70G  0 disk
└─xvda1 202:1    0  70G  0 part /
#
[ec2-user@ip-172-31-27-82 ~]$ mount | grep /dev/xv
/dev/xvda1 on / type ext4 (rw)
#
# 3. Show the reserve space of any non-root, ext-based volumes
[ec2-user@ip-172-31-27-82 ~]$ df -hP | column -t
Filesystem  Size  Used  Avail  Use%  Mounted   on
/dev/xvda1  69G   1.7G  64G    3%    /
tmpfs       7.3G  0     7.3G   0%    /dev/shm
#
# 4. Show that transparent hugepages is disabled
#
sudo su -
echo 'never' > /sys/kernel/mm/transparent_hugepage/enabled
echo 'never' > /sys/kernel/mm/transparent_hugepage/defrag
cat /sys/kernel/mm/transparent_hugepage/enabled
cat /sys/kernel/mm/transparent_hugepage/defrag
exit
#
[root@ip-172-31-27-85 ~]# cat /sys/kernel/mm/transparent_hugepage/enabled
always madvise [never]
[root@ip-172-31-27-85 ~]# cat /sys/kernel/mm/transparent_hugepage/defrag
always madvise [never]
#
# 5. Report the network interface attributes
[root@ip-172-31-27-85 ~]# ifconfig
eth0      Link encap:Ethernet  HWaddr 06:AD:01:AC:45:6F
          inet addr:172.31.27.85  Bcast:172.31.31.255  Mask:255.255.240.0
          inet6 addr: fe80::4ad:1ff:feac:456f/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:267 errors:0 dropped:0 overruns:0 frame:0
          TX packets:320 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:33235 (32.4 KiB)  TX bytes:37712 (36.8 KiB)
          Interrupt:145

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 b)  TX bytes:0 (0.0 b)
#
# 6. Show forward and reverse host lookups using getent and nslookup
 ec2-35-156-84-238.eu-central-1.compute.amazonaws.com 
 ec2-35-156-77-44.eu-central-1.compute.amazonaws.com  
 ec2-35-156-92-134.eu-central-1.compute.amazonaws.com 
 ec2-35-156-72-122.eu-central-1.compute.amazonaws.com 
 ec2-35-156-56-18.eu-central-1.compute.amazonaws.com  
#
# 6a. getent
[ec2-user@ip-172-31-27-82 ~]$ getent ahosts
127.0.0.1       localhost localhost.localdomain localhost4 localhost4.localdomain4
127.0.0.1       localhost localhost.localdomain localhost6 localhost6.localdomain6
#
# 6b.nslookup (http://www.thegeekstuff.com/2012/07/nslookup-examples)
[root@ip-172-31-27-85 ~]# nslookup 35.156.77.44
Server:         172.31.0.2
Address:        172.31.0.2#53

Non-authoritative answer:
44.77.156.35.in-addr.arpa       name = ec2-35-156-77-44.eu-central-1.compute.amazonaws.com.

Authoritative answers can be found from:
#
# 7. Verify the nscd service is running
[root@ip-172-31-27-85 ~]# sudo yum install nscd
[root@ip-172-31-27-85 ~]# sudo yum update yum
[root@ip-172-31-27-85 ~]# sudo service nscd start
Starting nscd:                                             [  OK  ]
[root@ip-172-31-27-85 ~]# sudo service nscd status
nscd (pid 2052) is running...
#
# 8. Verify the ntpd service is running
[root@ip-172-31-27-85 ~]# sudo yum install ntp
[root@ip-172-31-27-85 ~]# sudo yum update yum
[root@ip-172-31-27-85 ~]# sudo service ntpd start
Starting ntpd:                                             [  OK  ]
[root@ip-172-31-27-85 ~]# sudo service ntpd status
ntpd (pid  2161) is running...



