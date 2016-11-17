[roedelk@ip-172-31-21-228 ~]$ hadoop fs -ls /user/hive
Found 1 items
drwxrwxrwt   - hive hive          0 2016-11-16 11:22 /user/hive/warehouse

#sudo -u hdfs kinit -kt <hdfs.keytab> hdfs
#sudo -u hdfs hdfs dfs -chmod -R 771 /user/hive/warehouse
#sudo -u hdfs hdfs dfs -chown -R hive:hive /user/hive/warehouse

[CM]:
    > Hive service > Configuration tab > Scope = HiveServer2 > Category = Main
    Uncheck the "HiveServer2 Enable Impersonation" checkbox
    Save Changes

If you are using YARN, enable the Hive user to submit YARN jobs.
    > YARN service > Configuration tab > Scope = NodeManager > Category = Security
    Ensure the Allowed System Users property includes the hive user. If not, add hive.
    Save Change & Restart the YARN service

Enabling the Sentry Service for Hive
    > Hive service > Configuration tab > Scope = Hive (Service-Wide) > Category = Main.
    Locate the Sentry Service property and select Sentry.
    Save Changes & Restart Hive service

Enabling the Sentry Service for Hue
    > Hue service > Configuration tab > Scope > Hue (Service-Wide) > Category > Main
    Locate the Sentry Service property and select Sentry.
    Save Changes & Restart Hue

Add the Hive, Impala and Hue Groups to Sentry's Admin Groups
    > Sentry service > Configuration tab > Scope = Sentry (Service-Wide) > Category = Main
    Locate the Admin Groups property and add the hive, impala and hue groups to the list. 
    If an end user is in one of these admin groups, that user has administrative privileges on the Sentry Server.
    Save Changes


 A Quick Sentry Tutorial 
    
[ec2-user@ip-172-31-21-228 ~]$ sudo cat /etc/passwd | grep roedelk
[ec2-user@ip-172-31-21-228 ~]$ sudo cat /etc/group
    
sentry.service.admin.group  >> add kmem (Primary group of user roedelk)

> Restart Sentry

[ec2-user@ip-172-31-21-227 ~]$ beeline 
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-21-227.eu-central-1.compute.internal@SVAG.COM

0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20161117100606_3515b436-217a-4f38-96be-99c8f303ea19): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161117100606_3515b436-217a-4f38-96be-99c8f303ea19); Time taken: 0.722 seconds
INFO  : Executing command(queryId=hive_20161117100606_3515b436-217a-4f38-96be-99c8f303ea19): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117100606_3515b436-217a-4f38-96be-99c8f303ea19); Time taken: 0.245 seconds
INFO  : OK
+-----------+--+
| tab_name  |
+-----------+--+
+-----------+--+
No rows selected (2.28 seconds)

0: jdbc:hive2://localhost:10000/default> CREATE ROLE sentry_admin;
INFO  : Compiling command(queryId=hive_20161117100808_0c8fcfcb-7eb8-4140-9b51-3527eb8662db): CREATE ROLE sentry_admin
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161117100808_0c8fcfcb-7eb8-4140-9b51-3527eb8662db); Time taken: 0.1 seconds
INFO  : Executing command(queryId=hive_20161117100808_0c8fcfcb-7eb8-4140-9b51-3527eb8662db): CREATE ROLE sentry_admin
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117100808_0c8fcfcb-7eb8-4140-9b51-3527eb8662db); Time taken: 0.788 seconds
INFO  : OK
No rows affected (0.901 seconds)

0: jdbc:hive2://localhost:10000/default> GRANT ALL ON SERVER server1 TO ROLE sentry_admin;
INFO  : Compiling command(queryId=hive_20161117100808_afc2b3ec-a018-43a3-bf97-a4324a57e7b4): GRANT ALL ON SERVER server1 TO ROLE sentry_admin
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161117100808_afc2b3ec-a018-43a3-bf97-a4324a57e7b4); Time taken: 0.105 seconds
INFO  : Executing command(queryId=hive_20161117100808_afc2b3ec-a018-43a3-bf97-a4324a57e7b4): GRANT ALL ON SERVER server1 TO ROLE sentry_admin
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117100808_afc2b3ec-a018-43a3-bf97-a4324a57e7b4); Time taken: 0.095 seconds
INFO  : OK
No rows affected (0.213 seconds)

