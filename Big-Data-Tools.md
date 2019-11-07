# Big Data Tools

Apache HADOOP, if you download, you will get HDFS, Yarn & Map Reduce.

In the world of HADOOP we rarely do ETL, we actually do ELT.

* **SQOOP** - SQOOP is used to bring data from any SQL system to HADOOP. It can take from Oracale, MySQL etc. Its an Apache light weight tool. 
* **Flume** - Most popular Apache tool for pulling the unstructured data i.e. JSON, XML etc to HDFS. It is point to point. Doesn't store the data anywhere permanently. It is pull based.
* **KAFKA** - Its a messaging system, which can store data for 7 days by default. Multiple systems can goto kafka to get the data. It can't pull the data automatically, we need kafka producer to push the data.
* **Spark Streming/Flink/Storm** - Used for real time processing. Spark Streaming is a library in Spark. Spark Streaming can process batch, Storm can process single transaction.
* **Hive** - It is a tool in HDFS, used for processing data.
* **MR** - Map Reduce, processing the data on HDFS.
* **Pig** - Almost gone from market, scripting tool on Hadoop. 
* **Hive** - Used to write query on data, which is getting internally converted into Map Reduce.
* **Spark** - Faster than Map Reduce, near to real time processing.
* **Impala/HAWK, LLAP/Presto/DRILL/PHENOIX** - It can connect with HDFS, & used to query particular records & this is very fast. Impala is on Cloudera. HAWK is on Horton Works.
* **HBase** - It is installed on HDFS, it can do random read & writes. It is no SQL db of HADOOP. It has its own language. Phoneix is SQL on HBase. This will be OLTP system in HADOOP.
**ELK** - Elastic Log Stash Kibana, it is not in HADOOP ecosystem.

If you get commercial HADDOP from Cloudera, you get all the above.
