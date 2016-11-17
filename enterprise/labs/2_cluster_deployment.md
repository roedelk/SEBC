{
  "timestamp" : "2016-11-17T21:27:04.446Z",
  "clusters" : [ {
    "name" : "roedelk",
    "version" : "CDH5",
    "services" : [ {
      "name" : "hive",
      "type" : "HIVE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "HIVEMETASTORE",
          "items" : [ {
            "name" : "hive_metastore_java_heapsize",
            "value" : "609222656"
          } ]
        }, {
          "roleType" : "HIVESERVER2",
          "items" : [ {
            "name" : "hiveserver2_enable_impersonation",
            "value" : "false"
          }, {
            "name" : "hiveserver2_java_heapsize",
            "value" : "609222656"
          }, {
            "name" : "hiveserver2_spark_driver_memory",
            "value" : "966367641"
          }, {
            "name" : "hiveserver2_spark_executor_cores",
            "value" : "4"
          }, {
            "name" : "hiveserver2_spark_executor_memory",
            "value" : "3545550028"
          }, {
            "name" : "hiveserver2_spark_yarn_driver_memory_overhead",
            "value" : "102"
          }, {
            "name" : "hiveserver2_spark_yarn_executor_memory_overhead",
            "value" : "596"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_metastore_database_host",
          "value" : "ip-172-31-21-228.eu-central-1.compute.internal"
        }, {
          "name" : "hive_metastore_database_password",
          "value" : "hive_password"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "sentry_service",
          "value" : "sentry"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hive-GATEWAY-814791c316b87d184d94652383ed405f",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-088358a9ac223d890"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-a799deb281ea5211814ee438fe122f67",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-07f52dadbf5cd7a55"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-d8368b89b2af69471f8a9680f8eb2888",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0373b77bc0c4f2aad"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-db0140dd59c4b54bc7ac49b6afc90b67",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0fd70d7646bc6b84f"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-HIVEMETASTORE-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "HIVEMETASTORE",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "d17lym016ki1nohu565u3dq2q"
          } ]
        }
      }, {
        "name" : "hive-HIVESERVER2-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "HIVESERVER2",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "c5xhgok12n5s0mdbds5mywuss"
          } ]
        }
      } ],
      "displayName" : "Hive"
    }, {
      "name" : "zookeeper",
      "type" : "ZOOKEEPER",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "SERVER",
          "items" : [ {
            "name" : "zookeeper_server_java_heapsize",
            "value" : "609222656"
          } ]
        } ],
        "items" : [ {
          "name" : "enableSecurity",
          "value" : "true"
        } ]
      },
      "roles" : [ {
        "name" : "zookeeper-SERVER-814791c316b87d184d94652383ed405f",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-088358a9ac223d890"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "4i3blqshgeiumhs5mjv6732uz"
          }, {
            "name" : "serverId",
            "value" : "3"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "98zkdwv4uwavxe41eytrnuf6y"
          }, {
            "name" : "serverId",
            "value" : "2"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-d8368b89b2af69471f8a9680f8eb2888",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-0373b77bc0c4f2aad"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "lx7p0p2xz0dk6ytkvxnwikxq"
          }, {
            "name" : "serverId",
            "value" : "1"
          } ]
        }
      } ],
      "displayName" : "ZooKeeper"
    }, {
      "name" : "hue",
      "type" : "HUE",
      "config" : {
        "roleTypeConfigs" : [ ],
        "items" : [ {
          "name" : "database_host",
          "value" : "ip-172-31-21-228.eu-central-1.compute.internal"
        }, {
          "name" : "database_password",
          "value" : "pwd"
        }, {
          "name" : "database_type",
          "value" : "mysql"
        }, {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "hue_webhdfs",
          "value" : "hdfs-NAMENODE-bc46bdf8189aba5b3180e187d07b88db"
        }, {
          "name" : "oozie_service",
          "value" : "oozie"
        }, {
          "name" : "sentry_service",
          "value" : "sentry"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hue-HUE_SERVER-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "HUE_SERVER",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "5eh3j0t8k0prtylacmqna40bg"
          }, {
            "name" : "secret_key",
            "value" : "WQ95xvGfoCvTYBFxpo4DRebZKoQfZv"
          } ]
        }
      }, {
        "name" : "hue-KT_RENEWER-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "KT_RENEWER",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "8r0xyv6q1ic1n4wl9utxks468"
          } ]
        }
      } ],
      "displayName" : "Hue"
    }, {
      "name" : "oozie",
      "type" : "OOZIE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "OOZIE_SERVER",
          "items" : [ {
            "name" : "oozie_database_host",
            "value" : "ip-172-31-21-228.eu-central-1.compute.internal"
          }, {
            "name" : "oozie_database_password",
            "value" : "oozie"
          }, {
            "name" : "oozie_database_type",
            "value" : "mysql"
          }, {
            "name" : "oozie_database_user",
            "value" : "oozie"
          }, {
            "name" : "oozie_java_heapsize",
            "value" : "609222656"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "oozie-OOZIE_SERVER-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "OOZIE_SERVER",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "dian40k6kgqhflrh0jdoq5hy8"
          } ]
        }
      } ],
      "displayName" : "Oozie"
    }, {
      "name" : "yarn",
      "type" : "YARN",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "mapred_reduce_tasks",
            "value" : "8"
          }, {
            "name" : "mapred_submit_replication",
            "value" : "2"
          } ]
        }, {
          "roleType" : "JOBHISTORY",
          "items" : [ {
            "name" : "mr2_jobhistory_java_heapsize",
            "value" : "609222656"
          } ]
        }, {
          "roleType" : "NODEMANAGER",
          "items" : [ {
            "name" : "yarn_nodemanager_heartbeat_interval_ms",
            "value" : "100"
          }, {
            "name" : "yarn_nodemanager_local_dirs",
            "value" : "/yarn/nm"
          }, {
            "name" : "yarn_nodemanager_log_dirs",
            "value" : "/yarn/container-logs"
          }, {
            "name" : "yarn_nodemanager_resource_cpu_vcores",
            "value" : "4"
          }, {
            "name" : "yarn_nodemanager_resource_memory_mb",
            "value" : "5192"
          } ]
        }, {
          "roleType" : "RESOURCEMANAGER",
          "items" : [ {
            "name" : "resource_manager_java_heapsize",
            "value" : "609222656"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_mb",
            "value" : "5192"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_vcores",
            "value" : "3"
          } ]
        } ],
        "items" : [ {
          "name" : "hdfs_service",
          "value" : "hdfs"
        }, {
          "name" : "rm_dirty",
          "value" : "false"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "90"
        }, {
          "name" : "yarn_service_cgroups",
          "value" : "false"
        }, {
          "name" : "yarn_service_lce_always",
          "value" : "false"
        }, {
          "name" : "zk_authorization_secret_key",
          "value" : "BTheRr3O9rDM7G53eCV7h5azDOigiK"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "yarn-JOBHISTORY-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "JOBHISTORY",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "8ay9vo46vbzp1ctkh4h4hgqkz"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-814791c316b87d184d94652383ed405f",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-088358a9ac223d890"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "4ywrxdrouzfy6iozq19h8w3d8"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-a799deb281ea5211814ee438fe122f67",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-07f52dadbf5cd7a55"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "8kuotdao6ct032lx10qndk12b"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-d8368b89b2af69471f8a9680f8eb2888",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-0373b77bc0c4f2aad"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "cdjlob9jgc68akt8047b59y6w"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-db0140dd59c4b54bc7ac49b6afc90b67",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-0fd70d7646bc6b84f"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "ahos6s0jx32xv0egqd5fiwto4"
          } ]
        }
      }, {
        "name" : "yarn-RESOURCEMANAGER-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "RESOURCEMANAGER",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "rm_id",
            "value" : "53"
          }, {
            "name" : "role_jceks_password",
            "value" : "f1y38uo3zn5uddncxr00co773"
          } ]
        }
      } ],
      "displayName" : "YARN (MR2 Included)"
    }, {
      "name" : "hdfs",
      "type" : "HDFS",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "BALANCER",
          "items" : [ {
            "name" : "balancer_java_heapsize",
            "value" : "609222656"
          } ]
        }, {
          "roleType" : "DATANODE",
          "items" : [ {
            "name" : "dfs_data_dir_list",
            "value" : "/dfs/dn"
          }, {
            "name" : "dfs_datanode_data_dir_perm",
            "value" : "700"
          }, {
            "name" : "dfs_datanode_du_reserved",
            "value" : "7384732876"
          }, {
            "name" : "dfs_datanode_http_port",
            "value" : "1006"
          }, {
            "name" : "dfs_datanode_max_locked_memory",
            "value" : "4294967296"
          }, {
            "name" : "dfs_datanode_port",
            "value" : "1004"
          } ]
        }, {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "dfs_client_use_trash",
            "value" : "true"
          } ]
        }, {
          "roleType" : "NAMENODE",
          "items" : [ {
            "name" : "dfs_name_dir_list",
            "value" : "/dfs/nn"
          }, {
            "name" : "dfs_namenode_servicerpc_address",
            "value" : "8022"
          }, {
            "name" : "namenode_java_heapsize",
            "value" : "1073741824"
          } ]
        }, {
          "roleType" : "SECONDARYNAMENODE",
          "items" : [ {
            "name" : "fs_checkpoint_dir_list",
            "value" : "/dfs/snn"
          }, {
            "name" : "secondary_namenode_java_heapsize",
            "value" : "1073741824"
          } ]
        } ],
        "items" : [ {
          "name" : "dfs_client_use_datanode_hostname",
          "value" : "true"
        }, {
          "name" : "dfs_encrypt_data_transfer_algorithm",
          "value" : "AES/CTR/NoPadding"
        }, {
          "name" : "dfs_ha_fencing_cloudera_manager_secret_key",
          "value" : "MdIpcDbCYEvaUwBJ3A6Ffm5rD4t5vk"
        }, {
          "name" : "fc_authorization_secret_key",
          "value" : "uc0wKL2AzWXgQ6I8l1hPm0Env3Wxss"
        }, {
          "name" : "hadoop_security_authentication",
          "value" : "kerberos"
        }, {
          "name" : "hadoop_security_authorization",
          "value" : "true"
        }, {
          "name" : "http_auth_signature_secret",
          "value" : "d5YbKCBz5FuSgu20IXUyaJ0qYp1tBk"
        }, {
          "name" : "rm_dirty",
          "value" : "false"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "10"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hdfs-BALANCER-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "BALANCER",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-DATANODE-814791c316b87d184d94652383ed405f",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-088358a9ac223d890"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "1z00jif7lhzdeh2m0ui0aoljw"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-a799deb281ea5211814ee438fe122f67",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-07f52dadbf5cd7a55"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "b3bjuousd0p9detymzebdk34f"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-d8368b89b2af69471f8a9680f8eb2888",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-0373b77bc0c4f2aad"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "e57mvad8vxx9xxgc7lv2jd4n7"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-db0140dd59c4b54bc7ac49b6afc90b67",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-0fd70d7646bc6b84f"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "5v4fqdbt99v58v9cp1vv7jlli"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "namenode_id",
            "value" : "55"
          }, {
            "name" : "role_jceks_password",
            "value" : "98f6qn82r48b3s057lxvev2d"
          } ]
        }
      }, {
        "name" : "hdfs-SECONDARYNAMENODE-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "SECONDARYNAMENODE",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2ry4d4sarl2qio71qfa8jsmee"
          } ]
        }
      } ],
      "displayName" : "HDFS"
    }, {
      "name" : "sentry",
      "type" : "SENTRY",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "SENTRY_SERVER",
          "items" : [ {
            "name" : "sentry_server_java_heapsize",
            "value" : "268435456"
          } ]
        } ],
        "items" : [ {
          "name" : "hdfs_service",
          "value" : "hdfs"
        }, {
          "name" : "sentry_server_database_host",
          "value" : "ip-172-31-21-228.eu-central-1.compute.internal"
        }, {
          "name" : "sentry_server_database_password",
          "value" : "sentry_password"
        }, {
          "name" : "sentry_service_admin_group",
          "value" : "hive,kmem,impala,hue,solr"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "sentry-GATEWAY-814791c316b87d184d94652383ed405f",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-088358a9ac223d890"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "sentry-GATEWAY-a799deb281ea5211814ee438fe122f67",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-07f52dadbf5cd7a55"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "sentry-GATEWAY-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "sentry-GATEWAY-d8368b89b2af69471f8a9680f8eb2888",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0373b77bc0c4f2aad"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "sentry-GATEWAY-db0140dd59c4b54bc7ac49b6afc90b67",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0fd70d7646bc6b84f"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "sentry-SENTRY_SERVER-bc46bdf8189aba5b3180e187d07b88db",
        "type" : "SENTRY_SERVER",
        "hostRef" : {
          "hostId" : "i-0f2ef18fbe6530cf1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "4n41pd7crxi6b6hgdir94zba6"
          } ]
        }
      } ],
      "displayName" : "Sentry"
    } ]
  } ],
  "hosts" : [ {
    "hostId" : "i-0f2ef18fbe6530cf1",
    "ipAddress" : "172.31.21.227",
    "hostname" : "ip-172-31-21-227.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-0373b77bc0c4f2aad",
    "ipAddress" : "172.31.21.228",
    "hostname" : "ip-172-31-21-228.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-088358a9ac223d890",
    "ipAddress" : "172.31.21.229",
    "hostname" : "ip-172-31-21-229.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-0fd70d7646bc6b84f",
    "ipAddress" : "172.31.21.230",
    "hostname" : "ip-172-31-21-230.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-07f52dadbf5cd7a55",
    "ipAddress" : "172.31.21.231",
    "hostname" : "ip-172-31-21-231.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  } ],
  "users" : [ {
    "name" : "__cloudera_internal_user__afbaa67b-e7f4-4147-97a7-3b56264df82b",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "a2a4852d5bdbc7f6627661c13bec176593709c0e7e5ce39e0c6ca58087190c47",
    "pwSalt" : -5759457560105295589,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-EVENTSERVER-bc46bdf8189aba5b3180e187d07b88db",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "0e2d41adb002f8da1f2ff0a37eac92f85035e7a13579073d2f14ca6e6730bf03",
    "pwSalt" : -5046766967462823566,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-HOSTMONITOR-bc46bdf8189aba5b3180e187d07b88db",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "374ee2e1f70cb814007a2b429624a1015f575c22470e2dcef46d68ccf9fb0d95",
    "pwSalt" : 1469920814478149333,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-REPORTSMANAGER-bc46bdf8189aba5b3180e187d07b88db",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "c4e7475a4cd2d1c5ef0a34f645178406b26992fc77c576c97280fd125c65a77a",
    "pwSalt" : -700667276227624368,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-SERVICEMONITOR-bc46bdf8189aba5b3180e187d07b88db",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "3416ba932332d80f2e9d0987dfb84d3a9975a074358eb3f86f9a379bf4c9a528",
    "pwSalt" : -4931979956031303118,
    "pwLogin" : true
  }, {
    "name" : "admin",
    "roles" : [ "ROLE_ADMIN" ],
    "pwHash" : "fb98d588744a01ce1d20c9bba707bd356ae8f0c012562617cdb90fe7fd61ca9c",
    "pwSalt" : -1403442192030265595,
    "pwLogin" : true
  }, {
    "name" : "gioconte",
    "roles" : [ "ROLE_USER_ADMIN" ],
    "pwHash" : "e8d662bd6c980edf849e1a997b90877d00e6ee6d9a03898948513752ce92b279",
    "pwSalt" : 3313959613430194080,
    "pwLogin" : true
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ],
    "pwHash" : "1e6044676f986f29df8b16924fb0f8e650d9262a2849300c346277a41a89f6c2",
    "pwSalt" : -4931659173860171347,
    "pwLogin" : true
  }, {
    "name" : "roedelk",
    "roles" : [ "ROLE_USER_ADMIN" ],
    "pwHash" : "80b9629c519134fb8f39b5b8f2a4d8799aea5c90eb730c8cd5b1d6decb5ac025",
    "pwSalt" : -7637670612389994247,
    "pwLogin" : true
  } ],
  "versionInfo" : {
    "version" : "5.9.0",
    "buildUser" : "jenkins",
    "buildTimestamp" : "20161006-1801",
    "gitHash" : "898a5e032c080e18833dfc58180761f6ef2ea351",
    "snapshot" : false
  },
  "managementService" : {
    "name" : "mgmt",
    "type" : "MGMT",
    "config" : {
      "roleTypeConfigs" : [ {
        "roleType" : "EVENTSERVER",
        "items" : [ {
          "name" : "event_server_heapsize",
          "value" : "609222656"
        } ]
      }, {
        "roleType" : "HOSTMONITOR",
        "items" : [ {
          "name" : "firehose_heapsize",
          "value" : "609222656"
        }, {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "805306368"
        } ]
      }, {
        "roleType" : "REPORTSMANAGER",
        "items" : [ {
          "name" : "headlamp_database_host",
          "value" : "ip-172-31-21-228.eu-central-1.compute.internal"
        }, {
          "name" : "headlamp_database_name",
          "value" : "rman"
        }, {
          "name" : "headlamp_database_password",
          "value" : "rman_password"
        }, {
          "name" : "headlamp_database_user",
          "value" : "rman"
        }, {
          "name" : "headlamp_heapsize",
          "value" : "609222656"
        } ]
      }, {
        "roleType" : "SERVICEMONITOR",
        "items" : [ {
          "name" : "firehose_heapsize",
          "value" : "609222656"
        }, {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "805306368"
        } ]
      } ],
      "items" : [ ]
    },
    "roles" : [ {
      "name" : "mgmt-ALERTPUBLISHER-bc46bdf8189aba5b3180e187d07b88db",
      "type" : "ALERTPUBLISHER",
      "hostRef" : {
        "hostId" : "i-0f2ef18fbe6530cf1"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "5gbh9494uwiutfsh41dbgxbnk"
        } ]
      }
    }, {
      "name" : "mgmt-EVENTSERVER-bc46bdf8189aba5b3180e187d07b88db",
      "type" : "EVENTSERVER",
      "hostRef" : {
        "hostId" : "i-0f2ef18fbe6530cf1"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "ekxl17ozaim6vohgrvkumu8xf"
        } ]
      }
    }, {
      "name" : "mgmt-HOSTMONITOR-bc46bdf8189aba5b3180e187d07b88db",
      "type" : "HOSTMONITOR",
      "hostRef" : {
        "hostId" : "i-0f2ef18fbe6530cf1"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "evp9exi0vokjdohfpc2qkymo8"
        } ]
      }
    }, {
      "name" : "mgmt-REPORTSMANAGER-bc46bdf8189aba5b3180e187d07b88db",
      "type" : "REPORTSMANAGER",
      "hostRef" : {
        "hostId" : "i-0f2ef18fbe6530cf1"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "avpr21qphg6zcpuepgja7306m"
        } ]
      }
    }, {
      "name" : "mgmt-SERVICEMONITOR-bc46bdf8189aba5b3180e187d07b88db",
      "type" : "SERVICEMONITOR",
      "hostRef" : {
        "hostId" : "i-0f2ef18fbe6530cf1"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "47tdb7xae3vnoxz2ccz2gmhuq"
        } ]
      }
    } ],
    "displayName" : "Cloudera Management Service"
  },
  "managerSettings" : {
    "items" : [ {
      "name" : "AD_USE_SIMPLE_AUTH",
      "value" : "false"
    }, {
      "name" : "CLUSTER_STATS_START",
      "value" : "10/24/2012 20:40"
    }, {
      "name" : "KDC_ADMIN_PASSWORD",
      "value" : "BQIAAAA3AAEACFNWQUcuQ09NAAxjbG91ZGVyYS1zY20AAAABWC2PRAEAFwAQjqDrjL4DYOf/zgs2Koyd6Q=="
    }, {
      "name" : "KDC_ADMIN_USER",
      "value" : "cloudera-scm@SVAG.COM"
    }, {
      "name" : "KDC_HOST",
      "value" : "172.31.21.228"
    }, {
      "name" : "KRB_ENC_TYPES",
      "value" : "arcfour-hmac"
    }, {
      "name" : "KRB_MANAGE_KRB5_CONF",
      "value" : "true"
    }, {
      "name" : "MAX_RENEW_LIFE",
      "value" : "604800"
    }, {
      "name" : "PUBLIC_CLOUD_STATUS",
      "value" : "ON_PUBLIC_CLOUD"
    }, {
      "name" : "REMOTE_PARCEL_REPO_URLS",
      "value" : "https://archive.cloudera.com/cdh5/parcels/5.8.2/,https://archive.cloudera.com/cdh4/parcels/5.8.2/,https://archive.cloudera.com/impala/parcels/5.8.2/,https://archive.cloudera.com/search/parcels/5.8.2/,https://archive.cloudera.com/accumulo/parcels/1.4/,https://archive.cloudera.com/accumulo-c5/parcels/5.8.2/,https://archive.cloudera.com/kafka/parcels/5.8.2/,https://archive.cloudera.com/navigator-keytrustee5/parcels/5.8.2/,https://archive.cloudera.com/spark/parcels/5.8.2/,https://archive.cloudera.com/sqoop-connectors/parcels/5.8.2/,https://archive.cloudera.com/accumulo-c5/parcels/latest/,https://archive.cloudera.com/kafka/parcels/latest/,https://archive.cloudera.com/navigator-keytrustee5/parcels/latest/,https://archive.cloudera.com/spark/parcels/latest/,https://archive.cloudera.com/sqoop-connectors/parcels/latest/"
    }, {
      "name" : "SECURITY_REALM",
      "value" : "SVAG.COM"
    } ]
  }
}