jdbc:hive2://localhost:10000/default> GRANT ROLE sentry_admin TO GROUP kmem;
INFO  : Compiling command(queryId=hive_20161117100808_0926a01f-d56c-4dc6-9870-bbcfbfb9b154): GRANT ROLE sentry_admin TO GROUP kmem
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161117100808_0926a01f-d56c-4dc6-9870-bbcfbfb9b154); Time taken: 0.065 seconds
INFO  : Executing command(queryId=hive_20161117100808_0926a01f-d56c-4dc6-9870-bbcfbfb9b154): GRANT ROLE sentry_admin TO GROUP kmem
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117100808_0926a01f-d56c-4dc6-9870-bbcfbfb9b154); Time taken: 0.082 seconds
INFO  : OK
No rows affected (0.156 seconds)

0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20161117100909_bcba99bf-23e4-4f39-9627-ed0d6add9f01): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161117100909_bcba99bf-23e4-4f39-9627-ed0d6add9f01); Time taken: 0.065 seconds
INFO  : Executing command(queryId=hive_20161117100909_bcba99bf-23e4-4f39-9627-ed0d6add9f01): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117100909_bcba99bf-23e4-4f39-9627-ed0d6add9f01); Time taken: 0.132 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.249 seconds)


sudo groupadd selector
sudo groupadd inserters
sudo useradd -u 1100 -g selector george
sudo useradd -u 1200 -g inserters ferdinand
kadmin.local: add_principal george
>> Password: g1
kadmin.local: add_principal ferdinand
>> Password: f1

0: jdbc:hive2://localhost:10000/default> CREATE ROLE reads;
INFO  : Compiling command(queryId=hive_20161117101717_3372de07-30f4-4ef4-b4da-c937043702cc): CREATE ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161117101717_3372de07-30f4-4ef4-b4da-c937043702cc); Time taken: 0.072 seconds
INFO  : Executing command(queryId=hive_20161117101717_3372de07-30f4-4ef4-b4da-c937043702cc): CREATE ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117101717_3372de07-30f4-4ef4-b4da-c937043702cc); Time taken: 0.047 seconds
INFO  : OK
No rows affected (0.178 seconds)

0: jdbc:hive2://localhost:10000/default> CREATE ROLE writes;
INFO  : Compiling command(queryId=hive_20161117101818_0b160549-64fc-4c74-baaa-1cc114eeebc5): CREATE ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161117101818_0b160549-64fc-4c74-baaa-1cc114eeebc5); Time taken: 0.067 seconds
INFO  : Executing command(queryId=hive_20161117101818_0b160549-64fc-4c74-baaa-1cc114eeebc5): CREATE ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117101818_0b160549-64fc-4c74-baaa-1cc114eeebc5); Time taken: 0.03 seconds
INFO  : OK
No rows affected (0.106 seconds)

0: jdbc:hive2://localhost:10000/default> GRANT SELECT ON DATABASE default TO ROLE reads;
INFO  : Compiling command(queryId=hive_20161117101818_c38a8ff2-4c32-4e98-800f-586482d1b922): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161117101818_c38a8ff2-4c32-4e98-800f-586482d1b922); Time taken: 0.065 seconds
INFO  : Executing command(queryId=hive_20161117101818_c38a8ff2-4c32-4e98-800f-586482d1b922): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117101818_c38a8ff2-4c32-4e98-800f-586482d1b922); Time taken: 0.047 seconds
INFO  : OK
No rows affected (0.121 seconds)

0: jdbc:hive2://localhost:10000/default> GRANT ROLE reads TO GROUP selector;
INFO  : Compiling command(queryId=hive_20161117101818_6125cd85-11f2-4f05-8cdd-609dd536ac97): GRANT ROLE reads TO GROUP selector
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161117101818_6125cd85-11f2-4f05-8cdd-609dd536ac97); Time taken: 0.059 seconds
INFO  : Executing command(queryId=hive_20161117101818_6125cd85-11f2-4f05-8cdd-609dd536ac97): GRANT ROLE reads TO GROUP selector
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117101818_6125cd85-11f2-4f05-8cdd-609dd536ac97); Time taken: 0.045 seconds
INFO  : OK
No rows affected (0.116 seconds)

0: jdbc:hive2://localhost:10000/default>     REVOKE ALL ON DATABASE default FROM ROLE writes;
INFO  : Compiling command(queryId=hive_20161117101919_994d12c5-6a50-4814-aab2-9976b83745f2): REVOKE ALL ON DATABASE default FROM ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161117101919_994d12c5-6a50-4814-aab2-9976b83745f2); Time taken: 0.094 seconds
INFO  : Executing command(queryId=hive_20161117101919_994d12c5-6a50-4814-aab2-9976b83745f2): REVOKE ALL ON DATABASE default FROM ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117101919_994d12c5-6a50-4814-aab2-9976b83745f2); Time taken: 0.095 seconds
INFO  : OK
No rows affected (0.199 seconds)
0: jdbc:hive2://localhost:10000/default>     GRANT SELECT ON default.sample_07 TO ROLE writes;
INFO  : Compiling command(queryId=hive_20161117101919_9023afa6-70a8-4ee0-8a99-8beef8aa61d9): GRANT SELECT ON default.sample_07 TO ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161117101919_9023afa6-70a8-4ee0-8a99-8beef8aa61d9); Time taken: 0.066 seconds
INFO  : Executing command(queryId=hive_20161117101919_9023afa6-70a8-4ee0-8a99-8beef8aa61d9): GRANT SELECT ON default.sample_07 TO ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117101919_9023afa6-70a8-4ee0-8a99-8beef8aa61d9); Time taken: 0.048 seconds
INFO  : OK
No rows affected (0.123 seconds)
0: jdbc:hive2://localhost:10000/default>     GRANT ROLE writes TO GROUP inserters;
INFO  : Compiling command(queryId=hive_20161117101919_7180001b-f8f5-4737-8059-66e91db1a1e2): GRANT ROLE writes TO GROUP inserters
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161117101919_7180001b-f8f5-4737-8059-66e91db1a1e2); Time taken: 0.078 seconds
INFO  : Executing command(queryId=hive_20161117101919_7180001b-f8f5-4737-8059-66e91db1a1e2): GRANT ROLE writes TO GROUP inserters
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117101919_7180001b-f8f5-4737-8059-66e91db1a1e2); Time taken: 0.031 seconds
INFO  : OK
No rows affected (0.12 seconds)

[ec2-user@ip-172-31-21-227 ~]$ kinit george
Password for george@SVAG.COM:
[ec2-user@ip-172-31-21-227 ~]$ klist
Ticket cache: FILE:/tmp/krb5cc_500
Default principal: george@SVAG.COM

Valid starting     Expires            Service principal
11/17/16 10:19:52  11/18/16 10:19:52  krbtgt/SVAG.COM@SVAG.COM
        renew until 11/24/16 10:19:52

0: jdbc:hive2://localhost:10000/default>  SHOW TABLES;
INFO  : Compiling command(queryId=hive_20161117102323_9eaeeabb-73f7-45ec-9cf2-1a7f57723965): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161117102323_9eaeeabb-73f7-45ec-9cf2-1a7f57723965); Time taken: 0.068 seconds
INFO  : Executing command(queryId=hive_20161117102323_9eaeeabb-73f7-45ec-9cf2-1a7f57723965): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117102323_9eaeeabb-73f7-45ec-9cf2-1a7f57723965); Time taken: 0.138 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.329 seconds)

[ec2-user@ip-172-31-21-227 ~]$ kinit ferdinand
Password for ferdinand@SVAG.COM:
[ec2-user@ip-172-31-21-227 ~]$ klist
Ticket cache: FILE:/tmp/krb5cc_500
Default principal: ferdinand@SVAG.COM

Valid starting     Expires            Service principal
11/17/16 10:23:59  11/18/16 10:23:59  krbtgt/SVAG.COM@SVAG.COM
        renew until 11/24/16 10:23:59

0: jdbc:hive2://localhost:10000/default>  SHOW TABLES;
INFO  : Compiling command(queryId=hive_20161117102424_d13694a1-9aaf-48b5-938e-487450740e80): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161117102424_d13694a1-9aaf-48b5-938e-487450740e80); Time taken: 0.068 seconds
INFO  : Executing command(queryId=hive_20161117102424_d13694a1-9aaf-48b5-938e-487450740e80): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161117102424_d13694a1-9aaf-48b5-938e-487450740e80); Time taken: 0.137 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| sample_07  |
+------------+--+
1 row selected (0.336 seconds)


```

```
