# http://blog.puneethabm.in/configure-hadoop-security-with-cloudera-manager-using-kerberos/

[ec2-user@ip-172-31-21-228 ~]$ sudo service --status-all | grep running

sudo service cloudera-scm-agent  stop
sudo service cloudera-scm-server stop
sudo service mysqld              stop
sudo service nscd                stop
sudo service ntpd                stop

[ec2-user@ip-172-31-21-228 ~]$ sudo yum -y install krb5-server krb5-libs krb5-auth-dialog krb5-workstation openldap-clients
(...)
Installed:
  krb5-auth-dialog.x86_64 0:0.13-5.el6                                     krb5-server.x86_64 0:1.10.3-57.el6

Dependency Installed:
  GConf2.x86_64 0:2.28.0-6.el6                     ORBit2.x86_64 0:2.14.17-5.el6                    avahi-glib.x86_64 0:0.6.25-15.el6_8.1
  compat-xcb-util.x86_64 0:0.4.0-2.2.el6           dmz-cursor-themes.noarch 0:0.4-4.el6             flac.x86_64 0:1.2.1-7.el6_6
  gnome-icon-theme.noarch 0:2.28.0-8.el6           gnome-keyring.x86_64 0:2.28.2-8.el6_3            gnome-themes.noarch 0:2.28.1-7.el6
  gnome-vfs2.x86_64 0:2.24.2-8.el6                 gtk2-engines.x86_64 0:2.18.4-5.el6               libIDL.x86_64 0:0.8.13-2.1.el6
  libXres.x86_64 0:1.0.7-2.1.el6                   libart_lgpl.x86_64 0:2.3.20-5.1.el6              libasyncns.x86_64 0:0.8-1.1.el6
  libbonobo.x86_64 0:2.24.2-5.el6                  libbonoboui.x86_64 0:2.24.2-3.el6                libcanberra.x86_64 0:0.22-3.el6
  libcanberra-gtk2.x86_64 0:0.22-3.el6             libglade2.x86_64 0:2.6.4-3.1.el6                 libgnome.x86_64 0:2.28.0-11.el6
  libgnomecanvas.x86_64 0:2.26.0-4.el6             libgnomeui.x86_64 0:2.24.1-4.el6                 libnotify.x86_64 0:0.5.0-1.el6
  libsndfile.x86_64 0:1.0.20-5.el6                 libtool-ltdl.x86_64 0:2.2.6-15.5.el6             libwnck.x86_64 0:2.28.0-3.el6
  notification-daemon.x86_64 0:0.5.0-1.el6         pulseaudio-libs.x86_64 0:0.9.21-24.el6           sgml-common.noarch 0:0.6.3-33.el6
  sound-theme-freedesktop.noarch 0:0.7-3.el6       startup-notification.x86_64 0:0.10-2.1.el6       system-gnome-theme.noarch 0:60.0.2-1.el6
  system-icon-theme.noarch 0:6.0.0-2.el6
Complete!

[ec2-user@ip-172-31-21-231 ~]$ sudo yum -y install krb5-libs krb5-auth-dialog krb5-workstation openldap-clients

@server:
[ec2-user@ip-172-31-21-228 ~]$ sudo vi /var/kerberos/krb5kdc/kdc.conf
[kdcdefaults]
 kdc_ports = 88
 kdc_tcp_ports = 88
[realms]
  SVAG.COM = {
  #master_key_type = aes256-cts
  acl_file = /var/kerberos/krb5kdc/kadm5.acl
  dict_file = /usr/share/dict/words
  admin_keytab = /var/kerberos/krb5kdc/kadm5.keytab
  supported_enctypes = aes256-cts:normal aes128-cts:normal des3-hmac-sha1:normal arcfour-hmac:normal des-hmac-sha1:normal des-cbc-md5:normal des-cbc-crc:normal
  max_life = 1d
  max_renewable_life = 7d
 }

@all_nodes:
[ec2-user@ip-172-31-21-231 ~]$ sudo vi /etc/krb5.conf
[logging]
 default = FILE:/var/log/krb5libs.log
 kdc = FILE:/var/log/krb5kdc.log
 admin_server = FILE:/var/log/kadmind.log

[libdefaults]
 default_realm = SVAG.COM
 dns_lookup_realm = false
 dns_lookup_kdc = false
 ticket_lifetime = 24h
 renew_lifetime = 7d
 forwardable = true
 udp_preference_limit = 1
 default_tgs_enctypes = arcfour-hmac
 default_tkt_enctypes = arcfour-hmac 

[realms] 
  SVAG.COM = {
  kdc = 172.31.21.228    # ip-172-31-21-228.eu-central-1.compute.internal
  admin_server = 172.31.21.228  # ip-172-31-21-228.eu-central-1.compute.internal
 }

[domain_realm]
   .eu-central-1.compute.internal = SVAG.COM
   eu-central-1.compute.internal = SVAG.COM

@server:
[ec2-user@ip-172-31-21-228 ~]$ sudo /usr/sbin/kdb5_util create -s
Loading random data
Initializing database '/var/kerberos/krb5kdc/principal' for realm 'SVAG.COM',
master key name 'K/M@SVAG.COM'
You will be prompted for the database Master Password.
It is important that you NOT FORGET this password.
Enter KDC database master key:                  (pwd)
Re-enter KDC database master key to verify:     (pwd)

[ec2-user@ip-172-31-21-228 ~]$ sudo kadmin.local
kadmin.local:  addprinc cloudera-scm@SVAG.COM
WARNING: no policy specified for cloudera-scm@SVAG.COM; defaulting to no policy
Enter password for principal "cloudera-scm@SVAG.COM":       (scm1000)
Re-enter password for principal "cloudera-scm@SVAG.COM":    (scm1000)
Principal "cloudera-scm@SVAG.COM" created.

[ec2-user@ip-172-31-21-228 ~]$ sudo vi /var/kerberos/krb5kdc/kadm5.acl
*/admin@SVAG.COM *
cloudera-scm@SVAG.COM admilc

[ec2-user@ip-172-31-21-228 ~]$ sudo kadmin.local
kadmin.local:  addpol admin
kadmin.local:  addpol users
kadmin.local:  addpol hosts

[ec2-user@ip-172-31-21-228 ~]$ sudo service krb5kdc start
Starting Kerberos 5 KDC:                                   [  OK  ]
[ec2-user@ip-172-31-21-228 ~]$ sudo service kadmin start
Starting Kerberos 5 Admin Server:                          [  OK  ]

sudo service nscd                start
sudo service ntpd                start
sudo service mysqld              start
sudo service cloudera-scm-agent  start
sudo service cloudera-scm-server start


[ec2-user@ip-172-31-21-228 ~]$ kinit cloudera-scm
Password for cloudera-scm@SVAG.COM:

[ec2-user@ip-172-31-21-228 ~]$ klist
Ticket cache: FILE:/tmp/krb5cc_500
Default principal: cloudera-scm@SVAG.COM
Valid starting     Expires            Service principal
11/17/16 07:22:16  11/18/16 07:22:16  krbtgt/SVAG.COM@SVAG.COM
        renew until 11/24/16 07:22:16

        
[ec2-user@ip-172-31-21-228 ~]$ sudo kadmin.local
Authenticating as principal cloudera-scm/admin@SVAG.COM with password.
kadmin.local:    addprinc roedelk@SVAG.COM
WARNING: no policy specified for roedelk@SVAG.COM; defaulting to no policy
Enter password for principal "roedelk@SVAG.COM":     (cloudera)
Re-enter password for principal "roedelk@SVAG.COM":  (cloudera)
Principal "roedelk@SVAG.COM" created.

[ec2-user@ip-172-31-21-228 ~]$ kinit roedelk
Password for roedelk@SVAG.COM:
[ec2-user@ip-172-31-21-228 ~]$ klist
Ticket cache: FILE:/tmp/krb5cc_500
Default principal: roedelk@SVAG.COM

Valid starting     Expires            Service principal
11/17/16 07:31:46  11/18/16 07:31:46  krbtgt/SVAG.COM@SVAG.COM
        renew until 11/24/16 07:31:46



