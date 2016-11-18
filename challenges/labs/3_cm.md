mysql> show grants for hive;
+-----------------------------------------------------------------------------------------------------+
| Grants for hive@%                                                                                   |
+-----------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'hive'@'%' IDENTIFIED BY PASSWORD '*8AC2E431CC7A9F2C4C0E51A65B8D8175892D9F22' |
| GRANT ALL PRIVILEGES ON `metastore`.* TO 'hive'@'%'                                                 |
+-----------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> show grants for rman;
+-----------------------------------------------------------------------------------------------------+
| Grants for rman@%                                                                                   |
+-----------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'rman'@'%' IDENTIFIED BY PASSWORD '*AEF345BFE495D8E678EA9D3D5708FD110AD2F08E' |
| GRANT ALL PRIVILEGES ON `rman`.* TO 'rman'@'%'                                                      |
+-----------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)
mysql> show grants for scm;

mysql> show grants for scm;
+-------------------------------------------------------------------------------------------------------------+
| Grants for scm@%                                                                                            |
+-------------------------------------------------------------------------------------------------------------+
| GRANT ALL PRIVILEGES ON *.* TO 'scm'@'ip-172-31-23-172..eu-central-1.compute.internal' IDENTIFIED BY PASSWORD '*45E6E3C68BDF1AC7EBB5C5A3BCBD5E9437B293BE' |
+-------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)


Create user directories in HDFS for bavaria and saxony
sudo -u hdfs hdfs dfs -mkdir /user/bavaria
sudo -u hdfs hdfs dfs -mkdir /user/saxony

hdfs dfs -ls /user

http://35.156.92.123:7180/api/v12/hosts

    
    Login to the Hue console and install the Hive sample data

    Save a screenshot of the Hue home page into challenges/labs/3_hue_installed.png
