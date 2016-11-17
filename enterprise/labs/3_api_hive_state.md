 
# http://cloudera.github.io/cm_api/apidocs/v12/tutorial.html
 
# Stop command
$ curl -X POST -u admin:admin 'http://35.156.75.11:7180/api/v1/clusters/roedelk/services/hive/commands/stop'

[ec2-user@ip-172-31-21-230 ~]$ curl -X POST -u admin:admin 'http://35.156.75.11:7180/api/v1/clusters/roedelk/services/hive/commands/stop'
{
  "id" : 478,
  "name" : "Stop",
  "startTime" : "2016-11-17T21:55:58.749Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
  
# Service State 
[ec2-user@ip-172-31-21-230 ~]$ curl u admin:admin 'http://35.156.75.11:7180/api/v1/clusters/roedelk/services/hive''
{
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://ip-172-31-21-228.eu-central-1.compute.internal:7180/cmf/serviceRedirect/hive",
  "serviceState" : "STOPPED",
  "healthSummary" : "DISABLED",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "DISABLED"
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "DISABLED"
  } ],
  "configStale" : false

# Start command 
[ec2-user@ip-172-31-21-230 ~]$ curl -X POST -u admin:admin 'http://35.156.75.11:7180/api/v1/clusters/roedelk/services/hive/commands/start'
{
  "id" : 483,
  "name" : "Start",
  "startTime" : "2016-11-17T21:56:41.696Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }

# Service State 
[ec2-user@ip-172-31-21-230 ~]$ curl -u admin:admin 'http://35.156.75.11:7180/api/v1/clusters/roedelk/services/hive'
{
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://ip-172-31-21-228.eu-central-1.compute.internal:7180/cmf/serviceRedirect/hive",
  "serviceState" : "STARTED",
  "healthSummary" : "GOOD",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "GOOD"
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "GOOD"
  } ],
  "configStale" : false
