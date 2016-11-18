
#    List the region, AMI ID, and OS you are using
* eu-central-1b
* RHEL-6.7_HVM-20160219-x86_64-1-Hourly2-GP2 (ami-cd362ca1)
* Redhat 6.7

#    List the volume space you have available on each node
Filesystem  Size  Used  Avail  Use%  Mounted   on
/dev/xvda1  69G   1.7G  64G    3%    /
tmpfs       7.3G  0     7.3G   0%    /dev/shm

#    The command and output for yum repolist enabled
Loaded plugins: amazon-id, rhui-lb, security
Repo rhui-REGION-client-config-server-6 forced skip_if_unavailable=True due to: /etc/pki/rhui/cdn.redhat.com-chain.crt
Repo rhui-REGION-client-config-server-6 forced skip_if_unavailable=True due to: /etc/pki/rhui/product/rhui-client-config-server-6.crt
Repo rhui-REGION-client-config-server-6 forced skip_if_unavailable=True due to: /etc/pki/rhui/rhui-client-config-server-6.key
Repo rhui-REGION-rhel-server-releases forced skip_if_unavailable=True due to: /etc/pki/rhui/cdn.redhat.com-chain.crt
Repo rhui-REGION-rhel-server-releases forced skip_if_unavailable=True due to: /etc/pki/rhui/product/content-rhel6.crt
Repo rhui-REGION-rhel-server-releases forced skip_if_unavailable=True due to: /etc/pki/rhui/content-rhel6.key
Repo rhui-REGION-rhel-server-rh-common forced skip_if_unavailable=True due to: /etc/pki/rhui/cdn.redhat.com-chain.crt
Repo rhui-REGION-rhel-server-rh-common forced skip_if_unavailable=True due to: /etc/pki/rhui/product/content-rhel6.crt
Repo rhui-REGION-rhel-server-rh-common forced skip_if_unavailable=True due to: /etc/pki/rhui/content-rhel6.key
Could not contact CDS load balancer rhui2-cds01.eu-central-1.aws.ce.redhat.com, trying others.
Could not contact any CDS load balancers: rhui2-cds01.eu-central-1.aws.ce.redhat.com, rhui2-cds02.eu-central-1.aws.ce.redhat.com.


sudo groupadd --gid 2200 democratic 
sudo groupadd --gid 2300 social 
sudo adduser --password b1 --uid 2700 --gid 2300 bavaria
sudo adduser --password s1 --uid 2800 --gid 2200 saxony

[ec2-user@ip-172-31-23-170 ~]$ sudo cat /etc/passwd | grep bavaria
bavaria:x:2700:2300::/home/bavaria:/bin/bash
[ec2-user@ip-172-31-23-170 ~]$ sudo cat /etc/passwd | grep saxony
saxony:x:2800:2200::/home/saxony:/bin/bash
[ec2-user@ip-172-31-23-170 ~]$ sudo cat /etc/group | grep social
social:x:2300:
[ec2-user@ip-172-31-23-170 ~]$ sudo cat /etc/group | grep democratic
democratic:x:2200:
