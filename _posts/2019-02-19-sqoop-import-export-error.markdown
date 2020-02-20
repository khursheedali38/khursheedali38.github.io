---
layout: post
title: "Sqoop import and export error"
date: 2019-02-19 +00:50:39 -0500
categories: HDP Sandbox, Hadoop
tags: sqoop, import, export, error
---

As a beginner to HDP sandbox learning, you might be going through Hive and MySQL tutorials. While a lot of you might pretty well follow along with them, you might encounter some errors during runtime. This blog post covers some of those errors and their solutions.

For debugging the errors you encounter, you can view logs of that particular job. For example, import and export are done as mapreduce jobs with an `applicationId` for the job, you can query `YARN` for the logs as follows:

```shell
shell> yarn logs -applicationId  application_1485423751090_3566 > app_logs.txt
```

The above writes the error log into the file and you can view it.

## Sqoop import errors

### Logging initialization

The common sqoop import errors occur during import to hive particularly. Most common of them being the *log initializing getting decade to finish*, this is at times due to VM configs, and tough to troubleshoot.

A quick work around for this error is to *restart the vm*.

#### AccessBasedControl: User null

These occur because during import sqoop creates temporary files and need s access to hdfs. If you run the import task with a user who doesn't have the permission to access, then you would get this error.

To overcome this, you need to run the import task with the right user such as a `hdfs` or `hive` user. Change that as follows:

```shell
shell> sudo root
shell> sudo - hdfs
```

## Sqoop export errors

### Failed task due to other tasks failed | Export job failed

This can be due to various reasons, check the log via `yarn` as described above. It is mostly if the map job isn't able to parse your input. You should see the log as having `Can't parse input data..`. 

This may be due to incorrect `input-field-teminated-by` parameter given. You should correctly specify the delimiter of the hive table to be exported. You can check the delimiter as follows from hive view, the default delimiter is `\0001`.

```sql
hive> DESCRIBE EXTENDED <table_name>;
```

For a clean output you can also get the delmiter as 

```sql
hive> SHOW CREATE TABLE <table_name>;
```
