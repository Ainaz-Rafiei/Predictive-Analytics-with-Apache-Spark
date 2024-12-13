
# Functioning Cloud setup

This setup demonstrates a Spark-based data processing pipeline in Hadoop and HDFS, following the Medallion Architecture, consists of:

- Bronze Layer: Raw unstructured data.
- Silver Layer: Cleaned and transformed Parquet files.
- Gold Layer: Delta tables for analytics and updates.

The pipeline runs on OpenStack, with data stored in HDFS using Spark.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Hadoop and HDFS](#hadoop-and-hdfs)
3. [Spark UI](#spark-ui)
4. [Troubleshooting Hadoop and Spark Cluster Setup](#troubleshooting-hadoop-and-spark-cluster-setup)




## Prerequisites
To start the setup, ensure you have:

- Access to the OpenStack environment.
- SSH key to log into the master node.
- Hadoop and Spark installed and running.

Data available in the HDFS paths:

1- Bronze: 
```
/user/ubuntu/FinalProject/Unstructured_Price_paid_records
```
2- Silver:
```
 /user/ubuntu/FinalProject/Parquet_Clean_Data
 
```
3- Gold: 
```
/user/ubuntu/FinalProject/Delta_trainData
 
/user/ubuntu/FinalProject/Delta_testData

```



## Hadoop and HDFS


#### log into the Hadoop environment:

```
ssh ubuntu@152.94.163.65 -i ~/.ssh/ssh_key.pem
```


## HDFS Paths


#### View Directory Contents

```
hdfs dfs -ls /user/ubuntu/FinalProject
```


## Verify HDFS Data Paths


- Check the Raw Data in Bronze Layer:

```
hdfs dfs -ls /user/ubuntu/FinalProject/Unstructured_Price_paid_records
```

- Verify Cleaned Data in Silver Layer:

```
hdfs dfs -ls /user/ubuntu/FinalProject/Parquet_Clean_Data
```

- Inspect Delta Tables in Gold Layer:

Training:

```
hdfs dfs -ls /user/ubuntu/FinalProject/Delta_trainData
```
Testing:
```
hdfs dfs -ls /user/ubuntu/FinalProject/Delta_testData
```

## Spark UI

- Start the Spark History Server to monitor jobs:
```
$SPARK_HOME/sbin/start-history-server.sh
```

- Access the Spark UI: 
```
http://152.94.163.65:18080
```


## Troubleshooting Hadoop and Spark Cluster Setup
If you encounter issues, consider the following:
### 1.Handleing the port 22: Connection timed out by reboot hard the namenode in OpenStack
```
start-dfs.sh
```
### 2. Check for the existing Hadoop
```
systemctl list-units --type=service | grep hadoop
```
### 3. If there is not Haddoop restart Hadoop
```
$HADOOP_HOME/sbin/stop-dfs.sh
$HADOOP_HOME/sbin/start-dfs.sh
```
### 4. Check the hdfs status and  exist dataset
```
hdfs dfsadmin -report
```
```
hdfs dfs -ls /user/ubuntu/FinalProject/Unstructured_Price_paid_records/
```
### 5. Allow the cluster to start accepting write operations
```
hdfs dfsadmin -safemode leave
```
