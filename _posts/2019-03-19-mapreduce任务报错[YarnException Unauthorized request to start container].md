---
layout: post
title:  "mapreduce任务启动时，报错YarnException Unauthorized request to start container"
date:   2019-3-19 15:55
categories: mapreduce
tags: mapreduce 报错
---

* content
{:toc}

执行MapReduce任务时，出现如下报错：
```
[root@master mapreduce_wordcount_python]# bash run.sh 
rmr: DEPRECATED: Please use 'rm -r' instead.
rmr: `/output': No such file or directory
19/02/15 14:50:20 WARN streaming.StreamJob: -file option is deprecated, please use generic option -files instead.
packageJobJar: [./map_new.py, ./red_new.py, /tmp/hadoop-unjar1610102638531802348/] [] /tmp/streamjob2624593896310271836.jar tmpDir=null
19/02/15 14:50:21 INFO client.RMProxy: Connecting to ResourceManager at master/192.168.211.10:8032
19/02/15 14:50:21 INFO client.RMProxy: Connecting to ResourceManager at master/192.168.211.10:8032
19/02/15 14:50:22 INFO mapred.FileInputFormat: Total input paths to process : 1
19/02/15 14:50:22 INFO mapreduce.JobSubmitter: number of splits:2
19/02/15 14:50:22 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1550239813206_0002
19/02/15 14:50:23 INFO impl.YarnClientImpl: Submitted application application_1550239813206_0002
19/02/15 14:50:23 INFO mapreduce.Job: The url to track the job: http://master:8088/proxy/application_1550239813206_0002/
19/02/15 14:50:23 INFO mapreduce.Job: Running job: job_1550239813206_0002
19/02/15 14:50:24 INFO mapreduce.Job: Job job_1550239813206_0002 running in uber mode : false
19/02/15 14:50:24 INFO mapreduce.Job:  map 0% reduce 0%
19/02/15 14:50:24 INFO mapreduce.Job: Job job_1550239813206_0002 failed with state FAILED due to: Application application_1550239813206_0002 failed 2 times due to Error launching appattempt_1550239813206_0002_000002. Got exception: org.apache.hadoop.yarn.exceptions.YarnException: Unauthorized request to start container. 
This token is expired. current time is 1550242223020 found 1550214024349
Note: System times on machines may be out of sync. Check system time and time zones.
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at org.apache.hadoop.yarn.api.records.impl.pb.SerializedExceptionPBImpl.instantiateException(SerializedExceptionPBImpl.java:168)
	at org.apache.hadoop.yarn.api.records.impl.pb.SerializedExceptionPBImpl.deSerialize(SerializedExceptionPBImpl.java:106)
	at org.apache.hadoop.yarn.server.resourcemanager.amlauncher.AMLauncher.launch(AMLauncher.java:123)
	at org.apache.hadoop.yarn.server.resourcemanager.amlauncher.AMLauncher.run(AMLauncher.java:251)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
. Failing the application.
19/02/15 14:50:24 INFO mapreduce.Job: Counters: 0
19/02/15 14:50:24 ERROR streaming.StreamJob: Job not successful!
Streaming Command Failed!
```

在网上查了下报错，见[链接](https://stackoverflow.com/questions/20257878/yarnexception-unauthorized-request-to-start-container)

问题原因为：
```
This exception occurs when your nodes have different time settings. Make sure that your all 3 nodes have same time n timezone settings and then restart computer.
```

我检查了我的集群，确实发现集群各节点时间不对。

修改好时间，并做好ntpdate同步后，我未重启集群 ，直接重新执行，任务正常