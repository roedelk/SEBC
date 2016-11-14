# 1a. Check vm.swappiness on all your nodes: http://askubuntu.com/questions/103915/how-do-i-configure-swappiness
cat /proc/sys/vm/swappiness
# -> 
60
# 1b. Set the value to 1 if necessary
sudo sysctl vm.swappiness=1
cat /proc/sys/vm/swappiness
# -> 
1
#
# 2. Show the mount attributes of all volumes
lsblk
# ->
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
xvda    202:0    0     8G  0 disk
+-xvda1 202:1    0     8G  0 part /
xvdb    202:16   0  37.5G  0 disk /mnt
xvdc    202:32   0  37.5G  0 disk
#
mount | grep /dev/xv
# ->
/dev/xvda1 on / type ext4 (rw,discard)
/dev/xvdb on /mnt type ext3 (rw,_netdev)
#
# 3. Show the reserve space of any non-root, ext-based volumes
df -hP | column -t
# -> 
Filesystem  Size  Used  Avail  Use%  Mounted         on
udev        7.4G  12K   7.4G   1%    /dev
tmpfs       1.5G  344K  1.5G   1%    /run
/dev/xvda1  7.8G  801M  6.6G   11%   /
none        4.0K  0     4.0K   0%    /sys/fs/cgroup
none        5.0M  0     5.0M   0%    /run/lock
none        7.4G  0     7.4G   0%    /run/shm
none        100M  0     100M   0%    /run/user
/dev/xvdb   37G   49M   35G    1%    /mnt
#
# 4. Show that transparent hugepages is disabled
sudo vi /proc/vmstat | grep hugepages transparent
# -> 
Vim: Warning: Output is not to a terminal
nr_anon_transparent_hugepages 0

sudo su -
cat /sys/kernel/mm/transparent_hugepage/enabled
cat /sys/kernel/mm/transparent_hugepage/defrag
#
# Create the init.d script at /etc/init.d/disable-transparent-hugepages 
# (https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/)

#!/bin/bash
echo 'never' > /sys/kernel/mm/transparent_hugepage/enabled
echo 'never' > /sys/kernel/mm/transparent_hugepage/defrag

sudo chmod 755 /etc/init.d/disable-transparent-hugepages
sudo sh /etc/init.d/disable-transparent-hugepages
sudo update-rc.d disable-transparent-hugepages defaults

root@ip-172-31-17-139:~# cat /sys/kernel/mm/transparent_hugepage/enabled
always madvise [never]
root@ip-172-31-17-139:~# cat /sys/kernel/mm/transparent_hugepage/defrag
always madvise [never]
#
# 5. Report the network interface attributes
ifconfig
# ->
eth0      Link encap:Ethernet  HWaddr 06:45:d1:86:20:af
          inet addr:172.31.17.139  Bcast:172.31.31.255  Mask:255.255.240.0
          inet6 addr: fe80::445:d1ff:fe86:20af/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:638 errors:0 dropped:0 overruns:0 frame:0
          TX packets:647 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:71216 (71.2 KB)  TX bytes:78961 (78.9 KB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
#
# 6. Show forward and reverse host lookups using getent and nslookup
ec2-35-156-86-130.eu-central-1.compute.amazonaws.com
ec2-35-156-82-93.eu-central-1.compute.amazonaws.com
ec2-35-156-54-220.eu-central-1.compute.amazonaws.com
ec2-35-156-80-75.eu-central-1.compute.amazonaws.com
ec2-35-156-86-14.eu-central-1.compute.amazonaws.com
#
# 6a. getent
root@ip-172-31-17-139:~#  getent ahosts
127.0.0.1       localhost
127.0.0.1       ip6-localhost ip6-loopback
#
# 6b.nslookup (http://www.thegeekstuff.com/2012/07/nslookup-examples)
root@ip-172-31-17-139:~# nslookup 35.156.54.220
Server:         172.31.0.2
Address:        172.31.0.2#53

Non-authoritative answer:
220.54.156.35.in-addr.arpa      name = ec2-35-156-54-220.eu-central-1.compute.amazonaws.com.

Authoritative answers can be found from:
#
# 7. Verify the nscd service is running
root@ip-172-31-17-139:~# sudo apt-get install  nscd
root@ip-172-31-17-139:~# sudo apt-get update
root@ip-172-31-17-139:~# service nscd start
 * Starting Name Service Cache Daemon nscd                      [ OK ]
root@ip-172-31-17-139:~# service nscd status
 * Status of Name Service Cache Daemon service:   
 * running.
#
# 8. Verify the ntpd service is running
root@ip-172-31-17-139:~# sudo apt-get install ntp
root@ip-172-31-17-139:~# sudo apt-get update
root@ip-172-31-17-139:~# service ntp start
 * Starting NTP server ntpd                                     [ OK ]
root@ip-172-31-17-139:~# service ntp status
 * NTP server is running


