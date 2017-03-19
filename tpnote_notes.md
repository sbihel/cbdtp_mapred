# Summary
- Speculation enabled
    - Normal                                                          -> 270s
    - Normal with expiry interval of 30s and slowstart 0.05 (10GB)    -> 295s
    - Normal with expiry interval of 30s and slowstart 0.5 (10GB)     -> 311s
    - Normal with expiry interval of 30s and slowstart 1 (10GB)       -> 344s
    - CPU stress (hanoi on one node)                                  -> 284s
    - CPU stress (stress --cpu 16 command on one node)                -> 292s
    - Disk stress (script provided on one node)                       -> 292s
    - Death during map (20%)                                          -> 945s
    - Death during map (20%) with expiry interval of 30s              -> 382s
    - Death during map (20%) with expiry interval of 60s              -> 502s
    - Death after map (reduce 46%)                                    -> 904s
    - Death after map (reduce 32%) with expiry interval of 30s        -> 469s
    - Death after map (reduce 31%) with expiry interval of 60s        -> 367s
    - Wordcount normal with expiry interval of 30s                    -> 834s (?)
    - Wordcount normal with expiry interval of 30s and slowstart 0.05 -> 835s (?)
    - Wordcount normal with expiry interval of 30s and slowstart 0.5  -> 857s (?)
    - Wordcount normal with expiry interval of 30s and slowstart 1    -> 917s (?)
- Speculation disable
    - Normal                                                          -> 317s
    - CPU stress (hanoi on one node)                                  -> 305s
    - CPU stress (stress --cpu 16 on one node)                        -> 332s
    - Disk stress (script provided on one node)                       -> 369s
    - Death during map (20%)                                          -> 849s
    - Death during map (20%) with expiry interval of 30s              -> 446s
    - Death during map (20%) with expiry interval of 60s              -> 394s
    - Death after map (reduce 32%)                                    -> 911s
    - Death after map (reduce 31%) with expiry interval of 30s        -> 477s
    - Death after map (reduce 32%) with expiry interval of 60s        -> 419s


# Speculation enabled
## Normal
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 18:39:11 UTC 2017
17/03/16 18:39:11 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 18:39:12 INFO mapred.JobClient: Running job: job_201703161829_0002
17/03/16 18:39:13 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 18:39:19 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 18:39:22 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 18:39:25 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 18:39:26 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 18:39:29 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 18:39:31 INFO mapred.JobClient: Task Id : attempt_201703161829_0002_r_000003_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 18:39:31 INFO mapred.JobClient: Task Id : attempt_201703161829_0002_r_000001_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 18:39:32 INFO mapred.JobClient:  map 11% reduce 0%
17/03/16 18:39:33 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 18:39:36 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 18:39:39 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 18:39:42 INFO mapred.JobClient:  map 18% reduce 4%
17/03/16 18:39:43 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 18:39:45 INFO mapred.JobClient:  map 19% reduce 5%
17/03/16 18:39:46 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 18:39:48 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 18:39:49 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 18:39:52 INFO mapred.JobClient:  map 25% reduce 6%
17/03/16 18:39:53 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 18:39:54 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 18:39:56 INFO mapred.JobClient:  map 28% reduce 7%
17/03/16 18:39:57 INFO mapred.JobClient:  map 29% reduce 8%
17/03/16 18:39:59 INFO mapred.JobClient:  map 30% reduce 8%
17/03/16 18:40:00 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 18:40:03 INFO mapred.JobClient:  map 34% reduce 9%
17/03/16 18:40:06 INFO mapred.JobClient:  map 34% reduce 10%
17/03/16 18:40:07 INFO mapred.JobClient:  map 37% reduce 10%
17/03/16 18:40:09 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 18:40:11 INFO mapred.JobClient:  map 39% reduce 11%
17/03/16 18:40:13 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 18:40:14 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 18:40:18 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 18:40:21 INFO mapred.JobClient:  map 45% reduce 13%
17/03/16 18:40:22 INFO mapred.JobClient:  map 47% reduce 13%
17/03/16 18:40:24 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 18:40:25 INFO mapred.JobClient:  map 48% reduce 14%
17/03/16 18:40:26 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 18:40:27 INFO mapred.JobClient:  map 49% reduce 15%
17/03/16 18:40:28 INFO mapred.JobClient:  map 50% reduce 15%
17/03/16 18:40:29 INFO mapred.JobClient:  map 51% reduce 15%
17/03/16 18:40:30 INFO mapred.JobClient:  map 52% reduce 15%
17/03/16 18:40:31 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 18:40:33 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 18:40:34 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 18:40:35 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 18:40:37 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 18:40:38 INFO mapred.JobClient:  map 58% reduce 17%
17/03/16 18:40:40 INFO mapred.JobClient:  map 58% reduce 18%
17/03/16 18:40:41 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 18:40:42 INFO mapred.JobClient:  map 60% reduce 18%
17/03/16 18:40:43 INFO mapred.JobClient:  map 61% reduce 18%
17/03/16 18:40:44 INFO mapred.JobClient:  map 62% reduce 18%
17/03/16 18:40:46 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 18:40:47 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 18:40:50 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 18:40:51 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 18:40:52 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 18:40:54 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 18:40:56 INFO mapred.JobClient:  map 69% reduce 22%
17/03/16 18:40:58 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 18:40:59 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 18:41:01 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 18:41:03 INFO mapred.JobClient:  map 74% reduce 22%
17/03/16 18:41:04 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 18:41:05 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 18:41:06 INFO mapred.JobClient:  map 76% reduce 24%
17/03/16 18:41:07 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 18:41:08 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 18:41:10 INFO mapred.JobClient:  map 79% reduce 24%
17/03/16 18:41:11 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 18:41:12 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 18:41:14 INFO mapred.JobClient:  map 81% reduce 26%
17/03/16 18:41:15 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 18:41:17 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 18:41:18 INFO mapred.JobClient:  map 84% reduce 26%
17/03/16 18:41:19 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 18:41:20 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 18:41:22 INFO mapred.JobClient:  map 86% reduce 27%
17/03/16 18:41:23 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 18:41:24 INFO mapred.JobClient:  map 87% reduce 28%
17/03/16 18:41:25 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 18:41:26 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 18:41:28 INFO mapred.JobClient:  map 90% reduce 29%
17/03/16 18:41:31 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 18:41:32 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 18:41:33 INFO mapred.JobClient:  map 93% reduce 30%
17/03/16 18:41:34 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 18:41:35 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 18:41:37 INFO mapred.JobClient:  map 95% reduce 31%
17/03/16 18:41:38 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 18:41:40 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 18:41:41 INFO mapred.JobClient:  map 100% reduce 31%
17/03/16 18:41:43 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 18:41:46 INFO mapred.JobClient:  map 100% reduce 39%
17/03/16 18:41:49 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 18:41:52 INFO mapred.JobClient:  map 100% reduce 55%
17/03/16 18:41:53 INFO mapred.JobClient:  map 100% reduce 62%
17/03/16 18:41:55 INFO mapred.JobClient:  map 100% reduce 63%
17/03/16 18:41:56 INFO mapred.JobClient:  map 100% reduce 64%
17/03/16 18:41:58 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 18:41:58 INFO mapred.JobClient: Task Id : attempt_201703161829_0002_r_000000_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 18:42:01 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 18:42:02 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 18:42:04 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 18:42:07 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 18:42:08 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 18:42:10 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 18:42:11 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 18:42:14 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 18:42:17 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 18:42:20 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 18:42:23 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 18:42:26 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 18:42:28 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 18:42:29 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 18:42:31 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 18:42:32 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 18:42:35 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 18:42:41 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 18:42:56 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 18:43:02 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 18:43:09 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 18:43:15 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 18:43:21 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 18:43:24 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 18:43:26 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 18:43:35 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 18:43:42 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 18:43:42 INFO mapred.JobClient: Job complete: job_201703161829_0002
17/03/16 18:43:42 INFO mapred.JobClient: Counters: 30
17/03/16 18:43:42 INFO mapred.JobClient:   Job Counters
17/03/16 18:43:42 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 18:43:42 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=842303
17/03/16 18:43:42 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 18:43:42 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 18:43:42 INFO mapred.JobClient:     Launched map tasks=243
17/03/16 18:43:42 INFO mapred.JobClient:     Data-local map tasks=243
17/03/16 18:43:42 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1226732
17/03/16 18:43:42 INFO mapred.JobClient:   File Input Format Counters
17/03/16 18:43:42 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 18:43:42 INFO mapred.JobClient:   File Output Format Counters
17/03/16 18:43:42 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 18:43:42 INFO mapred.JobClient:   FileSystemCounters
17/03/16 18:43:42 INFO mapred.JobClient:     FILE_BYTES_READ=94263747685
17/03/16 18:43:42 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 18:43:42 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126523119244
17/03/16 18:43:42 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 18:43:42 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 18:43:42 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 18:43:42 INFO mapred.JobClient:     Map input records=3068055
17/03/16 18:43:42 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 18:43:42 INFO mapred.JobClient:     Spilled Records=12034372
17/03/16 18:43:42 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 18:43:42 INFO mapred.JobClient:     Total committed heap usage (bytes)=49355423744
17/03/16 18:43:42 INFO mapred.JobClient:     CPU time spent (ms)=1562810
17/03/16 18:43:42 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 18:43:42 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 18:43:42 INFO mapred.JobClient:     Combine input records=0
17/03/16 18:43:42 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 18:43:42 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 18:43:42 INFO mapred.JobClient:     Combine output records=0
17/03/16 18:43:42 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52982857728
17/03/16 18:43:42 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 18:43:42 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196229365760
17/03/16 18:43:42 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 18:43:42 UTC 2017
The job took 270 seconds.
```

## Normal with expiry interval of 30s and slowstart 0.05 (10GB)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 4 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 7 reduces.
Job started: Fri Mar 17 01:55:51 UTC 2017
17/03/17 01:55:51 INFO mapred.FileInputFormat: Total input paths to process : 40
17/03/17 01:55:52 INFO mapred.JobClient: Running job: job_201703170155_0001
17/03/17 01:55:53 INFO mapred.JobClient:  map 0% reduce 0%
17/03/17 01:55:59 INFO mapred.JobClient:  map 1% reduce 0%
17/03/17 01:56:00 INFO mapred.JobClient:  map 2% reduce 0%
17/03/17 01:56:03 INFO mapred.JobClient:  map 5% reduce 0%
17/03/17 01:56:06 INFO mapred.JobClient:  map 7% reduce 0%
17/03/17 01:56:09 INFO mapred.JobClient:  map 9% reduce 0%
17/03/17 01:56:13 INFO mapred.JobClient:  map 11% reduce 0%
17/03/17 01:56:14 INFO mapred.JobClient:  map 12% reduce 3%
17/03/17 01:56:17 INFO mapred.JobClient:  map 14% reduce 3%
17/03/17 01:56:20 INFO mapred.JobClient:  map 16% reduce 3%
17/03/17 01:56:21 INFO mapred.JobClient:  map 17% reduce 3%
17/03/17 01:56:23 INFO mapred.JobClient:  map 17% reduce 4%
17/03/17 01:56:24 INFO mapred.JobClient:  map 19% reduce 4%
17/03/17 01:56:26 INFO mapred.JobClient:  map 19% reduce 5%
17/03/17 01:56:27 INFO mapred.JobClient:  map 21% reduce 5%
17/03/17 01:56:28 INFO mapred.JobClient:  map 22% reduce 5%
17/03/17 01:56:29 INFO mapred.JobClient:  map 22% reduce 6%
17/03/17 01:56:30 INFO mapred.JobClient:  map 23% reduce 6%
17/03/17 01:56:31 INFO mapred.JobClient:  map 24% reduce 6%
17/03/17 01:56:32 INFO mapred.JobClient:  map 24% reduce 7%
17/03/17 01:56:34 INFO mapred.JobClient:  map 26% reduce 7%
17/03/17 01:56:35 INFO mapred.JobClient:  map 27% reduce 8%
17/03/17 01:56:37 INFO mapred.JobClient:  map 28% reduce 8%
17/03/17 01:56:38 INFO mapred.JobClient:  map 30% reduce 8%
17/03/17 01:56:41 INFO mapred.JobClient:  map 31% reduce 8%
17/03/17 01:56:42 INFO mapred.JobClient:  map 32% reduce 9%
17/03/17 01:56:45 INFO mapred.JobClient:  map 34% reduce 9%
17/03/17 01:56:47 INFO mapred.JobClient:  map 35% reduce 10%
17/03/17 01:56:48 INFO mapred.JobClient:  map 35% reduce 11%
17/03/17 01:56:49 INFO mapred.JobClient:  map 37% reduce 11%
17/03/17 01:56:52 INFO mapred.JobClient:  map 39% reduce 11%
17/03/17 01:56:54 INFO mapred.JobClient:  map 40% reduce 12%
17/03/17 01:56:56 INFO mapred.JobClient:  map 41% reduce 12%
17/03/17 01:56:57 INFO mapred.JobClient:  map 42% reduce 12%
17/03/17 01:56:59 INFO mapred.JobClient:  map 43% reduce 12%
17/03/17 01:57:00 INFO mapred.JobClient:  map 44% reduce 12%
17/03/17 01:57:01 INFO mapred.JobClient:  map 44% reduce 13%
17/03/17 01:57:02 INFO mapred.JobClient:  map 45% reduce 14%
17/03/17 01:57:04 INFO mapred.JobClient:  map 46% reduce 14%
17/03/17 01:57:05 INFO mapred.JobClient:  map 47% reduce 14%
17/03/17 01:57:06 INFO mapred.JobClient:  map 48% reduce 14%
17/03/17 01:57:07 INFO mapred.JobClient:  map 49% reduce 14%
17/03/17 01:57:08 INFO mapred.JobClient:  map 49% reduce 15%
17/03/17 01:57:09 INFO mapred.JobClient:  map 50% reduce 15%
17/03/17 01:57:11 INFO mapred.JobClient:  map 51% reduce 16%
17/03/17 01:57:12 INFO mapred.JobClient:  map 52% reduce 16%
17/03/17 01:57:14 INFO mapred.JobClient:  map 53% reduce 16%
17/03/17 01:57:15 INFO mapred.JobClient:  map 54% reduce 16%
17/03/17 01:57:16 INFO mapred.JobClient:  map 55% reduce 16%
17/03/17 01:57:17 INFO mapred.JobClient:  map 55% reduce 17%
17/03/17 01:57:18 INFO mapred.JobClient:  map 56% reduce 17%
17/03/17 01:57:19 INFO mapred.JobClient:  map 57% reduce 17%
17/03/17 01:57:21 INFO mapred.JobClient:  map 58% reduce 17%
17/03/17 01:57:22 INFO mapred.JobClient:  map 59% reduce 18%
17/03/17 01:57:23 INFO mapred.JobClient:  map 60% reduce 18%
17/03/17 01:57:26 INFO mapred.JobClient:  map 61% reduce 18%
17/03/17 01:57:27 INFO mapred.JobClient:  map 61% reduce 19%
17/03/17 01:57:28 INFO mapred.JobClient:  map 63% reduce 19%
17/03/17 01:57:29 INFO mapred.JobClient:  map 63% reduce 20%
17/03/17 01:57:30 INFO mapred.JobClient:  map 64% reduce 20%
17/03/17 01:57:33 INFO mapred.JobClient:  map 66% reduce 20%
17/03/17 01:57:36 INFO mapred.JobClient:  map 68% reduce 21%
17/03/17 01:57:37 INFO mapred.JobClient:  map 69% reduce 21%
17/03/17 01:57:39 INFO mapred.JobClient:  map 69% reduce 22%
17/03/17 01:57:40 INFO mapred.JobClient:  map 71% reduce 22%
17/03/17 01:57:43 INFO mapred.JobClient:  map 72% reduce 22%
17/03/17 01:57:44 INFO mapred.JobClient:  map 73% reduce 22%
17/03/17 01:57:45 INFO mapred.JobClient:  map 73% reduce 23%
17/03/17 01:57:46 INFO mapred.JobClient:  map 74% reduce 23%
17/03/17 01:57:47 INFO mapred.JobClient:  map 75% reduce 23%
17/03/17 01:57:48 INFO mapred.JobClient:  map 76% reduce 24%
17/03/17 01:57:51 INFO mapred.JobClient:  map 78% reduce 24%
17/03/17 01:57:53 INFO mapred.JobClient:  map 79% reduce 24%
17/03/17 01:57:54 INFO mapred.JobClient:  map 79% reduce 25%
17/03/17 01:57:55 INFO mapred.JobClient:  map 80% reduce 25%
17/03/17 01:57:56 INFO mapred.JobClient:  map 81% reduce 25%
17/03/17 01:57:59 INFO mapred.JobClient:  map 83% reduce 25%
17/03/17 01:58:00 INFO mapred.JobClient:  map 83% reduce 26%
17/03/17 01:58:01 INFO mapred.JobClient:  map 84% reduce 26%
17/03/17 01:58:02 INFO mapred.JobClient:  map 85% reduce 26%
17/03/17 01:58:03 INFO mapred.JobClient:  map 86% reduce 26%
17/03/17 01:58:04 INFO mapred.JobClient:  map 86% reduce 27%
17/03/17 01:58:06 INFO mapred.JobClient:  map 88% reduce 27%
17/03/17 01:58:08 INFO mapred.JobClient:  map 89% reduce 27%
17/03/17 01:58:09 INFO mapred.JobClient:  map 89% reduce 28%
17/03/17 01:58:10 INFO mapred.JobClient:  map 91% reduce 28%
17/03/17 01:58:12 INFO mapred.JobClient:  map 91% reduce 29%
17/03/17 01:58:13 INFO mapred.JobClient:  map 92% reduce 29%
17/03/17 01:58:14 INFO mapred.JobClient:  map 94% reduce 29%
17/03/17 01:58:17 INFO mapred.JobClient:  map 95% reduce 29%
17/03/17 01:58:18 INFO mapred.JobClient:  map 96% reduce 30%
17/03/17 01:58:20 INFO mapred.JobClient:  map 97% reduce 30%
17/03/17 01:58:21 INFO mapred.JobClient:  map 98% reduce 30%
17/03/17 01:58:22 INFO mapred.JobClient:  map 98% reduce 31%
17/03/17 01:58:23 INFO mapred.JobClient:  map 99% reduce 31%
17/03/17 01:58:24 INFO mapred.JobClient:  map 100% reduce 31%
17/03/17 01:58:25 INFO mapred.JobClient:  map 100% reduce 32%
17/03/17 01:58:30 INFO mapred.JobClient:  map 100% reduce 42%
17/03/17 01:58:31 INFO mapred.JobClient:  map 100% reduce 57%
17/03/17 01:58:33 INFO mapred.JobClient:  map 100% reduce 67%
17/03/17 01:58:34 INFO mapred.JobClient:  map 100% reduce 68%
17/03/17 01:58:36 INFO mapred.JobClient:  map 100% reduce 69%
17/03/17 01:58:39 INFO mapred.JobClient:  map 100% reduce 71%
17/03/17 01:58:42 INFO mapred.JobClient:  map 100% reduce 72%
17/03/17 01:58:43 INFO mapred.JobClient:  map 100% reduce 73%
17/03/17 01:58:45 INFO mapred.JobClient:  map 100% reduce 74%
17/03/17 01:58:48 INFO mapred.JobClient:  map 100% reduce 75%
17/03/17 01:58:49 INFO mapred.JobClient:  map 100% reduce 76%
17/03/17 01:58:52 INFO mapred.JobClient:  map 100% reduce 77%
17/03/17 01:58:55 INFO mapred.JobClient:  map 100% reduce 78%
17/03/17 01:58:57 INFO mapred.JobClient:  map 100% reduce 79%
17/03/17 01:58:58 INFO mapred.JobClient:  map 100% reduce 80%
17/03/17 01:59:00 INFO mapred.JobClient:  map 100% reduce 81%
17/03/17 01:59:03 INFO mapred.JobClient:  map 100% reduce 82%
17/03/17 01:59:04 INFO mapred.JobClient:  map 100% reduce 83%
17/03/17 01:59:07 INFO mapred.JobClient:  map 100% reduce 84%
17/03/17 01:59:09 INFO mapred.JobClient:  map 100% reduce 85%
17/03/17 01:59:12 INFO mapred.JobClient:  map 100% reduce 86%
17/03/17 01:59:13 INFO mapred.JobClient:  map 100% reduce 87%
17/03/17 01:59:19 INFO mapred.JobClient:  map 100% reduce 88%
17/03/17 01:59:28 INFO mapred.JobClient:  map 100% reduce 89%
17/03/17 01:59:34 INFO mapred.JobClient:  map 100% reduce 90%
17/03/17 01:59:39 INFO mapred.JobClient:  map 100% reduce 91%
17/03/17 01:59:43 INFO mapred.JobClient:  map 100% reduce 92%
17/03/17 01:59:49 INFO mapred.JobClient:  map 100% reduce 93%
17/03/17 01:59:58 INFO mapred.JobClient:  map 100% reduce 94%
17/03/17 02:00:04 INFO mapred.JobClient:  map 100% reduce 95%
17/03/17 02:00:11 INFO mapred.JobClient:  map 100% reduce 96%
17/03/17 02:00:18 INFO mapred.JobClient:  map 100% reduce 97%
17/03/17 02:00:30 INFO mapred.JobClient:  map 100% reduce 98%
17/03/17 02:00:40 INFO mapred.JobClient:  map 100% reduce 99%
17/03/17 02:00:46 INFO mapred.JobClient:  map 100% reduce 100%
17/03/17 02:00:46 INFO mapred.JobClient: Job complete: job_201703170155_0001
17/03/17 02:00:46 INFO mapred.JobClient: Counters: 31
17/03/17 02:00:46 INFO mapred.JobClient:   Job Counters
17/03/17 02:00:46 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/17 02:00:46 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=1128812
17/03/17 02:00:46 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/17 02:00:46 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/17 02:00:46 INFO mapred.JobClient:     Rack-local map tasks=1
17/03/17 02:00:46 INFO mapred.JobClient:     Launched map tasks=325
17/03/17 02:00:46 INFO mapred.JobClient:     Data-local map tasks=324
17/03/17 02:00:46 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1895724
17/03/17 02:00:46 INFO mapred.JobClient:   File Input Format Counters
17/03/17 02:00:46 INFO mapred.JobClient:     Bytes Read=43093428969
17/03/17 02:00:46 INFO mapred.JobClient:   File Output Format Counters
17/03/17 02:00:46 INFO mapred.JobClient:     Bytes Written=43091440103
17/03/17 02:00:46 INFO mapred.JobClient:   FileSystemCounters
17/03/17 02:00:46 INFO mapred.JobClient:     FILE_BYTES_READ=126519056927
17/03/17 02:00:46 INFO mapred.JobClient:     HDFS_BYTES_READ=43096366836
17/03/17 02:00:46 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=169526720229
17/03/17 02:00:46 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=43091440103
17/03/17 02:00:46 INFO mapred.JobClient:   Map-Reduce Framework
17/03/17 02:00:46 INFO mapred.JobClient:     Map output materialized bytes=43005669301
17/03/17 02:00:46 INFO mapred.JobClient:     Map input records=4089642
17/03/17 02:00:46 INFO mapred.JobClient:     Reduce shuffle bytes=43005669301
17/03/17 02:00:46 INFO mapred.JobClient:     Spilled Records=16119489
17/03/17 02:00:46 INFO mapred.JobClient:     Map output bytes=42982666575
17/03/17 02:00:46 INFO mapred.JobClient:     Total committed heap usage (bytes)=65844281344
17/03/17 02:00:46 INFO mapred.JobClient:     CPU time spent (ms)=2296190
17/03/17 02:00:46 INFO mapred.JobClient:     Map input bytes=43091438491
17/03/17 02:00:46 INFO mapred.JobClient:     SPLIT_RAW_BYTES=39680
17/03/17 02:00:46 INFO mapred.JobClient:     Combine input records=0
17/03/17 02:00:46 INFO mapred.JobClient:     Reduce input records=4089642
17/03/17 02:00:46 INFO mapred.JobClient:     Reduce input groups=4089642
17/03/17 02:00:46 INFO mapred.JobClient:     Combine output records=0
17/03/17 02:00:46 INFO mapred.JobClient:     Physical memory (bytes) snapshot=70710378496
17/03/17 02:00:46 INFO mapred.JobClient:     Reduce output records=4089642
17/03/17 02:00:46 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=262201307136
17/03/17 02:00:46 INFO mapred.JobClient:     Map output records=4089642
Job ended: Fri Mar 17 02:00:46 UTC 2017
The job took 295 seconds.
```

## Normal with expiry interval of 30s and slowstart 0.5 (10GB)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 4 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 7 reduces.
Job started: Fri Mar 17 01:37:45 UTC 2017
17/03/17 01:37:45 INFO mapred.FileInputFormat: Total input paths to process : 40
17/03/17 01:37:46 INFO mapred.JobClient: Running job: job_201703170136_0001
17/03/17 01:37:47 INFO mapred.JobClient:  map 0% reduce 0%
17/03/17 01:37:54 INFO mapred.JobClient:  map 2% reduce 0%
17/03/17 01:37:57 INFO mapred.JobClient:  map 5% reduce 0%
17/03/17 01:38:00 INFO mapred.JobClient:  map 6% reduce 0%
17/03/17 01:38:01 INFO mapred.JobClient:  map 7% reduce 0%
17/03/17 01:38:04 INFO mapred.JobClient:  map 9% reduce 0%
17/03/17 01:38:07 INFO mapred.JobClient:  map 12% reduce 0%
17/03/17 01:38:10 INFO mapred.JobClient:  map 14% reduce 0%
17/03/17 01:38:13 INFO mapred.JobClient:  map 15% reduce 0%
17/03/17 01:38:14 INFO mapred.JobClient:  map 17% reduce 0%
17/03/17 01:38:17 INFO mapred.JobClient:  map 19% reduce 0%
17/03/17 01:38:20 INFO mapred.JobClient:  map 21% reduce 0%
17/03/17 01:38:21 INFO mapred.JobClient:  map 22% reduce 0%
17/03/17 01:38:23 INFO mapred.JobClient:  map 23% reduce 0%
17/03/17 01:38:24 INFO mapred.JobClient:  map 24% reduce 0%
17/03/17 01:38:27 INFO mapred.JobClient:  map 27% reduce 0%
17/03/17 01:38:30 INFO mapred.JobClient:  map 28% reduce 0%
17/03/17 01:38:31 INFO mapred.JobClient:  map 30% reduce 0%
17/03/17 01:38:34 INFO mapred.JobClient:  map 32% reduce 0%
17/03/17 01:38:37 INFO mapred.JobClient:  map 35% reduce 0%
17/03/17 01:38:41 INFO mapred.JobClient:  map 37% reduce 0%
17/03/17 01:38:44 INFO mapred.JobClient:  map 40% reduce 0%
17/03/17 01:38:48 INFO mapred.JobClient:  map 42% reduce 0%
17/03/17 01:38:51 INFO mapred.JobClient:  map 44% reduce 0%
17/03/17 01:38:52 INFO mapred.JobClient:  map 45% reduce 0%
17/03/17 01:38:55 INFO mapred.JobClient:  map 46% reduce 0%
17/03/17 01:38:56 INFO mapred.JobClient:  map 47% reduce 0%
17/03/17 01:38:58 INFO mapred.JobClient:  map 48% reduce 0%
17/03/17 01:38:59 INFO mapred.JobClient:  map 49% reduce 0%
17/03/17 01:39:00 INFO mapred.JobClient:  map 50% reduce 0%
17/03/17 01:39:02 INFO mapred.JobClient:  map 51% reduce 0%
17/03/17 01:39:04 INFO mapred.JobClient:  map 53% reduce 0%
17/03/17 01:39:06 INFO mapred.JobClient:  map 54% reduce 0%
17/03/17 01:39:07 INFO mapred.JobClient:  map 55% reduce 0%
17/03/17 01:39:09 INFO mapred.JobClient:  map 56% reduce 0%
17/03/17 01:39:10 INFO mapred.JobClient:  map 56% reduce 1%
17/03/17 01:39:11 INFO mapred.JobClient:  map 56% reduce 3%
17/03/17 01:39:12 INFO mapred.JobClient:  map 58% reduce 3%
17/03/17 01:39:13 INFO mapred.JobClient:  map 58% reduce 4%
17/03/17 01:39:14 INFO mapred.JobClient:  map 59% reduce 5%
17/03/17 01:39:16 INFO mapred.JobClient:  map 60% reduce 5%
17/03/17 01:39:17 INFO mapred.JobClient:  map 61% reduce 7%
17/03/17 01:39:17 INFO mapred.JobClient: Task Id : attempt_201703170136_0001_r_000000_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at sun.net.www.http.ChunkedInputStream.processRaw(ChunkedInputStream.java:363)
        at sun.net.www.http.ChunkedInputStream.readAheadNonBlocking(ChunkedInputStream.java:520)
        at sun.net.www.http.ChunkedInputStream.readAhead(ChunkedInputStream.java:611)
        at sun.net.www.http.ChunkedInputStream.hurry(ChunkedInputStream.java:768)
        at sun.net.www.http.ChunkedInputStream.closeUnderlying(ChunkedInputStream.java:221)
        at sun.net.www.http.ChunkedInputStream.close(ChunkedInputStream.java:749)
        at java.io.FilterInputStream.close(FilterInputStream.java:181)
        at sun.net.www.protocol.http.HttpURLConnection$HttpInputStream.close(HttpURLConnection.java:3137)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$ShuffleRamManager.reserve(ReduceTask.java:1132)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1671)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/17 01:39:20 INFO mapred.JobClient:  map 62% reduce 9%
17/03/17 01:39:21 INFO mapred.JobClient:  map 63% reduce 10%
17/03/17 01:39:22 INFO mapred.JobClient:  map 64% reduce 10%
17/03/17 01:39:23 INFO mapred.JobClient:  map 64% reduce 12%
17/03/17 01:39:25 INFO mapred.JobClient:  map 66% reduce 12%
17/03/17 01:39:26 INFO mapred.JobClient:  map 66% reduce 14%
17/03/17 01:39:27 INFO mapred.JobClient:  map 66% reduce 15%
17/03/17 01:39:28 INFO mapred.JobClient:  map 67% reduce 15%
17/03/17 01:39:29 INFO mapred.JobClient:  map 68% reduce 16%
17/03/17 01:39:30 INFO mapred.JobClient:  map 68% reduce 18%
17/03/17 01:39:31 INFO mapred.JobClient:  map 69% reduce 18%
17/03/17 01:39:33 INFO mapred.JobClient:  map 70% reduce 19%
17/03/17 01:39:34 INFO mapred.JobClient:  map 71% reduce 19%
17/03/17 01:39:35 INFO mapred.JobClient:  map 71% reduce 20%
17/03/17 01:39:36 INFO mapred.JobClient:  map 72% reduce 20%
17/03/17 01:39:37 INFO mapred.JobClient:  map 73% reduce 21%
17/03/17 01:39:38 INFO mapred.JobClient:  map 74% reduce 21%
17/03/17 01:39:40 INFO mapred.JobClient:  map 75% reduce 22%
17/03/17 01:39:42 INFO mapred.JobClient:  map 76% reduce 22%
17/03/17 01:39:43 INFO mapred.JobClient:  map 76% reduce 23%
17/03/17 01:39:44 INFO mapred.JobClient:  map 77% reduce 23%
17/03/17 01:39:46 INFO mapred.JobClient:  map 79% reduce 24%
17/03/17 01:39:47 INFO mapred.JobClient:  map 80% reduce 24%
17/03/17 01:39:49 INFO mapred.JobClient:  map 80% reduce 25%
17/03/17 01:39:50 INFO mapred.JobClient:  map 81% reduce 25%
17/03/17 01:39:51 INFO mapred.JobClient:  map 82% reduce 25%
17/03/17 01:39:52 INFO mapred.JobClient:  map 83% reduce 26%
17/03/17 01:39:55 INFO mapred.JobClient:  map 85% reduce 26%
17/03/17 01:39:56 INFO mapred.JobClient:  map 85% reduce 27%
17/03/17 01:39:57 INFO mapred.JobClient:  map 86% reduce 27%
17/03/17 01:39:59 INFO mapred.JobClient:  map 87% reduce 28%
17/03/17 01:40:00 INFO mapred.JobClient:  map 88% reduce 28%
17/03/17 01:40:02 INFO mapred.JobClient:  map 89% reduce 28%
17/03/17 01:40:03 INFO mapred.JobClient:  map 90% reduce 28%
17/03/17 01:40:05 INFO mapred.JobClient:  map 91% reduce 29%
17/03/17 01:40:06 INFO mapred.JobClient:  map 92% reduce 29%
17/03/17 01:40:08 INFO mapred.JobClient:  map 93% reduce 29%
17/03/17 01:40:10 INFO mapred.JobClient:  map 95% reduce 30%
17/03/17 01:40:13 INFO mapred.JobClient:  map 96% reduce 30%
17/03/17 01:40:14 INFO mapred.JobClient:  map 97% reduce 30%
17/03/17 01:40:15 INFO mapred.JobClient:  map 98% reduce 30%
17/03/17 01:40:16 INFO mapred.JobClient:  map 98% reduce 31%
17/03/17 01:40:17 INFO mapred.JobClient:  map 99% reduce 31%
17/03/17 01:40:19 INFO mapred.JobClient:  map 100% reduce 32%
17/03/17 01:40:23 INFO mapred.JobClient:  map 100% reduce 37%
17/03/17 01:40:24 INFO mapred.JobClient:  map 100% reduce 42%
17/03/17 01:40:25 INFO mapred.JobClient:  map 100% reduce 52%
17/03/17 01:40:26 INFO mapred.JobClient:  map 100% reduce 62%
17/03/17 01:40:28 INFO mapred.JobClient:  map 100% reduce 67%
17/03/17 01:40:29 INFO mapred.JobClient:  map 100% reduce 68%
17/03/17 01:40:31 INFO mapred.JobClient:  map 100% reduce 69%
17/03/17 01:40:32 INFO mapred.JobClient:  map 100% reduce 70%
17/03/17 01:40:35 INFO mapred.JobClient:  map 100% reduce 71%
17/03/17 01:40:37 INFO mapred.JobClient:  map 100% reduce 72%
17/03/17 01:40:38 INFO mapred.JobClient:  map 100% reduce 73%
17/03/17 01:40:40 INFO mapred.JobClient:  map 100% reduce 74%
17/03/17 01:40:42 INFO mapred.JobClient:  map 100% reduce 75%
17/03/17 01:40:44 INFO mapred.JobClient:  map 100% reduce 76%
17/03/17 01:40:47 INFO mapred.JobClient:  map 100% reduce 77%
17/03/17 01:40:49 INFO mapred.JobClient:  map 100% reduce 78%
17/03/17 01:40:50 INFO mapred.JobClient:  map 100% reduce 79%
17/03/17 01:40:52 INFO mapred.JobClient:  map 100% reduce 80%
17/03/17 01:40:54 INFO mapred.JobClient:  map 100% reduce 81%
17/03/17 01:40:57 INFO mapred.JobClient:  map 100% reduce 82%
17/03/17 01:41:01 INFO mapred.JobClient:  map 100% reduce 83%
17/03/17 01:41:07 INFO mapred.JobClient:  map 100% reduce 84%
17/03/17 01:41:13 INFO mapred.JobClient:  map 100% reduce 85%
17/03/17 01:41:18 INFO mapred.JobClient:  map 100% reduce 86%
17/03/17 01:41:24 INFO mapred.JobClient:  map 100% reduce 87%
17/03/17 01:41:32 INFO mapred.JobClient:  map 100% reduce 88%
17/03/17 01:41:38 INFO mapred.JobClient:  map 100% reduce 89%
17/03/17 01:41:43 INFO mapred.JobClient:  map 100% reduce 90%
17/03/17 01:41:48 INFO mapred.JobClient:  map 100% reduce 91%
17/03/17 01:41:54 INFO mapred.JobClient:  map 100% reduce 92%
17/03/17 01:42:02 INFO mapred.JobClient:  map 100% reduce 93%
17/03/17 01:42:08 INFO mapred.JobClient:  map 100% reduce 94%
17/03/17 01:42:14 INFO mapred.JobClient:  map 100% reduce 95%
17/03/17 01:42:20 INFO mapred.JobClient:  map 100% reduce 96%
17/03/17 01:42:29 INFO mapred.JobClient:  map 100% reduce 97%
17/03/17 01:42:35 INFO mapred.JobClient:  map 100% reduce 98%
17/03/17 01:42:41 INFO mapred.JobClient:  map 100% reduce 99%
17/03/17 01:42:55 INFO mapred.JobClient:  map 100% reduce 100%
17/03/17 01:42:56 INFO mapred.JobClient: Job complete: job_201703170136_0001
17/03/17 01:42:56 INFO mapred.JobClient: Counters: 31
17/03/17 01:42:56 INFO mapred.JobClient:   Job Counters
17/03/17 01:42:56 INFO mapred.JobClient:     Launched reduce tasks=9
17/03/17 01:42:56 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=1122926
17/03/17 01:42:56 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/17 01:42:56 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/17 01:42:56 INFO mapred.JobClient:     Rack-local map tasks=1
17/03/17 01:42:56 INFO mapred.JobClient:     Launched map tasks=324
17/03/17 01:42:56 INFO mapred.JobClient:     Data-local map tasks=323
17/03/17 01:42:56 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1557039
17/03/17 01:42:56 INFO mapred.JobClient:   File Input Format Counters
17/03/17 01:42:56 INFO mapred.JobClient:     Bytes Read=43093428969
17/03/17 01:42:56 INFO mapred.JobClient:   File Output Format Counters
17/03/17 01:42:56 INFO mapred.JobClient:     Bytes Written=43091440103
17/03/17 01:42:56 INFO mapred.JobClient:   FileSystemCounters
17/03/17 01:42:56 INFO mapred.JobClient:     FILE_BYTES_READ=126385448599
17/03/17 01:42:56 INFO mapred.JobClient:     HDFS_BYTES_READ=43096366836
17/03/17 01:42:56 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=169393111574
17/03/17 01:42:56 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=43091440103
17/03/17 01:42:56 INFO mapred.JobClient:   Map-Reduce Framework
17/03/17 01:42:56 INFO mapred.JobClient:     Map output materialized bytes=43005669301
17/03/17 01:42:56 INFO mapred.JobClient:     Map input records=4089642
17/03/17 01:42:56 INFO mapred.JobClient:     Reduce shuffle bytes=43005669301
17/03/17 01:42:56 INFO mapred.JobClient:     Spilled Records=16106948
17/03/17 01:42:56 INFO mapred.JobClient:     Map output bytes=42982666575
17/03/17 01:42:56 INFO mapred.JobClient:     Total committed heap usage (bytes)=65873117184
17/03/17 01:42:56 INFO mapred.JobClient:     CPU time spent (ms)=2367970
17/03/17 01:42:56 INFO mapred.JobClient:     Map input bytes=43091438491
17/03/17 01:42:56 INFO mapred.JobClient:     SPLIT_RAW_BYTES=39680
17/03/17 01:42:56 INFO mapred.JobClient:     Combine input records=0
17/03/17 01:42:56 INFO mapred.JobClient:     Reduce input records=4089642
17/03/17 01:42:56 INFO mapred.JobClient:     Reduce input groups=4089642
17/03/17 01:42:56 INFO mapred.JobClient:     Combine output records=0
17/03/17 01:42:56 INFO mapred.JobClient:     Physical memory (bytes) snapshot=70637813760
17/03/17 01:42:56 INFO mapred.JobClient:     Reduce output records=4089642
17/03/17 01:42:56 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=261951856640
17/03/17 01:42:56 INFO mapred.JobClient:     Map output records=4089642
Job ended: Fri Mar 17 01:42:56 UTC 2017
The job took 311 seconds.
```

## Normal with expiry interval of 30s and slowstart 1 (10GB)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 4 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 7 reduces.
Job started: Fri Mar 17 01:45:02 UTC 2017
17/03/17 01:45:02 INFO mapred.FileInputFormat: Total input paths to process : 40
17/03/17 01:45:02 INFO mapred.JobClient: Running job: job_201703170144_0001
17/03/17 01:45:03 INFO mapred.JobClient:  map 0% reduce 0%
17/03/17 01:45:10 INFO mapred.JobClient:  map 2% reduce 0%
17/03/17 01:45:13 INFO mapred.JobClient:  map 5% reduce 0%
17/03/17 01:45:16 INFO mapred.JobClient:  map 6% reduce 0%
17/03/17 01:45:17 INFO mapred.JobClient:  map 7% reduce 0%
17/03/17 01:45:20 INFO mapred.JobClient:  map 9% reduce 0%
17/03/17 01:45:22 INFO mapred.JobClient:  map 10% reduce 0%
17/03/17 01:45:23 INFO mapred.JobClient:  map 12% reduce 0%
17/03/17 01:45:26 INFO mapred.JobClient:  map 13% reduce 0%
17/03/17 01:45:27 INFO mapred.JobClient:  map 14% reduce 0%
17/03/17 01:45:29 INFO mapred.JobClient:  map 15% reduce 0%
17/03/17 01:45:30 INFO mapred.JobClient:  map 17% reduce 0%
17/03/17 01:45:33 INFO mapred.JobClient:  map 19% reduce 0%
17/03/17 01:45:36 INFO mapred.JobClient:  map 21% reduce 0%
17/03/17 01:45:37 INFO mapred.JobClient:  map 22% reduce 0%
17/03/17 01:45:39 INFO mapred.JobClient:  map 23% reduce 0%
17/03/17 01:45:40 INFO mapred.JobClient:  map 24% reduce 0%
17/03/17 01:45:42 INFO mapred.JobClient:  map 25% reduce 0%
17/03/17 01:45:43 INFO mapred.JobClient:  map 27% reduce 0%
17/03/17 01:45:46 INFO mapred.JobClient:  map 28% reduce 0%
17/03/17 01:45:47 INFO mapred.JobClient:  map 30% reduce 0%
17/03/17 01:45:50 INFO mapred.JobClient:  map 32% reduce 0%
17/03/17 01:45:53 INFO mapred.JobClient:  map 33% reduce 0%
17/03/17 01:45:54 INFO mapred.JobClient:  map 35% reduce 0%
17/03/17 01:45:57 INFO mapred.JobClient:  map 36% reduce 0%
17/03/17 01:45:58 INFO mapred.JobClient:  map 37% reduce 0%
17/03/17 01:46:00 INFO mapred.JobClient:  map 38% reduce 0%
17/03/17 01:46:01 INFO mapred.JobClient:  map 39% reduce 0%
17/03/17 01:46:02 INFO mapred.JobClient:  map 40% reduce 0%
17/03/17 01:46:04 INFO mapred.JobClient:  map 41% reduce 0%
17/03/17 01:46:05 INFO mapred.JobClient:  map 42% reduce 0%
17/03/17 01:46:08 INFO mapred.JobClient:  map 43% reduce 0%
17/03/17 01:46:09 INFO mapred.JobClient:  map 44% reduce 0%
17/03/17 01:46:10 INFO mapred.JobClient:  map 45% reduce 0%
17/03/17 01:46:12 INFO mapred.JobClient:  map 46% reduce 0%
17/03/17 01:46:13 INFO mapred.JobClient:  map 47% reduce 0%
17/03/17 01:46:14 INFO mapred.JobClient:  map 48% reduce 0%
17/03/17 01:46:16 INFO mapred.JobClient:  map 49% reduce 0%
17/03/17 01:46:17 INFO mapred.JobClient:  map 50% reduce 0%
17/03/17 01:46:19 INFO mapred.JobClient:  map 51% reduce 0%
17/03/17 01:46:20 INFO mapred.JobClient:  map 52% reduce 0%
17/03/17 01:46:22 INFO mapred.JobClient:  map 54% reduce 0%
17/03/17 01:46:24 INFO mapred.JobClient:  map 55% reduce 0%
17/03/17 01:46:26 INFO mapred.JobClient:  map 57% reduce 0%
17/03/17 01:46:29 INFO mapred.JobClient:  map 59% reduce 0%
17/03/17 01:46:31 INFO mapred.JobClient:  map 60% reduce 0%
17/03/17 01:46:32 INFO mapred.JobClient:  map 61% reduce 0%
17/03/17 01:46:33 INFO mapred.JobClient:  map 62% reduce 0%
17/03/17 01:46:35 INFO mapred.JobClient:  map 63% reduce 0%
17/03/17 01:46:36 INFO mapred.JobClient:  map 64% reduce 0%
17/03/17 01:46:38 INFO mapred.JobClient:  map 65% reduce 0%
17/03/17 01:46:39 INFO mapred.JobClient:  map 66% reduce 0%
17/03/17 01:46:40 INFO mapred.JobClient:  map 67% reduce 0%
17/03/17 01:46:43 INFO mapred.JobClient:  map 69% reduce 0%
17/03/17 01:46:45 INFO mapred.JobClient:  map 70% reduce 0%
17/03/17 01:46:46 INFO mapred.JobClient:  map 71% reduce 0%
17/03/17 01:46:47 INFO mapred.JobClient:  map 72% reduce 0%
17/03/17 01:46:49 INFO mapred.JobClient:  map 73% reduce 0%
17/03/17 01:46:50 INFO mapred.JobClient:  map 74% reduce 0%
17/03/17 01:46:52 INFO mapred.JobClient:  map 75% reduce 0%
17/03/17 01:46:53 INFO mapred.JobClient:  map 76% reduce 0%
17/03/17 01:46:54 INFO mapred.JobClient:  map 77% reduce 0%
17/03/17 01:46:56 INFO mapred.JobClient:  map 78% reduce 0%
17/03/17 01:46:57 INFO mapred.JobClient:  map 79% reduce 0%
17/03/17 01:46:59 INFO mapred.JobClient:  map 80% reduce 0%
17/03/17 01:47:00 INFO mapred.JobClient:  map 81% reduce 0%
17/03/17 01:47:01 INFO mapred.JobClient:  map 82% reduce 0%
17/03/17 01:47:03 INFO mapred.JobClient:  map 83% reduce 0%
17/03/17 01:47:04 INFO mapred.JobClient:  map 84% reduce 0%
17/03/17 01:47:06 INFO mapred.JobClient:  map 85% reduce 0%
17/03/17 01:47:07 INFO mapred.JobClient:  map 87% reduce 0%
17/03/17 01:47:10 INFO mapred.JobClient:  map 88% reduce 0%
17/03/17 01:47:11 INFO mapred.JobClient:  map 89% reduce 0%
17/03/17 01:47:13 INFO mapred.JobClient:  map 90% reduce 0%
17/03/17 01:47:14 INFO mapred.JobClient:  map 91% reduce 0%
17/03/17 01:47:15 INFO mapred.JobClient:  map 92% reduce 0%
17/03/17 01:47:17 INFO mapred.JobClient:  map 94% reduce 0%
17/03/17 01:47:20 INFO mapred.JobClient:  map 95% reduce 0%
17/03/17 01:47:21 INFO mapred.JobClient:  map 96% reduce 0%
17/03/17 01:47:22 INFO mapred.JobClient:  map 97% reduce 0%
17/03/17 01:47:23 INFO mapred.JobClient:  map 98% reduce 0%
17/03/17 01:47:24 INFO mapred.JobClient:  map 99% reduce 0%
17/03/17 01:47:27 INFO mapred.JobClient:  map 100% reduce 0%
17/03/17 01:47:37 INFO mapred.JobClient:  map 100% reduce 2%
17/03/17 01:47:38 INFO mapred.JobClient:  map 100% reduce 3%
17/03/17 01:47:40 INFO mapred.JobClient:  map 100% reduce 5%
17/03/17 01:47:43 INFO mapred.JobClient:  map 100% reduce 8%
17/03/17 01:47:46 INFO mapred.JobClient:  map 100% reduce 9%
17/03/17 01:47:47 INFO mapred.JobClient:  map 100% reduce 10%
17/03/17 01:47:49 INFO mapred.JobClient:  map 100% reduce 11%
17/03/17 01:47:50 INFO mapred.JobClient:  map 100% reduce 12%
17/03/17 01:47:52 INFO mapred.JobClient:  map 100% reduce 14%
17/03/17 01:47:53 INFO mapred.JobClient:  map 100% reduce 15%
17/03/17 01:47:54 INFO mapred.JobClient:  map 100% reduce 16%
17/03/17 01:47:56 INFO mapred.JobClient:  map 100% reduce 18%
17/03/17 01:47:57 INFO mapred.JobClient:  map 100% reduce 19%
17/03/17 01:47:59 INFO mapred.JobClient:  map 100% reduce 20%
17/03/17 01:48:00 INFO mapred.JobClient:  map 100% reduce 21%
17/03/17 01:48:02 INFO mapred.JobClient:  map 100% reduce 23%
17/03/17 01:48:03 INFO mapred.JobClient:  map 100% reduce 24%
17/03/17 01:48:05 INFO mapred.JobClient:  map 100% reduce 26%
17/03/17 01:48:06 INFO mapred.JobClient:  map 100% reduce 27%
17/03/17 01:48:08 INFO mapred.JobClient:  map 100% reduce 29%
17/03/17 01:48:09 INFO mapred.JobClient:  map 100% reduce 30%
17/03/17 01:48:11 INFO mapred.JobClient:  map 100% reduce 31%
17/03/17 01:48:14 INFO mapred.JobClient:  map 100% reduce 37%
17/03/17 01:48:15 INFO mapred.JobClient:  map 100% reduce 42%
17/03/17 01:48:17 INFO mapred.JobClient:  map 100% reduce 57%
17/03/17 01:48:20 INFO mapred.JobClient:  map 100% reduce 63%
17/03/17 01:48:26 INFO mapred.JobClient:  map 100% reduce 68%
17/03/17 01:48:27 INFO mapred.JobClient:  map 100% reduce 69%
17/03/17 01:48:29 INFO mapred.JobClient:  map 100% reduce 70%
17/03/17 01:48:32 INFO mapred.JobClient:  map 100% reduce 71%
17/03/17 01:48:33 INFO mapred.JobClient:  map 100% reduce 72%
17/03/17 01:48:36 INFO mapred.JobClient:  map 100% reduce 73%
17/03/17 01:48:39 INFO mapred.JobClient:  map 100% reduce 74%
17/03/17 01:48:42 INFO mapred.JobClient:  map 100% reduce 75%
17/03/17 01:48:44 INFO mapred.JobClient:  map 100% reduce 76%
17/03/17 01:48:47 INFO mapred.JobClient:  map 100% reduce 77%
17/03/17 01:48:48 INFO mapred.JobClient:  map 100% reduce 78%
17/03/17 01:48:50 INFO mapred.JobClient:  map 100% reduce 79%
17/03/17 01:48:54 INFO mapred.JobClient:  map 100% reduce 81%
17/03/17 01:48:57 INFO mapred.JobClient:  map 100% reduce 82%
17/03/17 01:49:00 INFO mapred.JobClient:  map 100% reduce 83%
17/03/17 01:49:03 INFO mapred.JobClient:  map 100% reduce 84%
17/03/17 01:49:08 INFO mapred.JobClient:  map 100% reduce 85%
17/03/17 01:49:14 INFO mapred.JobClient:  map 100% reduce 86%
17/03/17 01:49:18 INFO mapred.JobClient:  map 100% reduce 87%
17/03/17 01:49:23 INFO mapred.JobClient:  map 100% reduce 88%
17/03/17 01:49:30 INFO mapred.JobClient:  map 100% reduce 89%
17/03/17 01:49:37 INFO mapred.JobClient:  map 100% reduce 90%
17/03/17 01:49:44 INFO mapred.JobClient:  map 100% reduce 91%
17/03/17 01:49:52 INFO mapred.JobClient:  map 100% reduce 92%
17/03/17 01:49:59 INFO mapred.JobClient:  map 100% reduce 93%
17/03/17 01:50:07 INFO mapred.JobClient:  map 100% reduce 94%
17/03/17 01:50:13 INFO mapred.JobClient:  map 100% reduce 95%
17/03/17 01:50:19 INFO mapred.JobClient:  map 100% reduce 96%
17/03/17 01:50:25 INFO mapred.JobClient:  map 100% reduce 97%
17/03/17 01:50:33 INFO mapred.JobClient:  map 100% reduce 98%
17/03/17 01:50:40 INFO mapred.JobClient:  map 100% reduce 99%
17/03/17 01:50:45 INFO mapred.JobClient:  map 100% reduce 100%
17/03/17 01:50:46 INFO mapred.JobClient: Job complete: job_201703170144_0001
17/03/17 01:50:46 INFO mapred.JobClient: Counters: 31
17/03/17 01:50:46 INFO mapred.JobClient:   Job Counters
17/03/17 01:50:46 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/17 01:50:46 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=1049364
17/03/17 01:50:46 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/17 01:50:46 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/17 01:50:46 INFO mapred.JobClient:     Rack-local map tasks=1
17/03/17 01:50:46 INFO mapred.JobClient:     Launched map tasks=324
17/03/17 01:50:46 INFO mapred.JobClient:     Data-local map tasks=323
17/03/17 01:50:46 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1345303
17/03/17 01:50:46 INFO mapred.JobClient:   File Input Format Counters
17/03/17 01:50:46 INFO mapred.JobClient:     Bytes Read=43093428969
17/03/17 01:50:46 INFO mapred.JobClient:   File Output Format Counters
17/03/17 01:50:46 INFO mapred.JobClient:     Bytes Written=43091440103
17/03/17 01:50:46 INFO mapred.JobClient:   FileSystemCounters
17/03/17 01:50:46 INFO mapred.JobClient:     FILE_BYTES_READ=126585121939
17/03/17 01:50:46 INFO mapred.JobClient:     HDFS_BYTES_READ=43096366836
17/03/17 01:50:46 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=169592784260
17/03/17 01:50:46 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=43091440103
17/03/17 01:50:46 INFO mapred.JobClient:   Map-Reduce Framework
17/03/17 01:50:46 INFO mapred.JobClient:     Map output materialized bytes=43005669301
17/03/17 01:50:46 INFO mapred.JobClient:     Map input records=4089642
17/03/17 01:50:46 INFO mapred.JobClient:     Reduce shuffle bytes=43005669301
17/03/17 01:50:46 INFO mapred.JobClient:     Spilled Records=16126173
17/03/17 01:50:46 INFO mapred.JobClient:     Map output bytes=42982666575
17/03/17 01:50:46 INFO mapred.JobClient:     Total committed heap usage (bytes)=65743618048
17/03/17 01:50:46 INFO mapred.JobClient:     CPU time spent (ms)=2420440
17/03/17 01:50:46 INFO mapred.JobClient:     Map input bytes=43091438491
17/03/17 01:50:46 INFO mapred.JobClient:     SPLIT_RAW_BYTES=39680
17/03/17 01:50:46 INFO mapred.JobClient:     Combine input records=0
17/03/17 01:50:46 INFO mapred.JobClient:     Reduce input records=4089642
17/03/17 01:50:46 INFO mapred.JobClient:     Reduce input groups=4089642
17/03/17 01:50:46 INFO mapred.JobClient:     Combine output records=0
17/03/17 01:50:46 INFO mapred.JobClient:     Physical memory (bytes) snapshot=70570450944
17/03/17 01:50:46 INFO mapred.JobClient:     Reduce output records=4089642
17/03/17 01:50:46 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=262892027904
17/03/17 01:50:46 INFO mapred.JobClient:     Map output records=4089642
Job ended: Fri Mar 17 01:50:46 UTC 2017
The job took 344 seconds.
```

## CPU stress (hanoi on one node)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted2
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted2 with 5 reduces.
Job started: Thu Mar 16 18:49:13 UTC 2017
17/03/16 18:49:14 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 18:49:14 INFO mapred.JobClient: Running job: job_201703161829_0003
17/03/16 18:49:15 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 18:49:21 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 18:49:24 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 18:49:27 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 18:49:31 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 18:49:33 INFO mapred.JobClient: Task Id : attempt_201703161829_0003_r_000004_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 18:49:33 INFO mapred.JobClient: Task Id : attempt_201703161829_0003_r_000003_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 18:49:34 INFO mapred.JobClient:  map 12% reduce 0%
17/03/16 18:49:35 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 18:49:37 INFO mapred.JobClient:  map 13% reduce 2%
17/03/16 18:49:38 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 18:49:41 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 18:49:44 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 18:49:47 INFO mapred.JobClient:  map 19% reduce 5%
17/03/16 18:49:48 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 18:49:50 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 18:49:51 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 18:49:54 INFO mapred.JobClient:  map 26% reduce 6%
17/03/16 18:49:55 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 18:49:56 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 18:49:57 INFO mapred.JobClient:  map 27% reduce 8%
17/03/16 18:49:58 INFO mapred.JobClient:  map 29% reduce 8%
17/03/16 18:50:01 INFO mapred.JobClient:  map 31% reduce 8%
17/03/16 18:50:02 INFO mapred.JobClient:  map 32% reduce 8%
17/03/16 18:50:05 INFO mapred.JobClient:  map 34% reduce 9%
17/03/16 18:50:08 INFO mapred.JobClient:  map 34% reduce 11%
17/03/16 18:50:09 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 18:50:12 INFO mapred.JobClient:  map 38% reduce 11%
17/03/16 18:50:13 INFO mapred.JobClient:  map 39% reduce 11%
17/03/16 18:50:14 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 18:50:15 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 18:50:16 INFO mapred.JobClient:  map 41% reduce 12%
17/03/16 18:50:17 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 18:50:19 INFO mapred.JobClient:  map 43% reduce 12%
17/03/16 18:50:20 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 18:50:22 INFO mapred.JobClient:  map 45% reduce 13%
17/03/16 18:50:24 INFO mapred.JobClient:  map 46% reduce 14%
17/03/16 18:50:25 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 18:50:28 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 18:50:29 INFO mapred.JobClient:  map 49% reduce 15%
17/03/16 18:50:31 INFO mapred.JobClient:  map 50% reduce 15%
17/03/16 18:50:32 INFO mapred.JobClient:  map 52% reduce 15%
17/03/16 18:50:33 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 18:50:35 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 18:50:38 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 18:50:39 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 18:50:41 INFO mapred.JobClient:  map 57% reduce 18%
17/03/16 18:50:42 INFO mapred.JobClient:  map 58% reduce 18%
17/03/16 18:50:43 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 18:50:46 INFO mapred.JobClient:  map 60% reduce 18%
17/03/16 18:50:47 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 18:50:50 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 18:50:53 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 18:50:54 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 18:50:58 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 18:50:59 INFO mapred.JobClient:  map 69% reduce 22%
17/03/16 18:51:01 INFO mapred.JobClient:  map 70% reduce 22%
17/03/16 18:51:02 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 18:51:04 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 18:51:05 INFO mapred.JobClient:  map 73% reduce 23%
17/03/16 18:51:06 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 18:51:09 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 18:51:10 INFO mapred.JobClient:  map 76% reduce 24%
17/03/16 18:51:12 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 18:51:13 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 18:51:14 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 18:51:15 INFO mapred.JobClient:  map 79% reduce 26%
17/03/16 18:51:16 INFO mapred.JobClient:  map 80% reduce 26%
17/03/16 18:51:19 INFO mapred.JobClient:  map 81% reduce 26%
17/03/16 18:51:20 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 18:51:23 INFO mapred.JobClient:  map 85% reduce 26%
17/03/16 18:51:24 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 18:51:26 INFO mapred.JobClient:  map 86% reduce 27%
17/03/16 18:51:27 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 18:51:28 INFO mapred.JobClient:  map 88% reduce 27%
17/03/16 18:51:29 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 18:51:30 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 18:51:31 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 18:51:33 INFO mapred.JobClient:  map 91% reduce 29%
17/03/16 18:51:34 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 18:51:36 INFO mapred.JobClient:  map 93% reduce 30%
17/03/16 18:51:37 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 18:51:38 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 18:51:40 INFO mapred.JobClient:  map 95% reduce 31%
17/03/16 18:51:41 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 18:51:44 INFO mapred.JobClient:  map 99% reduce 31%
17/03/16 18:51:45 INFO mapred.JobClient:  map 100% reduce 31%
17/03/16 18:51:47 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 18:51:51 INFO mapred.JobClient:  map 100% reduce 39%
17/03/16 18:51:52 INFO mapred.JobClient:  map 100% reduce 53%
17/03/16 18:51:54 INFO mapred.JobClient:  map 100% reduce 60%
17/03/16 18:51:55 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 18:51:57 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 18:51:58 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 18:52:01 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 18:52:04 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 18:52:06 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 18:52:07 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 18:52:07 INFO mapred.JobClient: Task Id : attempt_201703161829_0003_r_000000_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 18:52:10 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 18:52:12 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 18:52:13 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 18:52:15 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 18:52:16 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 18:52:18 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 18:52:19 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 18:52:21 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 18:52:22 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 18:52:27 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 18:52:28 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 18:52:31 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 18:52:35 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 18:52:39 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 18:52:45 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 18:52:49 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 18:52:57 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 18:53:02 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 18:53:07 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 18:53:13 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 18:53:18 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 18:53:25 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 18:53:31 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 18:53:37 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 18:53:42 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 18:53:48 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 18:53:57 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 18:53:58 INFO mapred.JobClient: Job complete: job_201703161829_0003
17/03/16 18:53:58 INFO mapred.JobClient: Counters: 30
17/03/16 18:53:58 INFO mapred.JobClient:   Job Counters
17/03/16 18:53:58 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 18:53:58 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=848469
17/03/16 18:53:58 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 18:53:58 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 18:53:58 INFO mapred.JobClient:     Launched map tasks=243
17/03/16 18:53:58 INFO mapred.JobClient:     Data-local map tasks=243
17/03/16 18:53:58 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1325927
17/03/16 18:53:58 INFO mapred.JobClient:   File Input Format Counters
17/03/16 18:53:58 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 18:53:58 INFO mapred.JobClient:   File Output Format Counters
17/03/16 18:53:58 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 18:53:58 INFO mapred.JobClient:   FileSystemCounters
17/03/16 18:53:58 INFO mapred.JobClient:     FILE_BYTES_READ=94341423134
17/03/16 18:53:58 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 18:53:58 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126600794938
17/03/16 18:53:58 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 18:53:58 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 18:53:58 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 18:53:58 INFO mapred.JobClient:     Map input records=3068055
17/03/16 18:53:58 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 18:53:58 INFO mapred.JobClient:     Spilled Records=12042036
17/03/16 18:53:58 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 18:53:58 INFO mapred.JobClient:     Total committed heap usage (bytes)=49355423744
17/03/16 18:53:58 INFO mapred.JobClient:     CPU time spent (ms)=1556110
17/03/16 18:53:58 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 18:53:58 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 18:53:58 INFO mapred.JobClient:     Combine input records=0
17/03/16 18:53:58 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 18:53:58 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 18:53:58 INFO mapred.JobClient:     Combine output records=0
17/03/16 18:53:58 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52961882112
17/03/16 18:53:58 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 18:53:58 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196081897472
17/03/16 18:53:58 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 18:53:58 UTC 2017
The job took 284 seconds.
```

## CPU stress (stress --cpu 16 command on one node)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 19:03:25 UTC 2017
17/03/16 19:03:25 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 19:03:26 INFO mapred.JobClient: Running job: job_201703161829_0004
17/03/16 19:03:27 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 19:03:33 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 19:03:36 INFO mapred.JobClient:  map 4% reduce 0%
17/03/16 19:03:38 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 19:03:39 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 19:03:41 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 19:03:43 INFO mapred.JobClient:  map 9% reduce 0%
17/03/16 19:03:45 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 19:03:46 INFO mapred.JobClient:  map 11% reduce 0%
17/03/16 19:03:48 INFO mapred.JobClient:  map 11% reduce 2%
17/03/16 19:03:49 INFO mapred.JobClient:  map 12% reduce 3%
17/03/16 19:03:50 INFO mapred.JobClient:  map 14% reduce 3%
17/03/16 19:03:53 INFO mapred.JobClient:  map 16% reduce 3%
17/03/16 19:03:55 INFO mapred.JobClient:  map 16% reduce 4%
17/03/16 19:03:56 INFO mapred.JobClient:  map 17% reduce 4%
17/03/16 19:03:57 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 19:03:58 INFO mapred.JobClient:  map 19% reduce 5%
17/03/16 19:04:00 INFO mapred.JobClient:  map 20% reduce 5%
17/03/16 19:04:01 INFO mapred.JobClient:  map 21% reduce 4%
17/03/16 19:04:02 INFO mapred.JobClient: Task Id : attempt_201703161829_0004_r_000003_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:04:03 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 19:04:04 INFO mapred.JobClient:  map 23% reduce 5%
17/03/16 19:04:06 INFO mapred.JobClient:  map 24% reduce 5%
17/03/16 19:04:07 INFO mapred.JobClient:  map 25% reduce 5%
17/03/16 19:04:08 INFO mapred.JobClient:  map 26% reduce 5%
17/03/16 19:04:10 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 19:04:12 INFO mapred.JobClient:  map 28% reduce 6%
17/03/16 19:04:13 INFO mapred.JobClient:  map 29% reduce 7%
17/03/16 19:04:14 INFO mapred.JobClient:  map 30% reduce 7%
17/03/16 19:04:16 INFO mapred.JobClient:  map 30% reduce 8%
17/03/16 19:04:17 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 19:04:20 INFO mapred.JobClient:  map 33% reduce 10%
17/03/16 19:04:21 INFO mapred.JobClient:  map 34% reduce 10%
17/03/16 19:04:22 INFO mapred.JobClient:  map 35% reduce 10%
17/03/16 19:04:24 INFO mapred.JobClient:  map 36% reduce 10%
17/03/16 19:04:25 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 19:04:28 INFO mapred.JobClient:  map 38% reduce 11%
17/03/16 19:04:29 INFO mapred.JobClient:  map 40% reduce 11%
17/03/16 19:04:30 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 19:04:32 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 19:04:34 INFO mapred.JobClient:  map 42% reduce 13%
17/03/16 19:04:35 INFO mapred.JobClient:  map 43% reduce 13%
17/03/16 19:04:36 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 19:04:37 INFO mapred.JobClient:  map 45% reduce 13%
17/03/16 19:04:38 INFO mapred.JobClient:  map 45% reduce 14%
17/03/16 19:04:39 INFO mapred.JobClient:  map 46% reduce 14%
17/03/16 19:04:40 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 19:04:41 INFO mapred.JobClient:  map 48% reduce 14%
17/03/16 19:04:43 INFO mapred.JobClient:  map 49% reduce 15%
17/03/16 19:04:44 INFO mapred.JobClient:  map 50% reduce 15%
17/03/16 19:04:47 INFO mapred.JobClient:  map 52% reduce 15%
17/03/16 19:04:49 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 19:04:50 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 19:04:53 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 19:04:54 INFO mapred.JobClient:  map 56% reduce 17%
17/03/16 19:04:55 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 19:04:57 INFO mapred.JobClient:  map 58% reduce 17%
17/03/16 19:04:58 INFO mapred.JobClient:  map 59% reduce 17%
17/03/16 19:04:59 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 19:05:00 INFO mapred.JobClient:  map 60% reduce 18%
17/03/16 19:05:01 INFO mapred.JobClient:  map 61% reduce 18%
17/03/16 19:05:02 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 19:05:04 INFO mapred.JobClient:  map 63% reduce 19%
17/03/16 19:05:05 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 19:05:07 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 19:05:09 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 19:05:10 INFO mapred.JobClient:  map 67% reduce 20%
17/03/16 19:05:11 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 19:05:12 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 19:05:14 INFO mapred.JobClient:  map 69% reduce 21%
17/03/16 19:05:16 INFO mapred.JobClient:  map 70% reduce 21%
17/03/16 19:05:17 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 19:05:19 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 19:05:20 INFO mapred.JobClient:  map 73% reduce 23%
17/03/16 19:05:22 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 19:05:23 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 19:05:25 INFO mapred.JobClient:  map 76% reduce 23%
17/03/16 19:05:26 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 19:05:28 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 19:05:30 INFO mapred.JobClient:  map 79% reduce 24%
17/03/16 19:05:32 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 19:05:33 INFO mapred.JobClient:  map 81% reduce 25%
17/03/16 19:05:34 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 19:05:37 INFO mapred.JobClient:  map 84% reduce 26%
17/03/16 19:05:38 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 19:05:39 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 19:05:41 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 19:05:44 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 19:05:45 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 19:05:46 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 19:05:48 INFO mapred.JobClient:  map 91% reduce 28%
17/03/16 19:05:49 INFO mapred.JobClient:  map 92% reduce 28%
17/03/16 19:05:50 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 19:05:52 INFO mapred.JobClient:  map 93% reduce 30%
17/03/16 19:05:53 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 19:05:55 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 19:05:56 INFO mapred.JobClient:  map 96% reduce 30%
17/03/16 19:05:57 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 19:05:58 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 19:06:01 INFO mapred.JobClient:  map 99% reduce 31%
17/03/16 19:06:02 INFO mapred.JobClient:  map 100% reduce 31%
17/03/16 19:06:03 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 19:06:06 INFO mapred.JobClient:  map 100% reduce 33%
17/03/16 19:06:10 INFO mapred.JobClient:  map 100% reduce 46%
17/03/16 19:06:11 INFO mapred.JobClient:  map 100% reduce 53%
17/03/16 19:06:12 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 19:06:14 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 19:06:15 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 19:06:18 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 19:06:21 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 19:06:24 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 19:06:26 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 19:06:28 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 19:06:30 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 19:06:33 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 19:06:36 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 19:06:38 INFO mapred.JobClient: Task Id : attempt_201703161829_0004_r_000001_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:06:39 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 19:06:40 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 19:06:42 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 19:06:44 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 19:06:45 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 19:06:47 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 19:06:49 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 19:06:52 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 19:06:55 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 19:06:58 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 19:07:01 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 19:07:07 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 19:07:09 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 19:07:12 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 19:07:17 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 19:07:22 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 19:07:30 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 19:07:37 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 19:07:44 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 19:07:51 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 19:08:00 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 19:08:09 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 19:08:18 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 19:08:18 INFO mapred.JobClient: Job complete: job_201703161829_0004
17/03/16 19:08:18 INFO mapred.JobClient: Counters: 30
17/03/16 19:08:18 INFO mapred.JobClient:   Job Counters
17/03/16 19:08:18 INFO mapred.JobClient:     Launched reduce tasks=7
17/03/16 19:08:18 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=875193
17/03/16 19:08:18 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 19:08:18 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 19:08:18 INFO mapred.JobClient:     Launched map tasks=243
17/03/16 19:08:18 INFO mapred.JobClient:     Data-local map tasks=243
17/03/16 19:08:18 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1275789
17/03/16 19:08:18 INFO mapred.JobClient:   File Input Format Counters
17/03/16 19:08:18 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 19:08:18 INFO mapred.JobClient:   File Output Format Counters
17/03/16 19:08:18 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 19:08:18 INFO mapred.JobClient:   FileSystemCounters
17/03/16 19:08:18 INFO mapred.JobClient:     FILE_BYTES_READ=94385037489
17/03/16 19:08:18 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 19:08:18 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126644409048
17/03/16 19:08:18 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 19:08:18 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 19:08:18 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 19:08:18 INFO mapred.JobClient:     Map input records=3068055
17/03/16 19:08:18 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 19:08:18 INFO mapred.JobClient:     Spilled Records=12045928
17/03/16 19:08:18 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 19:08:18 INFO mapred.JobClient:     Total committed heap usage (bytes)=49346510848
17/03/16 19:08:18 INFO mapred.JobClient:     CPU time spent (ms)=1622900
17/03/16 19:08:18 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 19:08:18 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 19:08:18 INFO mapred.JobClient:     Combine input records=0
17/03/16 19:08:18 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 19:08:18 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 19:08:18 INFO mapred.JobClient:     Combine output records=0
17/03/16 19:08:18 INFO mapred.JobClient:     Physical memory (bytes) snapshot=53088194560
17/03/16 19:08:18 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 19:08:18 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=194228973568
17/03/16 19:08:18 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 19:08:18 UTC 2017
The job took 292 seconds.
```

## Disk stress (script provided on one node)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 19:10:19 UTC 2017
17/03/16 19:10:19 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 19:10:19 INFO mapred.JobClient: Running job: job_201703161829_0005
17/03/16 19:10:20 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 19:10:26 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 19:10:29 INFO mapred.JobClient:  map 4% reduce 0%
17/03/16 19:10:30 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 19:10:32 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 19:10:33 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 19:10:36 INFO mapred.JobClient:  map 9% reduce 0%
17/03/16 19:10:37 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 19:10:38 INFO mapred.JobClient: Task Id : attempt_201703161829_0005_r_000001_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:10:39 INFO mapred.JobClient:  map 11% reduce 0%
17/03/16 19:10:40 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 19:10:42 INFO mapred.JobClient:  map 13% reduce 2%
17/03/16 19:10:43 INFO mapred.JobClient:  map 14% reduce 2%
17/03/16 19:10:44 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 19:10:45 INFO mapred.JobClient: Task Id : attempt_201703161829_0005_r_000000_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:10:46 INFO mapred.JobClient:  map 16% reduce 2%
17/03/16 19:10:47 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 19:10:49 INFO mapred.JobClient:  map 19% reduce 3%
17/03/16 19:10:53 INFO mapred.JobClient:  map 21% reduce 4%
17/03/16 19:10:54 INFO mapred.JobClient:  map 22% reduce 4%
17/03/16 19:10:55 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 19:10:56 INFO mapred.JobClient:  map 23% reduce 5%
17/03/16 19:10:57 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 19:11:00 INFO mapred.JobClient:  map 26% reduce 6%
17/03/16 19:11:01 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 19:11:03 INFO mapred.JobClient:  map 28% reduce 7%
17/03/16 19:11:04 INFO mapred.JobClient:  map 29% reduce 7%
17/03/16 19:11:06 INFO mapred.JobClient:  map 30% reduce 8%
17/03/16 19:11:07 INFO mapred.JobClient:  map 31% reduce 8%
17/03/16 19:11:08 INFO mapred.JobClient:  map 32% reduce 8%
17/03/16 19:11:09 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 19:11:10 INFO mapred.JobClient:  map 33% reduce 9%
17/03/16 19:11:11 INFO mapred.JobClient:  map 34% reduce 9%
17/03/16 19:11:13 INFO mapred.JobClient:  map 35% reduce 9%
17/03/16 19:11:14 INFO mapred.JobClient:  map 35% reduce 10%
17/03/16 19:11:15 INFO mapred.JobClient:  map 37% reduce 10%
17/03/16 19:11:16 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 19:11:18 INFO mapred.JobClient:  map 38% reduce 11%
17/03/16 19:11:19 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 19:11:20 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 19:11:22 INFO mapred.JobClient:  map 41% reduce 12%
17/03/16 19:11:23 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 19:11:25 INFO mapred.JobClient:  map 43% reduce 12%
17/03/16 19:11:26 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 19:11:28 INFO mapred.JobClient:  map 45% reduce 13%
17/03/16 19:11:29 INFO mapred.JobClient:  map 46% reduce 13%
17/03/16 19:11:30 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 19:11:32 INFO mapred.JobClient:  map 48% reduce 14%
17/03/16 19:11:33 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 19:11:35 INFO mapred.JobClient:  map 50% reduce 15%
17/03/16 19:11:37 INFO mapred.JobClient:  map 52% reduce 15%
17/03/16 19:11:38 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 19:11:39 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 19:11:40 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 19:11:41 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 19:11:42 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 19:11:44 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 19:11:47 INFO mapred.JobClient:  map 58% reduce 17%
17/03/16 19:11:48 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 19:11:50 INFO mapred.JobClient:  map 60% reduce 19%
17/03/16 19:11:51 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 19:11:54 INFO mapred.JobClient:  map 63% reduce 19%
17/03/16 19:11:55 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 19:11:56 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 19:11:57 INFO mapred.JobClient:  map 65% reduce 20%
17/03/16 19:11:58 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 19:11:59 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 19:12:02 INFO mapred.JobClient:  map 69% reduce 22%
17/03/16 19:12:04 INFO mapred.JobClient:  map 70% reduce 22%
17/03/16 19:12:05 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 19:12:06 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 19:12:08 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 19:12:09 INFO mapred.JobClient:  map 74% reduce 22%
17/03/16 19:12:11 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 19:12:12 INFO mapred.JobClient:  map 76% reduce 24%
17/03/16 19:12:13 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 19:12:15 INFO mapred.JobClient:  map 78% reduce 25%
17/03/16 19:12:16 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 19:12:18 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 19:12:19 INFO mapred.JobClient:  map 81% reduce 25%
17/03/16 19:12:20 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 19:12:22 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 19:12:23 INFO mapred.JobClient:  map 84% reduce 26%
17/03/16 19:12:24 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 19:12:25 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 19:12:27 INFO mapred.JobClient:  map 86% reduce 27%
17/03/16 19:12:28 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 19:12:30 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 19:12:31 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 19:12:33 INFO mapred.JobClient:  map 91% reduce 28%
17/03/16 19:12:35 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 19:12:36 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 19:12:37 INFO mapred.JobClient:  map 94% reduce 29%
17/03/16 19:12:38 INFO mapred.JobClient:  map 95% reduce 29%
17/03/16 19:12:40 INFO mapred.JobClient:  map 96% reduce 30%
17/03/16 19:12:42 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 19:12:45 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 19:12:47 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 19:12:54 INFO mapred.JobClient:  map 100% reduce 39%
17/03/16 19:12:55 INFO mapred.JobClient:  map 100% reduce 47%
17/03/16 19:12:58 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 19:13:00 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 19:13:01 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 19:13:04 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 19:13:06 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 19:13:07 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 19:13:07 INFO mapred.JobClient: Task Id : attempt_201703161829_0005_r_000002_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:13:09 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 19:13:10 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 19:13:12 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 19:13:13 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 19:13:15 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 19:13:16 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 19:13:18 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 19:13:21 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 19:13:23 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 19:13:24 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 19:13:26 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 19:13:28 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 19:13:33 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 19:13:41 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 19:13:48 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 19:13:56 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 19:14:04 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 19:14:12 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 19:14:18 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 19:14:25 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 19:14:32 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 19:14:40 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 19:14:48 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 19:14:53 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 19:14:59 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 19:15:05 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 19:15:10 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 19:15:11 INFO mapred.JobClient: Job complete: job_201703161829_0005
17/03/16 19:15:11 INFO mapred.JobClient: Counters: 30
17/03/16 19:15:11 INFO mapred.JobClient:   Job Counters
17/03/16 19:15:11 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 19:15:11 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=835448
17/03/16 19:15:11 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 19:15:11 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 19:15:11 INFO mapred.JobClient:     Launched map tasks=242
17/03/16 19:15:11 INFO mapred.JobClient:     Data-local map tasks=242
17/03/16 19:15:11 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1325147
17/03/16 19:15:11 INFO mapred.JobClient:   File Input Format Counters
17/03/16 19:15:11 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 19:15:11 INFO mapred.JobClient:   File Output Format Counters
17/03/16 19:15:11 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 19:15:11 INFO mapred.JobClient:   FileSystemCounters
17/03/16 19:15:11 INFO mapred.JobClient:     FILE_BYTES_READ=94401371345
17/03/16 19:15:11 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 19:15:11 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126660742904
17/03/16 19:15:11 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 19:15:11 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 19:15:11 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 19:15:11 INFO mapred.JobClient:     Map input records=3068055
17/03/16 19:15:11 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 19:15:11 INFO mapred.JobClient:     Spilled Records=12047721
17/03/16 19:15:11 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 19:15:11 INFO mapred.JobClient:     Total committed heap usage (bytes)=49356996608
17/03/16 19:15:11 INFO mapred.JobClient:     CPU time spent (ms)=1599840
17/03/16 19:15:11 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 19:15:11 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 19:15:11 INFO mapred.JobClient:     Combine input records=0
17/03/16 19:15:11 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 19:15:11 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 19:15:11 INFO mapred.JobClient:     Combine output records=0
17/03/16 19:15:11 INFO mapred.JobClient:     Physical memory (bytes) snapshot=53027225600
17/03/16 19:15:11 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 19:15:11 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196195803136
17/03/16 19:15:11 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 19:15:11 UTC 2017
The job took 292 seconds.
```

## Death during map (20%)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 20:40:21 UTC 2017
17/03/16 20:40:22 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 20:40:22 INFO mapred.JobClient: Running job: job_201703162038_0001
17/03/16 20:40:23 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 20:40:30 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 20:40:32 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 20:40:33 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 20:40:36 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 20:40:39 INFO mapred.JobClient:  map 8% reduce 0%
17/03/16 20:40:40 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 20:40:41 INFO mapred.JobClient: Task Id : attempt_201703162038_0001_r_000002_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 20:40:41 INFO mapred.JobClient: Task Id : attempt_201703162038_0001_r_000001_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 20:40:43 INFO mapred.JobClient:  map 12% reduce 1%
17/03/16 20:40:46 INFO mapred.JobClient:  map 14% reduce 2%
17/03/16 20:40:47 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 20:40:50 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 20:40:53 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 20:40:55 INFO mapred.JobClient:  map 19% reduce 5%
17/03/16 20:40:56 INFO mapred.JobClient:  map 20% reduce 5%
17/03/16 20:40:57 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 20:41:00 INFO mapred.JobClient:  map 24% reduce 5%
17/03/16 20:41:01 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 20:41:03 INFO mapred.JobClient:  map 25% reduce 6%
17/03/16 20:41:08 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 20:41:11 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 20:41:12 INFO mapred.JobClient:  map 29% reduce 7%
17/03/16 20:41:16 INFO mapred.JobClient:  map 30% reduce 7%
17/03/16 20:41:18 INFO mapred.JobClient:  map 31% reduce 7%
17/03/16 20:41:19 INFO mapred.JobClient:  map 32% reduce 7%
17/03/16 20:41:20 INFO mapred.JobClient:  map 32% reduce 8%
17/03/16 20:41:23 INFO mapred.JobClient:  map 34% reduce 8%
17/03/16 20:41:27 INFO mapred.JobClient:  map 35% reduce 8%
17/03/16 20:41:29 INFO mapred.JobClient:  map 36% reduce 8%
17/03/16 20:41:31 INFO mapred.JobClient:  map 37% reduce 8%
17/03/16 20:41:32 INFO mapred.JobClient:  map 37% reduce 9%
17/03/16 20:41:33 INFO mapred.JobClient:  map 38% reduce 9%
17/03/16 20:41:34 INFO mapred.JobClient:  map 39% reduce 9%
17/03/16 20:41:38 INFO mapred.JobClient:  map 40% reduce 9%
17/03/16 20:41:40 INFO mapred.JobClient:  map 41% reduce 9%
17/03/16 20:41:41 INFO mapred.JobClient:  map 42% reduce 9%
17/03/16 20:41:45 INFO mapred.JobClient:  map 44% reduce 9%
17/03/16 20:41:47 INFO mapred.JobClient:  map 44% reduce 10%
17/03/16 20:41:48 INFO mapred.JobClient:  map 45% reduce 10%
17/03/16 20:41:50 INFO mapred.JobClient:  map 46% reduce 10%
17/03/16 20:41:51 INFO mapred.JobClient:  map 47% reduce 10%
17/03/16 20:41:54 INFO mapred.JobClient:  map 47% reduce 11%
17/03/16 20:41:55 INFO mapred.JobClient:  map 48% reduce 11%
17/03/16 20:41:56 INFO mapred.JobClient:  map 49% reduce 11%
17/03/16 20:41:59 INFO mapred.JobClient:  map 50% reduce 11%
17/03/16 20:42:02 INFO mapred.JobClient:  map 51% reduce 11%
17/03/16 20:42:03 INFO mapred.JobClient:  map 52% reduce 11%
17/03/16 20:42:06 INFO mapred.JobClient:  map 53% reduce 12%
17/03/16 20:42:07 INFO mapred.JobClient:  map 54% reduce 12%
17/03/16 20:42:10 INFO mapred.JobClient:  map 55% reduce 12%
17/03/16 20:42:14 INFO mapred.JobClient:  map 56% reduce 12%
17/03/16 20:42:15 INFO mapred.JobClient:  map 57% reduce 12%
17/03/16 20:42:18 INFO mapred.JobClient:  map 58% reduce 13%
17/03/16 20:42:19 INFO mapred.JobClient:  map 59% reduce 13%
17/03/16 20:42:21 INFO mapred.JobClient:  map 60% reduce 13%
17/03/16 20:42:25 INFO mapred.JobClient:  map 62% reduce 13%
17/03/16 20:42:28 INFO mapred.JobClient:  map 63% reduce 13%
17/03/16 20:42:29 INFO mapred.JobClient:  map 64% reduce 13%
17/03/16 20:42:30 INFO mapred.JobClient:  map 64% reduce 14%
17/03/16 20:42:32 INFO mapred.JobClient:  map 65% reduce 14%
17/03/16 20:42:35 INFO mapred.JobClient:  map 67% reduce 14%
17/03/16 20:42:39 INFO mapred.JobClient:  map 69% reduce 15%
17/03/16 20:42:42 INFO mapred.JobClient:  map 70% reduce 15%
17/03/16 20:42:46 INFO mapred.JobClient:  map 72% reduce 15%
17/03/16 20:42:48 INFO mapred.JobClient:  map 72% reduce 16%
17/03/16 20:42:49 INFO mapred.JobClient:  map 73% reduce 16%
17/03/16 20:42:51 INFO mapred.JobClient:  map 74% reduce 16%
17/03/16 20:42:53 INFO mapred.JobClient:  map 75% reduce 16%
17/03/16 20:42:56 INFO mapred.JobClient:  map 77% reduce 16%
17/03/16 20:42:59 INFO mapred.JobClient:  map 78% reduce 16%
17/03/16 20:43:00 INFO mapred.JobClient:  map 78% reduce 17%
17/03/16 20:43:01 INFO mapred.JobClient:  map 79% reduce 17%
17/03/16 20:43:03 INFO mapred.JobClient:  map 80% reduce 17%
17/03/16 20:43:06 INFO mapred.JobClient:  map 82% reduce 17%
17/03/16 20:43:09 INFO mapred.JobClient:  map 83% reduce 18%
17/03/16 20:43:11 INFO mapred.JobClient:  map 84% reduce 18%
17/03/16 20:43:14 INFO mapred.JobClient:  map 85% reduce 18%
17/03/16 20:43:17 INFO mapred.JobClient:  map 87% reduce 18%
17/03/16 20:43:20 INFO mapred.JobClient:  map 88% reduce 18%
17/03/16 20:43:21 INFO mapred.JobClient:  map 89% reduce 18%
17/03/16 20:43:24 INFO mapred.JobClient:  map 90% reduce 19%
17/03/16 20:43:27 INFO mapred.JobClient:  map 91% reduce 19%
17/03/16 20:43:28 INFO mapred.JobClient:  map 92% reduce 19%
17/03/16 20:43:30 INFO mapred.JobClient:  map 92% reduce 20%
17/03/16 20:43:31 INFO mapred.JobClient:  map 94% reduce 20%
17/03/16 20:43:34 INFO mapred.JobClient:  map 95% reduce 20%
17/03/16 20:43:36 INFO mapred.JobClient:  map 95% reduce 21%
17/03/16 20:43:37 INFO mapred.JobClient:  map 96% reduce 21%
17/03/16 20:43:38 INFO mapred.JobClient:  map 97% reduce 21%
17/03/16 20:43:41 INFO mapred.JobClient:  map 98% reduce 21%
17/03/16 20:43:42 INFO mapred.JobClient:  map 99% reduce 21%
17/03/16 20:43:44 INFO mapred.JobClient:  map 100% reduce 21%
17/03/16 20:43:51 INFO mapred.JobClient:  map 100% reduce 22%
17/03/16 20:52:48 INFO mapred.JobClient:  map 100% reduce 19%
17/03/16 20:52:49 INFO mapred.JobClient:  map 99% reduce 19%
17/03/16 20:52:50 INFO mapred.JobClient:  map 98% reduce 19%
17/03/16 20:52:59 INFO mapred.JobClient:  map 99% reduce 19%
17/03/16 20:52:59 INFO mapred.JobClient: Task Id : attempt_201703162038_0001_r_000004_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 20:53:00 INFO mapred.JobClient:  map 98% reduce 19%
17/03/16 20:53:03 INFO mapred.JobClient:  map 99% reduce 19%
17/03/16 20:53:05 INFO mapred.JobClient:  map 100% reduce 19%
17/03/16 20:53:11 INFO mapred.JobClient:  map 100% reduce 27%
17/03/16 20:53:12 INFO mapred.JobClient:  map 100% reduce 34%
17/03/16 20:53:14 INFO mapred.JobClient:  map 100% reduce 41%
17/03/16 20:53:15 INFO mapred.JobClient:  map 100% reduce 42%
17/03/16 20:53:17 INFO mapred.JobClient:  map 100% reduce 43%
17/03/16 20:53:18 INFO mapred.JobClient:  map 100% reduce 44%
17/03/16 20:53:20 INFO mapred.JobClient:  map 100% reduce 45%
17/03/16 20:53:21 INFO mapred.JobClient:  map 100% reduce 46%
17/03/16 20:53:24 INFO mapred.JobClient:  map 100% reduce 47%
17/03/16 20:53:26 INFO mapred.JobClient:  map 100% reduce 48%
17/03/16 20:53:27 INFO mapred.JobClient:  map 100% reduce 49%
17/03/16 20:53:29 INFO mapred.JobClient:  map 100% reduce 50%
17/03/16 20:53:32 INFO mapred.JobClient:  map 100% reduce 51%
17/03/16 20:53:33 INFO mapred.JobClient:  map 100% reduce 52%
17/03/16 20:53:36 INFO mapred.JobClient:  map 100% reduce 53%
17/03/16 20:53:38 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 20:53:39 INFO mapred.JobClient:  map 100% reduce 55%
17/03/16 20:53:42 INFO mapred.JobClient:  map 100% reduce 56%
17/03/16 20:53:44 INFO mapred.JobClient:  map 100% reduce 57%
17/03/16 20:53:46 INFO mapred.JobClient:  map 100% reduce 58%
17/03/16 20:53:51 INFO mapred.JobClient:  map 100% reduce 59%
17/03/16 20:53:54 INFO mapred.JobClient:  map 100% reduce 60%
17/03/16 20:54:06 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 20:54:09 INFO mapred.JobClient:  map 100% reduce 62%
17/03/16 20:54:10 INFO mapred.JobClient:  map 100% reduce 63%
17/03/16 20:54:13 INFO mapred.JobClient:  map 100% reduce 64%
17/03/16 20:54:17 INFO mapred.JobClient:  map 100% reduce 65%
17/03/16 20:54:18 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 20:54:21 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 20:54:23 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 20:54:26 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 20:54:29 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 20:54:33 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 20:54:36 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 20:54:39 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 20:54:45 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 20:54:47 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 20:54:53 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 20:54:56 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 20:54:59 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 20:55:02 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 20:55:09 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 20:55:18 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 20:55:26 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 20:55:32 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 20:55:40 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 20:55:46 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 20:55:54 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 20:56:00 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 20:56:06 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 20:56:07 INFO mapred.JobClient: Job complete: job_201703162038_0001
17/03/16 20:56:07 INFO mapred.JobClient: Counters: 30
17/03/16 20:56:07 INFO mapred.JobClient:   Job Counters
17/03/16 20:56:07 INFO mapred.JobClient:     Launched reduce tasks=10
17/03/16 20:56:07 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=873594
17/03/16 20:56:07 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 20:56:07 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 20:56:07 INFO mapred.JobClient:     Launched map tasks=261
17/03/16 20:56:07 INFO mapred.JobClient:     Data-local map tasks=261
17/03/16 20:56:07 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=2657840
17/03/16 20:56:07 INFO mapred.JobClient:   File Input Format Counters
17/03/16 20:56:07 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 20:56:07 INFO mapred.JobClient:   File Output Format Counters
17/03/16 20:56:07 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 20:56:07 INFO mapred.JobClient:   FileSystemCounters
17/03/16 20:56:07 INFO mapred.JobClient:     FILE_BYTES_READ=94369500548
17/03/16 20:56:07 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 20:56:07 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126628872107
17/03/16 20:56:07 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 20:56:07 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 20:56:07 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 20:56:07 INFO mapred.JobClient:     Map input records=3068055
17/03/16 20:56:07 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 20:56:07 INFO mapred.JobClient:     Spilled Records=12044883
17/03/16 20:56:07 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 20:56:07 INFO mapred.JobClient:     Total committed heap usage (bytes)=49321869312
17/03/16 20:56:07 INFO mapred.JobClient:     CPU time spent (ms)=1525110
17/03/16 20:56:07 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 20:56:07 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 20:56:07 INFO mapred.JobClient:     Combine input records=0
17/03/16 20:56:07 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 20:56:07 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 20:56:07 INFO mapred.JobClient:     Combine output records=0
17/03/16 20:56:07 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52859531264
17/03/16 20:56:07 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 20:56:07 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196565377024
17/03/16 20:56:07 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 20:56:07 UTC 2017
The job took 945 seconds.
```

## Death during map (20%) with expiry interval of 30s
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 21:22:12 UTC 2017
17/03/16 21:22:12 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 21:22:12 INFO mapred.JobClient: Running job: job_201703162120_0001
17/03/16 21:22:13 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 21:22:19 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 21:22:23 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 21:22:24 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 21:22:27 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 21:22:30 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 21:22:32 INFO mapred.JobClient: Task Id : attempt_201703162120_0001_r_000002_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 21:22:32 INFO mapred.JobClient: Task Id : attempt_201703162120_0001_r_000003_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 21:22:34 INFO mapred.JobClient:  map 12% reduce 1%
17/03/16 21:22:35 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 21:22:37 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 21:22:41 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 21:22:41 INFO mapred.JobClient: Task Id : attempt_201703162120_0001_r_000002_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 21:22:44 INFO mapred.JobClient:  map 19% reduce 3%
17/03/16 21:22:47 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 21:22:48 INFO mapred.JobClient:  map 22% reduce 4%
17/03/16 21:22:50 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 21:22:51 INFO mapred.JobClient:  map 24% reduce 5%
17/03/16 21:22:56 INFO mapred.JobClient:  map 25% reduce 5%
17/03/16 21:22:58 INFO mapred.JobClient:  map 26% reduce 5%
17/03/16 21:22:59 INFO mapred.JobClient:  map 27% reduce 5%
17/03/16 21:23:01 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 21:23:02 INFO mapred.JobClient:  map 28% reduce 6%
17/03/16 21:23:04 INFO mapred.JobClient:  map 29% reduce 6%
17/03/16 21:23:07 INFO mapred.JobClient:  map 30% reduce 6%
17/03/16 21:23:09 INFO mapred.JobClient:  map 31% reduce 6%
17/03/16 21:23:11 INFO mapred.JobClient:  map 32% reduce 6%
17/03/16 21:23:13 INFO mapred.JobClient:  map 33% reduce 7%
17/03/16 21:23:14 INFO mapred.JobClient:  map 34% reduce 7%
17/03/16 21:23:19 INFO mapred.JobClient:  map 35% reduce 7%
17/03/16 21:23:20 INFO mapred.JobClient:  map 36% reduce 8%
17/03/16 21:23:22 INFO mapred.JobClient:  map 37% reduce 8%
17/03/16 21:23:23 INFO mapred.JobClient:  map 37% reduce 6%
17/03/16 21:23:24 INFO mapred.JobClient:  map 38% reduce 6%
17/03/16 21:23:25 INFO mapred.JobClient:  map 39% reduce 7%
17/03/16 21:23:26 INFO mapred.JobClient:  map 38% reduce 7%
17/03/16 21:23:27 INFO mapred.JobClient:  map 37% reduce 7%
17/03/16 21:23:38 INFO mapred.JobClient:  map 37% reduce 8%
17/03/16 21:23:41 INFO mapred.JobClient:  map 38% reduce 9%
17/03/16 21:23:44 INFO mapred.JobClient:  map 38% reduce 10%
17/03/16 21:23:45 INFO mapred.JobClient:  map 39% reduce 10%
17/03/16 21:23:48 INFO mapred.JobClient:  map 40% reduce 10%
17/03/16 21:23:49 INFO mapred.JobClient:  map 41% reduce 10%
17/03/16 21:23:52 INFO mapred.JobClient:  map 43% reduce 10%
17/03/16 21:23:54 INFO mapred.JobClient:  map 43% reduce 11%
17/03/16 21:23:55 INFO mapred.JobClient:  map 44% reduce 11%
17/03/16 21:23:58 INFO mapred.JobClient:  map 45% reduce 11%
17/03/16 21:24:00 INFO mapred.JobClient:  map 46% reduce 11%
17/03/16 21:24:02 INFO mapred.JobClient:  map 47% reduce 11%
17/03/16 21:24:03 INFO mapred.JobClient:  map 48% reduce 11%
17/03/16 21:24:04 INFO mapred.JobClient:  map 48% reduce 12%
17/03/16 21:24:06 INFO mapred.JobClient:  map 49% reduce 12%
17/03/16 21:24:10 INFO mapred.JobClient:  map 51% reduce 12%
17/03/16 21:24:11 INFO mapred.JobClient:  map 51% reduce 13%
17/03/16 21:24:13 INFO mapred.JobClient:  map 52% reduce 13%
17/03/16 21:24:14 INFO mapred.JobClient:  map 53% reduce 13%
17/03/16 21:24:17 INFO mapred.JobClient:  map 54% reduce 13%
17/03/16 21:24:20 INFO mapred.JobClient:  map 55% reduce 14%
17/03/16 21:24:21 INFO mapred.JobClient:  map 56% reduce 14%
17/03/16 21:24:23 INFO mapred.JobClient:  map 57% reduce 14%
17/03/16 21:24:25 INFO mapred.JobClient:  map 58% reduce 14%
17/03/16 21:24:27 INFO mapred.JobClient:  map 59% reduce 14%
17/03/16 21:24:28 INFO mapred.JobClient:  map 59% reduce 15%
17/03/16 21:24:30 INFO mapred.JobClient:  map 60% reduce 15%
17/03/16 21:24:32 INFO mapred.JobClient:  map 61% reduce 15%
17/03/16 21:24:35 INFO mapred.JobClient:  map 63% reduce 15%
17/03/16 21:24:37 INFO mapred.JobClient:  map 63% reduce 16%
17/03/16 21:24:38 INFO mapred.JobClient:  map 64% reduce 16%
17/03/16 21:24:42 INFO mapred.JobClient:  map 65% reduce 16%
17/03/16 21:24:45 INFO mapred.JobClient:  map 67% reduce 17%
17/03/16 21:24:49 INFO mapred.JobClient:  map 69% reduce 17%
17/03/16 21:24:52 INFO mapred.JobClient:  map 70% reduce 17%
17/03/16 21:24:53 INFO mapred.JobClient:  map 70% reduce 18%
17/03/16 21:24:55 INFO mapred.JobClient:  map 71% reduce 18%
17/03/16 21:24:56 INFO mapred.JobClient:  map 72% reduce 18%
17/03/16 21:24:59 INFO mapred.JobClient:  map 73% reduce 18%
17/03/16 21:25:00 INFO mapred.JobClient:  map 74% reduce 18%
17/03/16 21:25:02 INFO mapred.JobClient:  map 74% reduce 19%
17/03/16 21:25:03 INFO mapred.JobClient:  map 75% reduce 19%
17/03/16 21:25:05 INFO mapred.JobClient:  map 76% reduce 19%
17/03/16 21:25:06 INFO mapred.JobClient:  map 77% reduce 19%
17/03/16 21:25:09 INFO mapred.JobClient:  map 77% reduce 20%
17/03/16 21:25:10 INFO mapred.JobClient:  map 78% reduce 20%
17/03/16 21:25:12 INFO mapred.JobClient:  map 79% reduce 20%
17/03/16 21:25:13 INFO mapred.JobClient:  map 80% reduce 20%
17/03/16 21:25:15 INFO mapred.JobClient:  map 81% reduce 20%
17/03/16 21:25:17 INFO mapred.JobClient:  map 82% reduce 20%
17/03/16 21:25:20 INFO mapred.JobClient:  map 83% reduce 21%
17/03/16 21:25:22 INFO mapred.JobClient:  map 84% reduce 21%
17/03/16 21:25:24 INFO mapred.JobClient:  map 85% reduce 21%
17/03/16 21:25:27 INFO mapred.JobClient:  map 86% reduce 22%
17/03/16 21:25:28 INFO mapred.JobClient:  map 87% reduce 22%
17/03/16 21:25:31 INFO mapred.JobClient:  map 88% reduce 22%
17/03/16 21:25:33 INFO mapred.JobClient:  map 88% reduce 23%
17/03/16 21:25:34 INFO mapred.JobClient:  map 89% reduce 23%
17/03/16 21:25:35 INFO mapred.JobClient:  map 90% reduce 23%
17/03/16 21:25:37 INFO mapred.JobClient:  map 91% reduce 23%
17/03/16 21:25:38 INFO mapred.JobClient:  map 92% reduce 23%
17/03/16 21:25:39 INFO mapred.JobClient:  map 92% reduce 24%
17/03/16 21:25:42 INFO mapred.JobClient:  map 93% reduce 24%
17/03/16 21:25:44 INFO mapred.JobClient:  map 94% reduce 24%
17/03/16 21:25:47 INFO mapred.JobClient:  map 95% reduce 24%
17/03/16 21:25:48 INFO mapred.JobClient:  map 95% reduce 25%
17/03/16 21:25:49 INFO mapred.JobClient:  map 96% reduce 25%
17/03/16 21:25:50 INFO mapred.JobClient:  map 97% reduce 25%
17/03/16 21:25:54 INFO mapred.JobClient:  map 98% reduce 25%
17/03/16 21:25:55 INFO mapred.JobClient:  map 99% reduce 25%
17/03/16 21:25:58 INFO mapred.JobClient:  map 100% reduce 25%
17/03/16 21:25:59 INFO mapred.JobClient:  map 100% reduce 26%
17/03/16 21:26:03 INFO mapred.JobClient:  map 100% reduce 33%
17/03/16 21:26:06 INFO mapred.JobClient:  map 100% reduce 34%
17/03/16 21:26:07 INFO mapred.JobClient:  map 100% reduce 40%
17/03/16 21:26:08 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 21:26:09 INFO mapred.JobClient:  map 100% reduce 55%
17/03/16 21:26:11 INFO mapred.JobClient:  map 100% reduce 56%
17/03/16 21:26:12 INFO mapred.JobClient:  map 100% reduce 57%
17/03/16 21:26:14 INFO mapred.JobClient:  map 100% reduce 58%
17/03/16 21:26:16 INFO mapred.JobClient:  map 100% reduce 59%
17/03/16 21:26:18 INFO mapred.JobClient:  map 100% reduce 60%
17/03/16 21:26:20 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 21:26:23 INFO mapred.JobClient:  map 100% reduce 62%
17/03/16 21:26:25 INFO mapred.JobClient:  map 100% reduce 63%
17/03/16 21:26:26 INFO mapred.JobClient:  map 100% reduce 64%
17/03/16 21:26:28 INFO mapred.JobClient:  map 100% reduce 65%
17/03/16 21:26:29 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 21:26:31 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 21:26:32 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 21:26:35 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 21:26:37 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 21:26:41 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 21:26:44 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 21:26:46 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 21:26:47 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 21:26:50 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 21:26:52 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 21:26:53 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 21:27:01 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 21:27:09 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 21:27:21 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 21:27:27 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 21:27:30 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 21:27:36 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 21:27:39 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 21:27:48 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 21:27:51 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 21:28:00 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 21:28:06 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 21:28:09 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 21:28:15 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 21:28:18 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 21:28:24 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 21:28:27 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 21:28:34 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 21:28:34 INFO mapred.JobClient: Job complete: job_201703162120_0001
17/03/16 21:28:34 INFO mapred.JobClient: Counters: 30
17/03/16 21:28:34 INFO mapred.JobClient:   Job Counters
17/03/16 21:28:34 INFO mapred.JobClient:     Launched reduce tasks=9
17/03/16 21:28:34 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=899694
17/03/16 21:28:34 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 21:28:34 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 21:28:34 INFO mapred.JobClient:     Launched map tasks=262
17/03/16 21:28:34 INFO mapred.JobClient:     Data-local map tasks=262
17/03/16 21:28:34 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1169078
17/03/16 21:28:34 INFO mapred.JobClient:   File Input Format Counters
17/03/16 21:28:34 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 21:28:34 INFO mapred.JobClient:   File Output Format Counters
17/03/16 21:28:34 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 21:28:34 INFO mapred.JobClient:   FileSystemCounters
17/03/16 21:28:34 INFO mapred.JobClient:     FILE_BYTES_READ=94476000990
17/03/16 21:28:34 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 21:28:34 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126735372304
17/03/16 21:28:34 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 21:28:34 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 21:28:34 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 21:28:34 INFO mapred.JobClient:     Map input records=3068055
17/03/16 21:28:34 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 21:28:34 INFO mapred.JobClient:     Spilled Records=12054832
17/03/16 21:28:34 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 21:28:34 INFO mapred.JobClient:     Total committed heap usage (bytes)=49358569472
17/03/16 21:28:34 INFO mapred.JobClient:     CPU time spent (ms)=1522850
17/03/16 21:28:34 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 21:28:34 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 21:28:34 INFO mapred.JobClient:     Combine input records=0
17/03/16 21:28:34 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 21:28:34 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 21:28:34 INFO mapred.JobClient:     Combine output records=0
17/03/16 21:28:34 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52925669376
17/03/16 21:28:34 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 21:28:34 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196127035392
17/03/16 21:28:34 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 21:28:34 UTC 2017
The job took 382 seconds.
```

## Death during map (20%) with expiry interval of 60s
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 22:14:33 UTC 2017
17/03/16 22:14:33 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 22:14:33 INFO mapred.JobClient: Running job: job_201703162213_0001
17/03/16 22:14:34 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 22:14:41 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 22:14:44 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 22:14:47 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 22:14:50 INFO mapred.JobClient:  map 8% reduce 0%
17/03/16 22:14:51 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 22:14:53 INFO mapred.JobClient: Task Id : attempt_201703162213_0001_r_000001_0, Status : FAILED
17/03/16 22:14:55 INFO mapred.JobClient:  map 12% reduce 1%
17/03/16 22:14:56 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 22:14:56 INFO mapred.JobClient: Task Id : attempt_201703162213_0001_r_000002_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 22:14:58 INFO mapred.JobClient:  map 13% reduce 2%
17/03/16 22:14:59 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 22:15:02 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 22:15:03 INFO mapred.JobClient: Task Id : attempt_201703162213_0001_r_000001_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 22:15:05 INFO mapred.JobClient:  map 19% reduce 3%
17/03/16 22:15:08 INFO mapred.JobClient:  map 20% reduce 3%
17/03/16 22:15:09 INFO mapred.JobClient:  map 22% reduce 3%
17/03/16 22:15:11 INFO mapred.JobClient:  map 22% reduce 4%
17/03/16 22:15:12 INFO mapred.JobClient:  map 24% reduce 4%
17/03/16 22:15:15 INFO mapred.JobClient:  map 25% reduce 4%
17/03/16 22:15:17 INFO mapred.JobClient:  map 25% reduce 5%
17/03/16 22:15:19 INFO mapred.JobClient:  map 26% reduce 5%
17/03/16 22:15:20 INFO mapred.JobClient:  map 27% reduce 5%
17/03/16 22:15:23 INFO mapred.JobClient:  map 28% reduce 5%
17/03/16 22:15:25 INFO mapred.JobClient:  map 29% reduce 5%
17/03/16 22:15:28 INFO mapred.JobClient:  map 30% reduce 5%
17/03/16 22:15:30 INFO mapred.JobClient:  map 31% reduce 5%
17/03/16 22:15:32 INFO mapred.JobClient:  map 32% reduce 6%
17/03/16 22:15:34 INFO mapred.JobClient:  map 33% reduce 6%
17/03/16 22:15:35 INFO mapred.JobClient:  map 34% reduce 6%
17/03/16 22:15:38 INFO mapred.JobClient:  map 35% reduce 6%
17/03/16 22:15:41 INFO mapred.JobClient:  map 36% reduce 6%
17/03/16 22:15:42 INFO mapred.JobClient:  map 37% reduce 6%
17/03/16 22:15:45 INFO mapred.JobClient:  map 38% reduce 6%
17/03/16 22:15:46 INFO mapred.JobClient:  map 39% reduce 6%
17/03/16 22:15:49 INFO mapred.JobClient:  map 40% reduce 6%
17/03/16 22:15:52 INFO mapred.JobClient:  map 41% reduce 6%
17/03/16 22:15:54 INFO mapred.JobClient:  map 42% reduce 7%
17/03/16 22:15:56 INFO mapred.JobClient:  map 43% reduce 7%
17/03/16 22:15:57 INFO mapred.JobClient:  map 44% reduce 7%
17/03/16 22:16:00 INFO mapred.JobClient:  map 45% reduce 7%
17/03/16 22:16:04 INFO mapred.JobClient:  map 46% reduce 7%
17/03/16 22:16:06 INFO mapred.JobClient:  map 47% reduce 7%
17/03/16 22:16:07 INFO mapred.JobClient:  map 48% reduce 7%
17/03/16 22:16:08 INFO mapred.JobClient:  map 48% reduce 8%
17/03/16 22:16:10 INFO mapred.JobClient:  map 49% reduce 8%
17/03/16 22:16:13 INFO mapred.JobClient:  map 50% reduce 6%
17/03/16 22:16:15 INFO mapred.JobClient:  map 49% reduce 6%
17/03/16 22:16:18 INFO mapred.JobClient:  map 51% reduce 6%
17/03/16 22:16:19 INFO mapred.JobClient:  map 49% reduce 6%
17/03/16 22:16:22 INFO mapred.JobClient:  map 49% reduce 7%
17/03/16 22:16:25 INFO mapred.JobClient:  map 50% reduce 7%
17/03/16 22:16:26 INFO mapred.JobClient:  map 49% reduce 8%
17/03/16 22:16:28 INFO mapred.JobClient:  map 50% reduce 8%
17/03/16 22:16:29 INFO mapred.JobClient:  map 49% reduce 9%
17/03/16 22:16:30 INFO mapred.JobClient:  map 50% reduce 9%
17/03/16 22:16:32 INFO mapred.JobClient:  map 51% reduce 10%
17/03/16 22:16:34 INFO mapred.JobClient:  map 52% reduce 10%
17/03/16 22:16:35 INFO mapred.JobClient:  map 52% reduce 12%
17/03/16 22:16:36 INFO mapred.JobClient:  map 53% reduce 12%
17/03/16 22:16:38 INFO mapred.JobClient:  map 53% reduce 13%
17/03/16 22:16:39 INFO mapred.JobClient:  map 54% reduce 13%
17/03/16 22:16:41 INFO mapred.JobClient:  map 54% reduce 14%
17/03/16 22:16:42 INFO mapred.JobClient:  map 55% reduce 14%
17/03/16 22:16:43 INFO mapred.JobClient:  map 56% reduce 14%
17/03/16 22:16:45 INFO mapred.JobClient:  map 57% reduce 14%
17/03/16 22:16:47 INFO mapred.JobClient:  map 58% reduce 14%
17/03/16 22:16:49 INFO mapred.JobClient:  map 59% reduce 15%
17/03/16 22:16:52 INFO mapred.JobClient:  map 60% reduce 15%
17/03/16 22:16:54 INFO mapred.JobClient:  map 61% reduce 15%
17/03/16 22:16:55 INFO mapred.JobClient:  map 62% reduce 15%
17/03/16 22:16:58 INFO mapred.JobClient:  map 63% reduce 16%
17/03/16 22:17:01 INFO mapred.JobClient:  map 64% reduce 16%
17/03/16 22:17:02 INFO mapred.JobClient:  map 65% reduce 16%
17/03/16 22:17:04 INFO mapred.JobClient:  map 65% reduce 17%
17/03/16 22:17:05 INFO mapred.JobClient:  map 66% reduce 17%
17/03/16 22:17:06 INFO mapred.JobClient:  map 67% reduce 17%
17/03/16 22:17:09 INFO mapred.JobClient:  map 68% reduce 17%
17/03/16 22:17:12 INFO mapred.JobClient:  map 69% reduce 17%
17/03/16 22:17:13 INFO mapred.JobClient:  map 70% reduce 17%
17/03/16 22:17:16 INFO mapred.JobClient:  map 72% reduce 18%
17/03/16 22:17:20 INFO mapred.JobClient:  map 73% reduce 18%
17/03/16 22:17:22 INFO mapred.JobClient:  map 74% reduce 19%
17/03/16 22:17:23 INFO mapred.JobClient:  map 75% reduce 19%
17/03/16 22:17:27 INFO mapred.JobClient:  map 77% reduce 19%
17/03/16 22:17:30 INFO mapred.JobClient:  map 78% reduce 20%
17/03/16 22:17:32 INFO mapred.JobClient:  map 79% reduce 20%
17/03/16 22:17:34 INFO mapred.JobClient:  map 80% reduce 20%
17/03/16 22:17:37 INFO mapred.JobClient:  map 81% reduce 20%
17/03/16 22:17:38 INFO mapred.JobClient:  map 82% reduce 20%
17/03/16 22:17:39 INFO mapred.JobClient:  map 82% reduce 21%
17/03/16 22:17:41 INFO mapred.JobClient:  map 83% reduce 21%
17/03/16 22:17:45 INFO mapred.JobClient:  map 85% reduce 22%
17/03/16 22:17:48 INFO mapred.JobClient:  map 86% reduce 22%
17/03/16 22:17:49 INFO mapred.JobClient:  map 87% reduce 22%
17/03/16 22:17:52 INFO mapred.JobClient:  map 88% reduce 22%
17/03/16 22:17:54 INFO mapred.JobClient:  map 88% reduce 23%
17/03/16 22:17:55 INFO mapred.JobClient:  map 89% reduce 23%
17/03/16 22:17:56 INFO mapred.JobClient:  map 90% reduce 23%
17/03/16 22:17:58 INFO mapred.JobClient:  map 91% reduce 23%
17/03/16 22:17:59 INFO mapred.JobClient:  map 92% reduce 23%
17/03/16 22:18:02 INFO mapred.JobClient:  map 93% reduce 23%
17/03/16 22:18:03 INFO mapred.JobClient:  map 93% reduce 24%
17/03/16 22:18:05 INFO mapred.JobClient:  map 94% reduce 24%
17/03/16 22:18:07 INFO mapred.JobClient:  map 95% reduce 24%
17/03/16 22:18:09 INFO mapred.JobClient:  map 96% reduce 24%
17/03/16 22:18:11 INFO mapred.JobClient:  map 96% reduce 25%
17/03/16 22:18:12 INFO mapred.JobClient:  map 97% reduce 25%
17/03/16 22:18:16 INFO mapred.JobClient:  map 98% reduce 25%
17/03/16 22:18:17 INFO mapred.JobClient:  map 99% reduce 25%
17/03/16 22:18:19 INFO mapred.JobClient:  map 100% reduce 25%
17/03/16 22:18:21 INFO mapred.JobClient:  map 100% reduce 26%
17/03/16 22:18:27 INFO mapred.JobClient:  map 100% reduce 41%
17/03/16 22:18:29 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 22:18:30 INFO mapred.JobClient:  map 100% reduce 55%
17/03/16 22:18:32 INFO mapred.JobClient:  map 100% reduce 56%
17/03/16 22:18:35 INFO mapred.JobClient:  map 100% reduce 57%
17/03/16 22:18:36 INFO mapred.JobClient:  map 100% reduce 58%
17/03/16 22:18:38 INFO mapred.JobClient:  map 100% reduce 59%
17/03/16 22:18:39 INFO mapred.JobClient:  map 100% reduce 60%
17/03/16 22:18:41 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 22:18:42 INFO mapred.JobClient:  map 100% reduce 62%
17/03/16 22:18:44 INFO mapred.JobClient:  map 100% reduce 63%
17/03/16 22:18:45 INFO mapred.JobClient:  map 100% reduce 64%
17/03/16 22:18:47 INFO mapred.JobClient:  map 100% reduce 65%
17/03/16 22:18:48 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 22:18:51 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 22:18:56 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 22:18:59 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 22:19:03 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 22:19:12 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 22:19:21 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 22:19:32 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 22:19:42 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 22:19:51 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 22:20:01 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 22:20:12 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 22:20:19 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 22:20:30 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 22:20:38 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 22:20:45 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 22:20:54 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 22:20:57 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 22:21:03 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 22:21:09 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 22:21:12 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 22:21:21 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 22:21:24 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 22:21:30 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 22:21:36 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 22:22:00 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 22:22:21 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 22:22:37 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 22:22:54 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 22:22:55 INFO mapred.JobClient: Job complete: job_201703162213_0001
17/03/16 22:22:55 INFO mapred.JobClient: Counters: 30
17/03/16 22:22:55 INFO mapred.JobClient:   Job Counters
17/03/16 22:22:55 INFO mapred.JobClient:     Launched reduce tasks=11
17/03/16 22:22:55 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=906124
17/03/16 22:22:55 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 22:22:55 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 22:22:55 INFO mapred.JobClient:     Launched map tasks=262
17/03/16 22:22:55 INFO mapred.JobClient:     Data-local map tasks=262
17/03/16 22:22:55 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1498946
17/03/16 22:22:55 INFO mapred.JobClient:   File Input Format Counters
17/03/16 22:22:55 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 22:22:55 INFO mapred.JobClient:   File Output Format Counters
17/03/16 22:22:55 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 22:22:55 INFO mapred.JobClient:   FileSystemCounters
17/03/16 22:22:55 INFO mapred.JobClient:     FILE_BYTES_READ=94345884216
17/03/16 22:22:55 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 22:22:55 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126605255530
17/03/16 22:22:55 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 22:22:55 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 22:22:55 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 22:22:55 INFO mapred.JobClient:     Map input records=3068055
17/03/16 22:22:55 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 22:22:55 INFO mapred.JobClient:     Spilled Records=12042685
17/03/16 22:22:55 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 22:22:55 INFO mapred.JobClient:     Total committed heap usage (bytes)=49332355072
17/03/16 22:22:55 INFO mapred.JobClient:     CPU time spent (ms)=1530590
17/03/16 22:22:55 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 22:22:55 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 22:22:55 INFO mapred.JobClient:     Combine input records=0
17/03/16 22:22:55 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 22:22:55 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 22:22:55 INFO mapred.JobClient:     Combine output records=0
17/03/16 22:22:55 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52902096896
17/03/16 22:22:55 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 22:22:55 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196402388992
17/03/16 22:22:55 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 22:22:55 UTC 2017
The job took 502 seconds.
```

## Death after map (reduce 46%)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 20:58:30 UTC 2017
17/03/16 20:58:30 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 20:58:31 INFO mapred.JobClient: Running job: job_201703162057_0001
17/03/16 20:58:32 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 20:58:39 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 20:58:41 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 20:58:42 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 20:58:45 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 20:58:48 INFO mapred.JobClient:  map 8% reduce 0%
17/03/16 20:58:49 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 20:58:51 INFO mapred.JobClient: Task Id : attempt_201703162057_0001_r_000004_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 20:58:52 INFO mapred.JobClient:  map 11% reduce 1%
17/03/16 20:58:53 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 20:58:55 INFO mapred.JobClient:  map 13% reduce 2%
17/03/16 20:58:56 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 20:58:59 INFO mapred.JobClient:  map 17% reduce 3%
17/03/16 20:59:02 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 20:59:05 INFO mapred.JobClient:  map 20% reduce 5%
17/03/16 20:59:06 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 20:59:08 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 20:59:09 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 20:59:11 INFO mapred.JobClient:  map 24% reduce 7%
17/03/16 20:59:12 INFO mapred.JobClient:  map 26% reduce 7%
17/03/16 20:59:13 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 20:59:15 INFO mapred.JobClient:  map 28% reduce 7%
17/03/16 20:59:16 INFO mapred.JobClient:  map 29% reduce 7%
17/03/16 20:59:17 INFO mapred.JobClient:  map 29% reduce 8%
17/03/16 20:59:19 INFO mapred.JobClient:  map 31% reduce 8%
17/03/16 20:59:20 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 20:59:22 INFO mapred.JobClient:  map 33% reduce 9%
17/03/16 20:59:23 INFO mapred.JobClient:  map 34% reduce 9%
17/03/16 20:59:25 INFO mapred.JobClient:  map 34% reduce 10%
17/03/16 20:59:26 INFO mapred.JobClient:  map 35% reduce 10%
17/03/16 20:59:28 INFO mapred.JobClient:  map 36% reduce 11%
17/03/16 20:59:29 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 20:59:31 INFO mapred.JobClient:  map 39% reduce 11%
17/03/16 20:59:33 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 20:59:34 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 20:59:35 INFO mapred.JobClient:  map 41% reduce 12%
17/03/16 20:59:36 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 20:59:38 INFO mapred.JobClient:  map 43% reduce 12%
17/03/16 20:59:39 INFO mapred.JobClient:  map 44% reduce 12%
17/03/16 20:59:41 INFO mapred.JobClient:  map 46% reduce 13%
17/03/16 20:59:43 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 20:59:45 INFO mapred.JobClient:  map 48% reduce 14%
17/03/16 20:59:46 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 20:59:48 INFO mapred.JobClient:  map 50% reduce 14%
17/03/16 20:59:49 INFO mapred.JobClient:  map 51% reduce 15%
17/03/16 20:59:50 INFO mapred.JobClient:  map 52% reduce 15%
17/03/16 20:59:51 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 20:59:52 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 20:59:53 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 20:59:55 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 20:59:56 INFO mapred.JobClient:  map 56% reduce 17%
17/03/16 20:59:57 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 20:59:59 INFO mapred.JobClient:  map 58% reduce 17%
17/03/16 21:00:00 INFO mapred.JobClient:  map 58% reduce 18%
17/03/16 21:00:01 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 21:00:02 INFO mapred.JobClient:  map 60% reduce 18%
17/03/16 21:00:04 INFO mapred.JobClient:  map 61% reduce 18%
17/03/16 21:00:06 INFO mapred.JobClient:  map 62% reduce 18%
17/03/16 21:00:07 INFO mapred.JobClient:  map 63% reduce 19%
17/03/16 21:00:08 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 21:00:09 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 21:00:12 INFO mapred.JobClient:  map 65% reduce 20%
17/03/16 21:00:13 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 21:00:14 INFO mapred.JobClient:  map 67% reduce 20%
17/03/16 21:00:15 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 21:00:16 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 21:00:17 INFO mapred.JobClient:  map 69% reduce 22%
17/03/16 21:00:20 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 21:00:21 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 21:00:23 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 21:00:24 INFO mapred.JobClient:  map 74% reduce 22%
17/03/16 21:00:25 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 21:00:27 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 21:00:29 INFO mapred.JobClient:  map 77% reduce 23%
17/03/16 21:00:30 INFO mapred.JobClient:  map 78% reduce 23%
17/03/16 21:00:31 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 21:00:33 INFO mapred.JobClient:  map 79% reduce 24%
17/03/16 21:00:34 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 21:00:35 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 21:00:36 INFO mapred.JobClient:  map 81% reduce 25%
17/03/16 21:00:37 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 21:00:38 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 21:00:40 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 21:00:42 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 21:00:43 INFO mapred.JobClient:  map 86% reduce 27%
17/03/16 21:00:44 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 21:00:45 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 21:00:47 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 21:00:49 INFO mapred.JobClient:  map 90% reduce 29%
17/03/16 21:00:50 INFO mapred.JobClient:  map 91% reduce 29%
17/03/16 21:00:51 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 21:00:52 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 21:00:54 INFO mapred.JobClient:  map 94% reduce 29%
17/03/16 21:00:55 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 21:00:57 INFO mapred.JobClient:  map 96% reduce 30%
17/03/16 21:00:58 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 21:00:59 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 21:01:01 INFO mapred.JobClient:  map 99% reduce 32%
17/03/16 21:01:02 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 21:01:07 INFO mapred.JobClient:  map 100% reduce 39%
17/03/16 21:01:08 INFO mapred.JobClient:  map 100% reduce 46%
17/03/16 21:01:09 INFO mapred.JobClient:  map 100% reduce 53%
17/03/16 21:01:10 INFO mapred.JobClient:  map 100% reduce 60%
17/03/16 21:01:13 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 21:01:15 INFO mapred.JobClient:  map 100% reduce 62%
17/03/16 21:01:18 INFO mapred.JobClient:  map 100% reduce 63%
17/03/16 21:01:22 INFO mapred.JobClient:  map 100% reduce 64%
17/03/16 21:01:26 INFO mapred.JobClient:  map 100% reduce 65%
17/03/16 21:01:29 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 21:01:32 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 21:01:35 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 21:01:38 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 21:01:39 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 21:01:43 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 21:01:44 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 21:01:47 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 21:01:49 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 21:01:53 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 21:02:05 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 21:02:13 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 21:02:19 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 21:02:23 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 21:02:32 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 21:11:38 INFO mapred.JobClient:  map 99% reduce 64%
17/03/16 21:11:39 INFO mapred.JobClient:  map 98% reduce 64%
17/03/16 21:11:41 INFO mapred.JobClient:  map 99% reduce 64%
17/03/16 21:11:42 INFO mapred.JobClient:  map 98% reduce 64%
17/03/16 21:11:50 INFO mapred.JobClient:  map 98% reduce 65%
17/03/16 21:11:51 INFO mapred.JobClient:  map 99% reduce 65%
17/03/16 21:11:52 INFO mapred.JobClient:  map 98% reduce 65%
17/03/16 21:11:53 INFO mapred.JobClient:  map 98% reduce 66%
17/03/16 21:11:59 INFO mapred.JobClient:  map 98% reduce 67%
17/03/16 21:12:01 INFO mapred.JobClient:  map 99% reduce 67%
17/03/16 21:12:02 INFO mapred.JobClient:  map 98% reduce 68%
17/03/16 21:12:05 INFO mapred.JobClient:  map 98% reduce 69%
17/03/16 21:12:08 INFO mapred.JobClient:  map 98% reduce 70%
17/03/16 21:12:11 INFO mapred.JobClient:  map 99% reduce 70%
17/03/16 21:12:12 INFO mapred.JobClient:  map 98% reduce 70%
17/03/16 21:12:19 INFO mapred.JobClient:  map 98% reduce 71%
17/03/16 21:12:20 INFO mapred.JobClient:  map 99% reduce 71%
17/03/16 21:12:21 INFO mapred.JobClient:  map 98% reduce 71%
17/03/16 21:12:28 INFO mapred.JobClient:  map 99% reduce 71%
17/03/16 21:12:29 INFO mapred.JobClient:  map 98% reduce 71%
17/03/16 21:12:34 INFO mapred.JobClient:  map 98% reduce 72%
17/03/16 21:12:39 INFO mapred.JobClient:  map 99% reduce 72%
17/03/16 21:12:40 INFO mapred.JobClient:  map 98% reduce 72%
17/03/16 21:12:41 INFO mapred.JobClient:  map 99% reduce 72%
17/03/16 21:12:42 INFO mapred.JobClient:  map 98% reduce 72%
17/03/16 21:12:46 INFO mapred.JobClient:  map 99% reduce 72%
17/03/16 21:12:50 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 21:12:53 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 21:12:58 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 21:13:00 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 21:13:03 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 21:13:04 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 21:13:07 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 21:13:09 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 21:13:12 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 21:13:13 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 21:13:16 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 21:13:19 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 21:13:22 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 21:13:24 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 21:13:27 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 21:13:28 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 21:13:33 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 21:13:35 INFO mapred.JobClient: Job complete: job_201703162057_0001
17/03/16 21:13:35 INFO mapred.JobClient: Counters: 30
17/03/16 21:13:35 INFO mapred.JobClient:   Job Counters
17/03/16 21:13:35 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 21:13:35 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=1115445
17/03/16 21:13:35 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 21:13:35 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 21:13:35 INFO mapred.JobClient:     Launched map tasks=324
17/03/16 21:13:35 INFO mapred.JobClient:     Data-local map tasks=324
17/03/16 21:13:35 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1527675
17/03/16 21:13:35 INFO mapred.JobClient:   File Input Format Counters
17/03/16 21:13:35 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 21:13:35 INFO mapred.JobClient:   File Output Format Counters
17/03/16 21:13:35 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 21:13:35 INFO mapred.JobClient:   FileSystemCounters
17/03/16 21:13:35 INFO mapred.JobClient:     FILE_BYTES_READ=94257179133
17/03/16 21:13:35 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 21:13:35 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126516550692
17/03/16 21:13:35 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 21:13:35 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 21:13:35 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 21:13:35 INFO mapred.JobClient:     Map input records=3068055
17/03/16 21:13:35 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 21:13:35 INFO mapred.JobClient:     Spilled Records=12034178
17/03/16 21:13:35 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 21:13:35 INFO mapred.JobClient:     Total committed heap usage (bytes)=49353850880
17/03/16 21:13:35 INFO mapred.JobClient:     CPU time spent (ms)=1549480
17/03/16 21:13:35 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 21:13:35 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 21:13:35 INFO mapred.JobClient:     Combine input records=0
17/03/16 21:13:35 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 21:13:35 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 21:13:35 INFO mapred.JobClient:     Combine output records=0
17/03/16 21:13:35 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52923805696
17/03/16 21:13:35 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 21:13:35 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196524367872
17/03/16 21:13:35 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 21:13:35 UTC 2017
The job took 904 seconds.
```

## Death after map (reduce 32%) with expiry interval of 30s
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 21:37:43 UTC 2017
17/03/16 21:37:43 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 21:37:43 INFO mapred.JobClient: Running job: job_201703162137_0001
17/03/16 21:37:44 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 21:37:50 INFO mapred.JobClient:  map 1% reduce 0%
17/03/16 21:37:51 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 21:37:53 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 21:37:54 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 21:37:57 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 21:38:00 INFO mapred.JobClient:  map 9% reduce 0%
17/03/16 21:38:01 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 21:38:04 INFO mapred.JobClient:  map 12% reduce 1%
17/03/16 21:38:05 INFO mapred.JobClient:  map 12% reduce 3%
17/03/16 21:38:08 INFO mapred.JobClient:  map 15% reduce 3%
17/03/16 21:38:11 INFO mapred.JobClient:  map 17% reduce 3%
17/03/16 21:38:14 INFO mapred.JobClient:  map 18% reduce 5%
17/03/16 21:38:15 INFO mapred.JobClient:  map 19% reduce 5%
17/03/16 21:38:18 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 21:38:20 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 21:38:21 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 21:38:24 INFO mapred.JobClient:  map 25% reduce 6%
17/03/16 21:38:25 INFO mapred.JobClient:  map 26% reduce 6%
17/03/16 21:38:26 INFO mapred.JobClient:  map 27% reduce 8%
17/03/16 21:38:28 INFO mapred.JobClient:  map 29% reduce 6%
17/03/16 21:38:29 INFO mapred.JobClient: Task Id : attempt_201703162137_0001_r_000001_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 21:38:31 INFO mapred.JobClient:  map 30% reduce 6%
17/03/16 21:38:33 INFO mapred.JobClient:  map 31% reduce 7%
17/03/16 21:38:34 INFO mapred.JobClient:  map 32% reduce 7%
17/03/16 21:38:36 INFO mapred.JobClient:  map 33% reduce 7%
17/03/16 21:38:37 INFO mapred.JobClient:  map 34% reduce 7%
17/03/16 21:38:39 INFO mapred.JobClient:  map 35% reduce 8%
17/03/16 21:38:41 INFO mapred.JobClient:  map 36% reduce 8%
17/03/16 21:38:42 INFO mapred.JobClient:  map 37% reduce 9%
17/03/16 21:38:43 INFO mapred.JobClient:  map 38% reduce 9%
17/03/16 21:38:45 INFO mapred.JobClient:  map 38% reduce 10%
17/03/16 21:38:46 INFO mapred.JobClient:  map 39% reduce 10%
17/03/16 21:38:48 INFO mapred.JobClient:  map 40% reduce 11%
17/03/16 21:38:50 INFO mapred.JobClient:  map 41% reduce 11%
17/03/16 21:38:51 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 21:38:53 INFO mapred.JobClient:  map 43% reduce 13%
17/03/16 21:38:54 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 21:38:57 INFO mapred.JobClient:  map 45% reduce 14%
17/03/16 21:38:58 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 21:39:00 INFO mapred.JobClient:  map 48% reduce 14%
17/03/16 21:39:01 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 21:39:04 INFO mapred.JobClient:  map 51% reduce 15%
17/03/16 21:39:05 INFO mapred.JobClient:  map 52% reduce 15%
17/03/16 21:39:07 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 21:39:08 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 21:39:10 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 21:39:11 INFO mapred.JobClient:  map 56% reduce 17%
17/03/16 21:39:14 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 21:39:15 INFO mapred.JobClient:  map 59% reduce 17%
17/03/16 21:39:16 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 21:39:18 INFO mapred.JobClient:  map 60% reduce 18%
17/03/16 21:39:19 INFO mapred.JobClient:  map 60% reduce 19%
17/03/16 21:39:20 INFO mapred.JobClient:  map 61% reduce 19%
17/03/16 21:39:21 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 21:39:22 INFO mapred.JobClient:  map 63% reduce 20%
17/03/16 21:39:24 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 21:39:25 INFO mapred.JobClient:  map 65% reduce 20%
17/03/16 21:39:27 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 21:39:28 INFO mapred.JobClient:  map 66% reduce 21%
17/03/16 21:39:29 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 21:39:30 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 21:39:31 INFO mapred.JobClient:  map 69% reduce 21%
17/03/16 21:39:32 INFO mapred.JobClient:  map 69% reduce 22%
17/03/16 21:39:33 INFO mapred.JobClient:  map 70% reduce 22%
17/03/16 21:39:34 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 21:39:35 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 21:39:36 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 21:39:37 INFO mapred.JobClient:  map 74% reduce 22%
17/03/16 21:39:38 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 21:39:40 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 21:39:41 INFO mapred.JobClient:  map 76% reduce 24%
17/03/16 21:39:43 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 21:39:44 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 21:39:46 INFO mapred.JobClient:  map 79% reduce 24%
17/03/16 21:39:47 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 21:39:50 INFO mapred.JobClient:  map 81% reduce 26%
17/03/16 21:39:51 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 21:39:52 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 21:39:54 INFO mapred.JobClient:  map 84% reduce 26%
17/03/16 21:39:55 INFO mapred.JobClient:  map 85% reduce 26%
17/03/16 21:39:56 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 21:39:57 INFO mapred.JobClient:  map 86% reduce 27%
17/03/16 21:39:58 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 21:39:59 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 21:40:02 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 21:40:04 INFO mapred.JobClient:  map 91% reduce 28%
17/03/16 21:40:05 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 21:40:06 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 21:40:08 INFO mapred.JobClient:  map 93% reduce 30%
17/03/16 21:40:10 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 21:40:11 INFO mapred.JobClient:  map 95% reduce 31%
17/03/16 21:40:12 INFO mapred.JobClient:  map 96% reduce 31%
17/03/16 21:40:13 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 21:40:14 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 21:40:16 INFO mapred.JobClient:  map 99% reduce 31%
17/03/16 21:40:17 INFO mapred.JobClient:  map 100% reduce 31%
17/03/16 21:40:18 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 21:40:54 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:40:57 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:40:58 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:41:04 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:41:05 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:41:11 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:41:12 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:41:15 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:41:16 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:41:18 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:41:19 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:41:21 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:41:22 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:41:32 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:41:33 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:41:38 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:41:39 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:41:48 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:41:49 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:41:56 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:41:57 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:41:58 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:42:00 INFO mapred.JobClient:  map 98% reduce 26%
17/03/16 21:42:03 INFO mapred.JobClient:  map 99% reduce 26%
17/03/16 21:42:06 INFO mapred.JobClient:  map 100% reduce 26%
17/03/16 21:42:13 INFO mapred.JobClient:  map 100% reduce 33%
17/03/16 21:42:15 INFO mapred.JobClient:  map 100% reduce 40%
17/03/16 21:42:18 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 21:42:19 INFO mapred.JobClient:  map 100% reduce 55%
17/03/16 21:42:21 INFO mapred.JobClient:  map 100% reduce 56%
17/03/16 21:42:22 INFO mapred.JobClient:  map 100% reduce 57%
17/03/16 21:42:24 INFO mapred.JobClient:  map 100% reduce 58%
17/03/16 21:42:27 INFO mapred.JobClient:  map 100% reduce 60%
17/03/16 21:42:30 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 21:42:31 INFO mapred.JobClient:  map 100% reduce 62%
17/03/16 21:42:33 INFO mapred.JobClient:  map 100% reduce 63%
17/03/16 21:42:34 INFO mapred.JobClient:  map 100% reduce 64%
17/03/16 21:42:37 INFO mapred.JobClient:  map 100% reduce 65%
17/03/16 21:42:39 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 21:42:40 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 21:42:42 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 21:42:45 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 21:42:46 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 21:42:48 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 21:42:49 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 21:42:52 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 21:42:54 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 21:42:57 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 21:42:58 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 21:43:01 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 21:43:04 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 21:43:07 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 21:43:13 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 21:43:17 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 21:43:25 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 21:43:31 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 21:43:34 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 21:43:40 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 21:43:46 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 21:44:00 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 21:44:04 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 21:44:12 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 21:44:27 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 21:44:45 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 21:45:00 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 21:45:15 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 21:45:31 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 21:45:32 INFO mapred.JobClient: Job complete: job_201703162137_0001
17/03/16 21:45:32 INFO mapred.JobClient: Counters: 30
17/03/16 21:45:32 INFO mapred.JobClient:   Job Counters
17/03/16 21:45:32 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 21:45:32 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=1122057
17/03/16 21:45:32 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 21:45:32 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 21:45:32 INFO mapred.JobClient:     Launched map tasks=321
17/03/16 21:45:32 INFO mapred.JobClient:     Data-local map tasks=321
17/03/16 21:45:32 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1367851
17/03/16 21:45:32 INFO mapred.JobClient:   File Input Format Counters
17/03/16 21:45:32 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 21:45:32 INFO mapred.JobClient:   File Output Format Counters
17/03/16 21:45:32 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 21:45:32 INFO mapred.JobClient:   FileSystemCounters
17/03/16 21:45:32 INFO mapred.JobClient:     FILE_BYTES_READ=94399860025
17/03/16 21:45:32 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 21:45:32 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126659231339
17/03/16 21:45:32 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 21:45:32 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 21:45:32 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 21:45:32 INFO mapred.JobClient:     Map input records=3068055
17/03/16 21:45:32 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 21:45:32 INFO mapred.JobClient:     Spilled Records=12047375
17/03/16 21:45:32 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 21:45:32 INFO mapred.JobClient:     Total committed heap usage (bytes)=49344937984
17/03/16 21:45:32 INFO mapred.JobClient:     CPU time spent (ms)=1543820
17/03/16 21:45:32 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 21:45:32 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 21:45:32 INFO mapred.JobClient:     Combine input records=0
17/03/16 21:45:32 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 21:45:32 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 21:45:32 INFO mapred.JobClient:     Combine output records=0
17/03/16 21:45:32 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52952838144
17/03/16 21:45:32 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 21:45:32 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=197086748672
17/03/16 21:45:32 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 21:45:32 UTC 2017
The job took 469 seconds.
```

## Death after map (reduce 31%) with expiry interval of 60s
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 22:25:53 UTC 2017
17/03/16 22:25:53 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 22:25:54 INFO mapred.JobClient: Running job: job_201703162224_0001
17/03/16 22:25:55 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 22:26:01 INFO mapred.JobClient:  map 1% reduce 0%
17/03/16 22:26:02 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 22:26:04 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 22:26:05 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 22:26:08 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 22:26:11 INFO mapred.JobClient:  map 9% reduce 0%
17/03/16 22:26:12 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 22:26:13 INFO mapred.JobClient: Task Id : attempt_201703162224_0001_r_000001_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 22:26:15 INFO mapred.JobClient:  map 12% reduce 0%
17/03/16 22:26:16 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 22:26:18 INFO mapred.JobClient:  map 14% reduce 2%
17/03/16 22:26:19 INFO mapred.JobClient:  map 15% reduce 3%
17/03/16 22:26:22 INFO mapred.JobClient:  map 17% reduce 3%
17/03/16 22:26:25 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 22:26:28 INFO mapred.JobClient:  map 21% reduce 5%
17/03/16 22:26:29 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 22:26:31 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 22:26:32 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 22:26:34 INFO mapred.JobClient:  map 24% reduce 7%
17/03/16 22:26:35 INFO mapred.JobClient:  map 26% reduce 7%
17/03/16 22:26:36 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 22:26:38 INFO mapred.JobClient:  map 28% reduce 7%
17/03/16 22:26:39 INFO mapred.JobClient:  map 29% reduce 7%
17/03/16 22:26:40 INFO mapred.JobClient:  map 29% reduce 8%
17/03/16 22:26:42 INFO mapred.JobClient:  map 30% reduce 8%
17/03/16 22:26:43 INFO mapred.JobClient:  map 31% reduce 9%
17/03/16 22:26:45 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 22:26:46 INFO mapred.JobClient:  map 33% reduce 9%
17/03/16 22:26:47 INFO mapred.JobClient:  map 34% reduce 10%
17/03/16 22:26:49 INFO mapred.JobClient:  map 35% reduce 10%
17/03/16 22:26:50 INFO mapred.JobClient:  map 36% reduce 10%
17/03/16 22:26:52 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 22:26:54 INFO mapred.JobClient:  map 39% reduce 11%
17/03/16 22:26:55 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 22:26:57 INFO mapred.JobClient:  map 41% reduce 12%
17/03/16 22:26:59 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 22:27:00 INFO mapred.JobClient:  map 43% reduce 12%
17/03/16 22:27:01 INFO mapred.JobClient:  map 44% reduce 12%
17/03/16 22:27:02 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 22:27:04 INFO mapred.JobClient:  map 46% reduce 13%
17/03/16 22:27:07 INFO mapred.JobClient:  map 48% reduce 14%
17/03/16 22:27:09 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 22:27:11 INFO mapred.JobClient:  map 50% reduce 15%
17/03/16 22:27:12 INFO mapred.JobClient:  map 51% reduce 15%
17/03/16 22:27:13 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 22:27:14 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 22:27:16 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 22:27:17 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 22:27:18 INFO mapred.JobClient:  map 56% reduce 17%
17/03/16 22:27:21 INFO mapred.JobClient:  map 58% reduce 17%
17/03/16 22:27:23 INFO mapred.JobClient:  map 59% reduce 17%
17/03/16 22:27:25 INFO mapred.JobClient:  map 60% reduce 17%
17/03/16 22:27:26 INFO mapred.JobClient:  map 61% reduce 18%
17/03/16 22:27:28 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 22:27:30 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 22:27:32 INFO mapred.JobClient:  map 65% reduce 20%
17/03/16 22:27:34 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 22:27:35 INFO mapred.JobClient:  map 66% reduce 21%
17/03/16 22:27:36 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 22:27:37 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 22:27:38 INFO mapred.JobClient:  map 69% reduce 21%
17/03/16 22:27:39 INFO mapred.JobClient:  map 70% reduce 21%
17/03/16 22:27:40 INFO mapred.JobClient:  map 71% reduce 21%
17/03/16 22:27:41 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 22:27:42 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 22:27:43 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 22:27:44 INFO mapred.JobClient:  map 73% reduce 23%
17/03/16 22:27:45 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 22:27:46 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 22:27:47 INFO mapred.JobClient:  map 76% reduce 23%
17/03/16 22:27:49 INFO mapred.JobClient:  map 77% reduce 23%
17/03/16 22:27:50 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 22:27:52 INFO mapred.JobClient:  map 79% reduce 24%
17/03/16 22:27:53 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 22:27:54 INFO mapred.JobClient:  map 81% reduce 25%
17/03/16 22:27:56 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 22:27:57 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 22:27:59 INFO mapred.JobClient:  map 84% reduce 26%
17/03/16 22:28:00 INFO mapred.JobClient:  map 85% reduce 26%
17/03/16 22:28:01 INFO mapred.JobClient:  map 86% reduce 27%
17/03/16 22:28:03 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 22:28:04 INFO mapred.JobClient:  map 87% reduce 28%
17/03/16 22:28:05 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 22:28:06 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 22:28:07 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 22:28:08 INFO mapred.JobClient:  map 90% reduce 29%
17/03/16 22:28:09 INFO mapred.JobClient:  map 91% reduce 29%
17/03/16 22:28:10 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 22:28:12 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 22:28:13 INFO mapred.JobClient:  map 94% reduce 29%
17/03/16 22:28:14 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 22:28:16 INFO mapred.JobClient:  map 96% reduce 30%
17/03/16 22:28:17 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 22:28:19 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 22:28:20 INFO mapred.JobClient:  map 99% reduce 31%
17/03/16 22:28:21 INFO mapred.JobClient:  map 100% reduce 31%
17/03/16 22:28:22 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 22:28:28 INFO mapred.JobClient:  map 100% reduce 39%
17/03/16 22:28:32 INFO mapred.JobClient:  map 100% reduce 40%
17/03/16 22:28:38 INFO mapred.JobClient:  map 100% reduce 41%
17/03/16 22:28:41 INFO mapred.JobClient:  map 100% reduce 42%
17/03/16 22:28:47 INFO mapred.JobClient:  map 100% reduce 43%
17/03/16 22:28:53 INFO mapred.JobClient:  map 100% reduce 44%
17/03/16 22:28:59 INFO mapred.JobClient:  map 100% reduce 45%
17/03/16 22:29:39 INFO mapred.JobClient:  map 100% reduce 33%
17/03/16 22:29:40 INFO mapred.JobClient:  map 98% reduce 33%
17/03/16 22:29:51 INFO mapred.JobClient:  map 98% reduce 34%
17/03/16 22:29:54 INFO mapred.JobClient:  map 98% reduce 36%
17/03/16 22:29:57 INFO mapred.JobClient:  map 98% reduce 37%
17/03/16 22:30:00 INFO mapred.JobClient:  map 98% reduce 38%
17/03/16 22:30:03 INFO mapred.JobClient:  map 98% reduce 39%
17/03/16 22:30:06 INFO mapred.JobClient:  map 98% reduce 40%
17/03/16 22:30:09 INFO mapred.JobClient:  map 98% reduce 41%
17/03/16 22:30:10 INFO mapred.JobClient:  map 98% reduce 42%
17/03/16 22:30:13 INFO mapred.JobClient:  map 98% reduce 43%
17/03/16 22:30:14 INFO mapred.JobClient:  map 99% reduce 43%
17/03/16 22:30:15 INFO mapred.JobClient:  map 98% reduce 43%
17/03/16 22:30:16 INFO mapred.JobClient:  map 98% reduce 44%
17/03/16 22:30:21 INFO mapred.JobClient:  map 99% reduce 44%
17/03/16 22:30:22 INFO mapred.JobClient:  map 98% reduce 44%
17/03/16 22:30:30 INFO mapred.JobClient:  map 99% reduce 44%
17/03/16 22:30:31 INFO mapred.JobClient:  map 98% reduce 45%
17/03/16 22:30:40 INFO mapred.JobClient:  map 99% reduce 45%
17/03/16 22:30:41 INFO mapred.JobClient:  map 98% reduce 45%
17/03/16 22:30:44 INFO mapred.JobClient:  map 99% reduce 45%
17/03/16 22:30:45 INFO mapred.JobClient:  map 98% reduce 45%
17/03/16 22:30:46 INFO mapred.JobClient:  map 98% reduce 46%
17/03/16 22:30:48 INFO mapred.JobClient:  map 99% reduce 46%
17/03/16 22:30:51 INFO mapred.JobClient:  map 100% reduce 46%
17/03/16 22:30:58 INFO mapred.JobClient:  map 100% reduce 53%
17/03/16 22:31:00 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 22:31:01 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 22:31:03 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 22:31:06 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 22:31:07 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 22:31:09 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 22:31:12 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 22:31:13 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 22:31:15 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 22:31:16 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 22:31:19 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 22:31:21 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 22:31:22 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 22:31:24 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 22:31:25 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 22:31:28 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 22:31:30 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 22:31:31 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 22:31:33 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 22:31:37 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 22:31:39 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 22:31:42 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 22:31:45 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 22:31:46 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 22:31:48 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 22:31:51 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 22:31:54 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 22:31:55 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 22:31:58 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 22:32:01 INFO mapred.JobClient: Job complete: job_201703162224_0001
17/03/16 22:32:01 INFO mapred.JobClient: Counters: 30
17/03/16 22:32:01 INFO mapred.JobClient:   Job Counters
17/03/16 22:32:01 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 22:32:01 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=1095518
17/03/16 22:32:01 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 22:32:01 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 22:32:01 INFO mapred.JobClient:     Launched map tasks=321
17/03/16 22:32:01 INFO mapred.JobClient:     Data-local map tasks=321
17/03/16 22:32:01 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1148964
17/03/16 22:32:01 INFO mapred.JobClient:   File Input Format Counters
17/03/16 22:32:01 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 22:32:01 INFO mapred.JobClient:   File Output Format Counters
17/03/16 22:32:01 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 22:32:01 INFO mapred.JobClient:   FileSystemCounters
17/03/16 22:32:01 INFO mapred.JobClient:     FILE_BYTES_READ=94315734705
17/03/16 22:32:01 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 22:32:01 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126575106019
17/03/16 22:32:01 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 22:32:01 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 22:32:01 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 22:32:01 INFO mapred.JobClient:     Map input records=3068055
17/03/16 22:32:01 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 22:32:01 INFO mapred.JobClient:     Spilled Records=12039520
17/03/16 22:32:01 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 22:32:01 INFO mapred.JobClient:     Total committed heap usage (bytes)=49356996608
17/03/16 22:32:01 INFO mapred.JobClient:     CPU time spent (ms)=1526220
17/03/16 22:32:01 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 22:32:01 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 22:32:01 INFO mapred.JobClient:     Combine input records=0
17/03/16 22:32:01 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 22:32:01 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 22:32:01 INFO mapred.JobClient:     Combine output records=0
17/03/16 22:32:01 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52922314752
17/03/16 22:32:01 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 22:32:01 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=197335511040
17/03/16 22:32:01 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 22:32:01 UTC 2017
The job took 367 seconds.
```

## Wordcount normal with expiry interval of 30s
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar wordcount outputtext outputtextcounted
17/03/16 23:16:05 INFO input.FileInputFormat: Total input paths to process : 30
17/03/16 23:16:05 INFO util.NativeCodeLoader: Loaded the native-hadoop library
17/03/16 23:16:05 WARN snappy.LoadSnappy: Snappy native library not loaded
17/03/16 23:16:05 INFO mapred.JobClient: Running job: job_201703162256_0003
17/03/16 23:16:06 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 23:16:19 INFO mapred.JobClient:  map 1% reduce 0%
17/03/16 23:16:27 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 23:16:37 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 23:16:44 INFO mapred.JobClient:  map 4% reduce 0%
17/03/16 23:16:55 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 23:17:01 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 23:17:11 INFO mapred.JobClient:  map 6% reduce 2%
17/03/16 23:17:12 INFO mapred.JobClient:  map 7% reduce 2%
17/03/16 23:17:19 INFO mapred.JobClient:  map 8% reduce 2%
17/03/16 23:17:29 INFO mapred.JobClient:  map 9% reduce 2%
17/03/16 23:17:37 INFO mapred.JobClient:  map 10% reduce 2%
17/03/16 23:17:44 INFO mapred.JobClient:  map 11% reduce 2%
17/03/16 23:17:48 INFO mapred.JobClient:  map 11% reduce 3%
17/03/16 23:17:54 INFO mapred.JobClient:  map 12% reduce 3%
17/03/16 23:18:01 INFO mapred.JobClient:  map 13% reduce 3%
17/03/16 23:18:09 INFO mapred.JobClient:  map 13% reduce 4%
17/03/16 23:18:12 INFO mapred.JobClient:  map 14% reduce 4%
17/03/16 23:18:19 INFO mapred.JobClient:  map 15% reduce 4%
17/03/16 23:18:29 INFO mapred.JobClient:  map 16% reduce 4%
17/03/16 23:18:33 INFO mapred.JobClient:  map 16% reduce 5%
17/03/16 23:18:35 INFO mapred.JobClient:  map 17% reduce 5%
17/03/16 23:18:47 INFO mapred.JobClient:  map 18% reduce 5%
17/03/16 23:18:54 INFO mapred.JobClient:  map 19% reduce 5%
17/03/16 23:19:03 INFO mapred.JobClient:  map 19% reduce 6%
17/03/16 23:19:04 INFO mapred.JobClient:  map 20% reduce 6%
17/03/16 23:19:13 INFO mapred.JobClient:  map 21% reduce 6%
17/03/16 23:19:20 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 23:19:24 INFO mapred.JobClient:  map 22% reduce 7%
17/03/16 23:19:30 INFO mapred.JobClient:  map 23% reduce 7%
17/03/16 23:19:37 INFO mapred.JobClient:  map 24% reduce 7%
17/03/16 23:19:48 INFO mapred.JobClient:  map 25% reduce 8%
17/03/16 23:19:54 INFO mapred.JobClient:  map 26% reduce 8%
17/03/16 23:20:07 INFO mapred.JobClient:  map 27% reduce 8%
17/03/16 23:20:12 INFO mapred.JobClient:  map 28% reduce 8%
17/03/16 23:20:18 INFO mapred.JobClient:  map 28% reduce 9%
17/03/16 23:20:22 INFO mapred.JobClient:  map 29% reduce 9%
17/03/16 23:20:29 INFO mapred.JobClient:  map 30% reduce 9%
17/03/16 23:20:38 INFO mapred.JobClient:  map 31% reduce 9%
17/03/16 23:20:45 INFO mapred.JobClient:  map 31% reduce 10%
17/03/16 23:20:47 INFO mapred.JobClient:  map 32% reduce 10%
17/03/16 23:20:55 INFO mapred.JobClient:  map 33% reduce 10%
17/03/16 23:21:05 INFO mapred.JobClient:  map 34% reduce 10%
17/03/16 23:21:10 INFO mapred.JobClient:  map 34% reduce 11%
17/03/16 23:21:12 INFO mapred.JobClient:  map 35% reduce 11%
17/03/16 23:21:22 INFO mapred.JobClient:  map 36% reduce 11%
17/03/16 23:21:30 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 23:21:38 INFO mapred.JobClient:  map 38% reduce 11%
17/03/16 23:21:39 INFO mapred.JobClient:  map 38% reduce 12%
17/03/16 23:21:46 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 23:21:55 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 23:22:01 INFO mapred.JobClient:  map 40% reduce 13%
17/03/16 23:22:03 INFO mapred.JobClient:  map 41% reduce 13%
17/03/16 23:22:11 INFO mapred.JobClient:  map 42% reduce 13%
17/03/16 23:22:21 INFO mapred.JobClient:  map 43% reduce 13%
17/03/16 23:22:25 INFO mapred.JobClient:  map 43% reduce 14%
17/03/16 23:22:29 INFO mapred.JobClient:  map 44% reduce 14%
17/03/16 23:22:39 INFO mapred.JobClient:  map 45% reduce 14%
17/03/16 23:22:45 INFO mapred.JobClient:  map 46% reduce 14%
17/03/16 23:22:55 INFO mapred.JobClient:  map 47% reduce 15%
17/03/16 23:23:01 INFO mapred.JobClient:  map 48% reduce 15%
17/03/16 23:23:10 INFO mapred.JobClient:  map 49% reduce 15%
17/03/16 23:23:13 INFO mapred.JobClient:  map 49% reduce 16%
17/03/16 23:23:20 INFO mapred.JobClient:  map 50% reduce 16%
17/03/16 23:23:27 INFO mapred.JobClient:  map 51% reduce 16%
17/03/16 23:23:36 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 23:23:37 INFO mapred.JobClient:  map 52% reduce 17%
17/03/16 23:23:44 INFO mapred.JobClient:  map 53% reduce 17%
17/03/16 23:23:54 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 23:24:01 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 23:24:10 INFO mapred.JobClient:  map 55% reduce 18%
17/03/16 23:24:12 INFO mapred.JobClient:  map 56% reduce 18%
17/03/16 23:24:18 INFO mapred.JobClient:  map 57% reduce 18%
17/03/16 23:24:29 INFO mapred.JobClient:  map 58% reduce 18%
17/03/16 23:24:31 INFO mapred.JobClient:  map 58% reduce 19%
17/03/16 23:24:36 INFO mapred.JobClient:  map 59% reduce 19%
17/03/16 23:24:44 INFO mapred.JobClient:  map 60% reduce 19%
17/03/16 23:24:54 INFO mapred.JobClient:  map 61% reduce 19%
17/03/16 23:25:02 INFO mapred.JobClient:  map 62% reduce 20%
17/03/16 23:25:11 INFO mapred.JobClient:  map 63% reduce 20%
17/03/16 23:25:19 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 23:25:29 INFO mapred.JobClient:  map 65% reduce 20%
17/03/16 23:25:32 INFO mapred.JobClient:  map 65% reduce 21%
17/03/16 23:25:37 INFO mapred.JobClient:  map 66% reduce 21%
17/03/16 23:25:46 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 23:25:47 INFO mapred.JobClient:  map 67% reduce 22%
17/03/16 23:25:53 INFO mapred.JobClient:  map 68% reduce 22%
17/03/16 23:26:02 INFO mapred.JobClient:  map 69% reduce 22%
17/03/16 23:26:11 INFO mapred.JobClient:  map 70% reduce 22%
17/03/16 23:26:18 INFO mapred.JobClient:  map 70% reduce 23%
17/03/16 23:26:19 INFO mapred.JobClient:  map 71% reduce 23%
17/03/16 23:26:28 INFO mapred.JobClient:  map 72% reduce 23%
17/03/16 23:26:36 INFO mapred.JobClient:  map 73% reduce 23%
17/03/16 23:26:46 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 23:26:48 INFO mapred.JobClient:  map 74% reduce 24%
17/03/16 23:26:53 INFO mapred.JobClient:  map 75% reduce 24%
17/03/16 23:27:03 INFO mapred.JobClient:  map 76% reduce 24%
17/03/16 23:27:09 INFO mapred.JobClient:  map 76% reduce 25%
17/03/16 23:27:11 INFO mapred.JobClient:  map 77% reduce 25%
17/03/16 23:27:20 INFO mapred.JobClient:  map 78% reduce 25%
17/03/16 23:27:29 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 23:27:33 INFO mapred.JobClient:  map 79% reduce 26%
17/03/16 23:27:37 INFO mapred.JobClient:  map 80% reduce 26%
17/03/16 23:27:46 INFO mapred.JobClient:  map 81% reduce 26%
17/03/16 23:27:53 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 23:27:54 INFO mapred.JobClient:  map 82% reduce 27%
17/03/16 23:28:02 INFO mapred.JobClient:  map 83% reduce 27%
17/03/16 23:28:11 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 23:28:20 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 23:28:24 INFO mapred.JobClient:  map 85% reduce 28%
17/03/16 23:28:28 INFO mapred.JobClient:  map 86% reduce 28%
17/03/16 23:28:37 INFO mapred.JobClient:  map 87% reduce 28%
17/03/16 23:28:45 INFO mapred.JobClient:  map 88% reduce 29%
17/03/16 23:28:51 INFO mapred.JobClient:  map 89% reduce 29%
17/03/16 23:28:54 INFO mapred.JobClient:  map 90% reduce 29%
17/03/16 23:28:58 INFO mapred.JobClient:  map 91% reduce 29%
17/03/16 23:29:00 INFO mapred.JobClient:  map 91% reduce 30%
17/03/16 23:29:01 INFO mapred.JobClient:  map 92% reduce 30%
17/03/16 23:29:05 INFO mapred.JobClient:  map 93% reduce 30%
17/03/16 23:29:06 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 23:29:10 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 23:29:12 INFO mapred.JobClient:  map 96% reduce 31%
17/03/16 23:29:15 INFO mapred.JobClient:  map 97% reduce 32%
17/03/16 23:29:18 INFO mapred.JobClient:  map 98% reduce 32%
17/03/16 23:29:21 INFO mapred.JobClient:  map 99% reduce 32%
17/03/16 23:29:23 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 23:29:30 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 23:29:33 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 23:29:36 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 23:29:39 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 23:29:42 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 23:29:45 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 23:29:48 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 23:29:51 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 23:29:54 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 23:29:58 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 23:30:00 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 23:30:01 INFO mapred.JobClient: Job complete: job_201703162256_0003
17/03/16 23:30:01 INFO mapred.JobClient: Counters: 29
17/03/16 23:30:01 INFO mapred.JobClient:   Job Counters
17/03/16 23:30:01 INFO mapred.JobClient:     Launched reduce tasks=1
17/03/16 23:30:01 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=4714216
17/03/16 23:30:01 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 23:30:01 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 23:30:01 INFO mapred.JobClient:     Launched map tasks=273
17/03/16 23:30:01 INFO mapred.JobClient:     Data-local map tasks=273
17/03/16 23:30:01 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=776220
17/03/16 23:30:01 INFO mapred.JobClient:   File Output Format Counters
17/03/16 23:30:01 INFO mapred.JobClient:     Bytes Written=905243269
17/03/16 23:30:01 INFO mapred.JobClient:   FileSystemCounters
17/03/16 23:30:01 INFO mapred.JobClient:     FILE_BYTES_READ=7723792581
17/03/16 23:30:01 INFO mapred.JobClient:     HDFS_BYTES_READ=33076469383
17/03/16 23:30:01 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=9842249571
17/03/16 23:30:01 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=905243269
17/03/16 23:30:01 INFO mapred.JobClient:   File Input Format Counters
17/03/16 23:30:01 INFO mapred.JobClient:     Bytes Read=33076431583
17/03/16 23:30:01 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 23:30:01 INFO mapred.JobClient:     Map output materialized bytes=2104789579
17/03/16 23:30:01 INFO mapred.JobClient:     Map input records=3083933
17/03/16 23:30:01 INFO mapred.JobClient:     Reduce shuffle bytes=2104789579
17/03/16 23:30:01 INFO mapred.JobClient:     Spilled Records=331737342
17/03/16 23:30:01 INFO mapred.JobClient:     Map output bytes=45668578968
17/03/16 23:30:01 INFO mapred.JobClient:     Total committed heap usage (bytes)=51630309376
17/03/16 23:30:01 INFO mapred.JobClient:     CPU time spent (ms)=6500160
17/03/16 23:30:01 INFO mapred.JobClient:     Combine input records=3199108188
17/03/16 23:30:01 INFO mapred.JobClient:     SPLIT_RAW_BYTES=37800
17/03/16 23:30:01 INFO mapred.JobClient:     Reduce input records=44636370
17/03/16 23:30:01 INFO mapred.JobClient:     Reduce input groups=25104128
17/03/16 23:30:01 INFO mapred.JobClient:     Combine output records=213527379
17/03/16 23:30:01 INFO mapred.JobClient:     Physical memory (bytes) snapshot=61105635328
17/03/16 23:30:01 INFO mapred.JobClient:     Reduce output records=25104128
17/03/16 23:30:01 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=216050573312
17/03/16 23:30:01 INFO mapred.JobClient:     Map output records=3030217179
```

## Wordcount normal with expiry interval of 30s and slowstart 0.05
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar wordcount outputtext outputtextcounted
17/03/16 23:34:50 INFO input.FileInputFormat: Total input paths to process : 30
17/03/16 23:34:50 INFO util.NativeCodeLoader: Loaded the native-hadoop library
17/03/16 23:34:50 WARN snappy.LoadSnappy: Snappy native library not loaded
17/03/16 23:34:51 INFO mapred.JobClient: Running job: job_201703162334_0001
17/03/16 23:34:52 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 23:35:05 INFO mapred.JobClient:  map 1% reduce 0%
17/03/16 23:35:12 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 23:35:24 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 23:35:30 INFO mapred.JobClient:  map 4% reduce 0%
17/03/16 23:35:40 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 23:35:48 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 23:35:58 INFO mapred.JobClient:  map 6% reduce 2%
17/03/16 23:35:59 INFO mapred.JobClient:  map 7% reduce 2%
17/03/16 23:36:05 INFO mapred.JobClient:  map 8% reduce 2%
17/03/16 23:36:17 INFO mapred.JobClient:  map 9% reduce 2%
17/03/16 23:36:23 INFO mapred.JobClient:  map 10% reduce 2%
17/03/16 23:36:29 INFO mapred.JobClient:  map 11% reduce 2%
17/03/16 23:36:35 INFO mapred.JobClient:  map 11% reduce 3%
17/03/16 23:36:39 INFO mapred.JobClient:  map 12% reduce 3%
17/03/16 23:36:46 INFO mapred.JobClient:  map 13% reduce 3%
17/03/16 23:36:56 INFO mapred.JobClient:  map 13% reduce 4%
17/03/16 23:36:57 INFO mapred.JobClient:  map 14% reduce 4%
17/03/16 23:37:04 INFO mapred.JobClient:  map 15% reduce 4%
17/03/16 23:37:11 INFO mapred.JobClient:  map 15% reduce 5%
17/03/16 23:37:14 INFO mapred.JobClient:  map 16% reduce 5%
17/03/16 23:37:22 INFO mapred.JobClient:  map 17% reduce 5%
17/03/16 23:37:33 INFO mapred.JobClient:  map 18% reduce 5%
17/03/16 23:37:39 INFO mapred.JobClient:  map 19% reduce 5%
17/03/16 23:37:46 INFO mapred.JobClient:  map 20% reduce 5%
17/03/16 23:37:50 INFO mapred.JobClient:  map 20% reduce 6%
17/03/16 23:37:56 INFO mapred.JobClient:  map 21% reduce 6%
17/03/16 23:38:03 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 23:38:12 INFO mapred.JobClient:  map 22% reduce 7%
17/03/16 23:38:14 INFO mapred.JobClient:  map 23% reduce 7%
17/03/16 23:38:21 INFO mapred.JobClient:  map 24% reduce 7%
17/03/16 23:38:26 INFO mapred.JobClient:  map 24% reduce 8%
17/03/16 23:38:31 INFO mapred.JobClient:  map 25% reduce 8%
17/03/16 23:38:38 INFO mapred.JobClient:  map 26% reduce 8%
17/03/16 23:38:49 INFO mapred.JobClient:  map 27% reduce 8%
17/03/16 23:38:55 INFO mapred.JobClient:  map 28% reduce 8%
17/03/16 23:39:06 INFO mapred.JobClient:  map 28% reduce 9%
17/03/16 23:39:07 INFO mapred.JobClient:  map 29% reduce 9%
17/03/16 23:39:13 INFO mapred.JobClient:  map 30% reduce 9%
17/03/16 23:39:20 INFO mapred.JobClient:  map 31% reduce 9%
17/03/16 23:39:27 INFO mapred.JobClient:  map 31% reduce 10%
17/03/16 23:39:30 INFO mapred.JobClient:  map 32% reduce 10%
17/03/16 23:39:37 INFO mapred.JobClient:  map 33% reduce 10%
17/03/16 23:39:48 INFO mapred.JobClient:  map 34% reduce 10%
17/03/16 23:39:51 INFO mapred.JobClient:  map 34% reduce 11%
17/03/16 23:39:54 INFO mapred.JobClient:  map 35% reduce 11%
17/03/16 23:40:06 INFO mapred.JobClient:  map 36% reduce 11%
17/03/16 23:40:12 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 23:40:23 INFO mapred.JobClient:  map 38% reduce 11%
17/03/16 23:40:27 INFO mapred.JobClient:  map 38% reduce 12%
17/03/16 23:40:29 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 23:40:39 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 23:40:42 INFO mapred.JobClient:  map 40% reduce 13%
17/03/16 23:40:47 INFO mapred.JobClient:  map 41% reduce 13%
17/03/16 23:40:54 INFO mapred.JobClient:  map 42% reduce 13%
17/03/16 23:41:05 INFO mapred.JobClient:  map 43% reduce 13%
17/03/16 23:41:06 INFO mapred.JobClient:  map 43% reduce 14%
17/03/16 23:41:11 INFO mapred.JobClient:  map 44% reduce 14%
17/03/16 23:41:23 INFO mapred.JobClient:  map 45% reduce 14%
17/03/16 23:41:30 INFO mapred.JobClient:  map 46% reduce 14%
17/03/16 23:41:41 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 23:41:42 INFO mapred.JobClient:  map 47% reduce 15%
17/03/16 23:41:47 INFO mapred.JobClient:  map 48% reduce 15%
17/03/16 23:41:58 INFO mapred.JobClient:  map 49% reduce 15%
17/03/16 23:42:03 INFO mapred.JobClient:  map 49% reduce 16%
17/03/16 23:42:05 INFO mapred.JobClient:  map 50% reduce 16%
17/03/16 23:42:12 INFO mapred.JobClient:  map 51% reduce 16%
17/03/16 23:42:18 INFO mapred.JobClient:  map 51% reduce 17%
17/03/16 23:42:22 INFO mapred.JobClient:  map 52% reduce 17%
17/03/16 23:42:29 INFO mapred.JobClient:  map 53% reduce 17%
17/03/16 23:42:39 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 23:42:45 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 23:42:57 INFO mapred.JobClient:  map 56% reduce 18%
17/03/16 23:43:03 INFO mapred.JobClient:  map 57% reduce 18%
17/03/16 23:43:16 INFO mapred.JobClient:  map 58% reduce 18%
17/03/16 23:43:19 INFO mapred.JobClient:  map 58% reduce 19%
17/03/16 23:43:22 INFO mapred.JobClient:  map 59% reduce 19%
17/03/16 23:43:32 INFO mapred.JobClient:  map 60% reduce 19%
17/03/16 23:43:40 INFO mapred.JobClient:  map 61% reduce 19%
17/03/16 23:43:48 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 23:43:50 INFO mapred.JobClient:  map 62% reduce 20%
17/03/16 23:44:00 INFO mapred.JobClient:  map 63% reduce 20%
17/03/16 23:44:06 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 23:44:13 INFO mapred.JobClient:  map 64% reduce 21%
17/03/16 23:44:17 INFO mapred.JobClient:  map 65% reduce 21%
17/03/16 23:44:23 INFO mapred.JobClient:  map 66% reduce 21%
17/03/16 23:44:33 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 23:44:35 INFO mapred.JobClient:  map 67% reduce 22%
17/03/16 23:44:40 INFO mapred.JobClient:  map 68% reduce 22%
17/03/16 23:44:52 INFO mapred.JobClient:  map 69% reduce 22%
17/03/16 23:44:58 INFO mapred.JobClient:  map 70% reduce 22%
17/03/16 23:45:05 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 23:45:14 INFO mapred.JobClient:  map 71% reduce 23%
17/03/16 23:45:15 INFO mapred.JobClient:  map 72% reduce 23%
17/03/16 23:45:22 INFO mapred.JobClient:  map 73% reduce 23%
17/03/16 23:45:33 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 23:45:35 INFO mapred.JobClient:  map 74% reduce 24%
17/03/16 23:45:40 INFO mapred.JobClient:  map 75% reduce 24%
17/03/16 23:45:50 INFO mapred.JobClient:  map 76% reduce 25%
17/03/16 23:45:57 INFO mapred.JobClient:  map 77% reduce 25%
17/03/16 23:46:08 INFO mapred.JobClient:  map 78% reduce 25%
17/03/16 23:46:14 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 23:46:20 INFO mapred.JobClient:  map 79% reduce 26%
17/03/16 23:46:23 INFO mapred.JobClient:  map 80% reduce 26%
17/03/16 23:46:32 INFO mapred.JobClient:  map 81% reduce 26%
17/03/16 23:46:39 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 23:46:49 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 23:46:50 INFO mapred.JobClient:  map 83% reduce 27%
17/03/16 23:46:56 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 23:47:05 INFO mapred.JobClient:  map 84% reduce 28%
17/03/16 23:47:07 INFO mapred.JobClient:  map 85% reduce 28%
17/03/16 23:47:13 INFO mapred.JobClient:  map 86% reduce 28%
17/03/16 23:47:24 INFO mapred.JobClient:  map 87% reduce 28%
17/03/16 23:47:31 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 23:47:35 INFO mapred.JobClient:  map 88% reduce 29%
17/03/16 23:47:39 INFO mapred.JobClient:  map 89% reduce 29%
17/03/16 23:47:41 INFO mapred.JobClient:  map 90% reduce 29%
17/03/16 23:47:44 INFO mapred.JobClient:  map 91% reduce 29%
17/03/16 23:47:47 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 23:47:50 INFO mapred.JobClient:  map 93% reduce 30%
17/03/16 23:47:52 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 23:47:56 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 23:47:57 INFO mapred.JobClient:  map 96% reduce 30%
17/03/16 23:47:59 INFO mapred.JobClient:  map 96% reduce 31%
17/03/16 23:48:00 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 23:48:02 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 23:48:05 INFO mapred.JobClient:  map 98% reduce 32%
17/03/16 23:48:07 INFO mapred.JobClient:  map 99% reduce 32%
17/03/16 23:48:08 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 23:48:15 INFO mapred.JobClient:  map 100% reduce 33%
17/03/16 23:48:18 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 23:48:21 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 23:48:24 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 23:48:27 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 23:48:30 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 23:48:33 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 23:48:36 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 23:48:39 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 23:48:42 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 23:48:45 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 23:48:47 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 23:48:47 INFO mapred.JobClient: Job complete: job_201703162334_0001
17/03/16 23:48:47 INFO mapred.JobClient: Counters: 29
17/03/16 23:48:47 INFO mapred.JobClient:   Job Counters
17/03/16 23:48:47 INFO mapred.JobClient:     Launched reduce tasks=1
17/03/16 23:48:47 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=4708771
17/03/16 23:48:47 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 23:48:47 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 23:48:47 INFO mapred.JobClient:     Launched map tasks=274
17/03/16 23:48:47 INFO mapred.JobClient:     Data-local map tasks=274
17/03/16 23:48:47 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=775291
17/03/16 23:48:47 INFO mapred.JobClient:   File Output Format Counters
17/03/16 23:48:47 INFO mapred.JobClient:     Bytes Written=905243269
17/03/16 23:48:47 INFO mapred.JobClient:   FileSystemCounters
17/03/16 23:48:47 INFO mapred.JobClient:     FILE_BYTES_READ=7723882535
17/03/16 23:48:47 INFO mapred.JobClient:     HDFS_BYTES_READ=33076469383
17/03/16 23:48:47 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=9842339525
17/03/16 23:48:47 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=905243269
17/03/16 23:48:47 INFO mapred.JobClient:   File Input Format Counters
17/03/16 23:48:47 INFO mapred.JobClient:     Bytes Read=33076431583
17/03/16 23:48:47 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 23:48:47 INFO mapred.JobClient:     Map output materialized bytes=2104789579
17/03/16 23:48:47 INFO mapred.JobClient:     Map input records=3083933
17/03/16 23:48:47 INFO mapred.JobClient:     Reduce shuffle bytes=2104789579
17/03/16 23:48:47 INFO mapred.JobClient:     Spilled Records=331696782
17/03/16 23:48:47 INFO mapred.JobClient:     Map output bytes=45668578968
17/03/16 23:48:47 INFO mapred.JobClient:     Total committed heap usage (bytes)=51973718016
17/03/16 23:48:47 INFO mapred.JobClient:     CPU time spent (ms)=6490850
17/03/16 23:48:47 INFO mapred.JobClient:     Combine input records=3199186381
17/03/16 23:48:47 INFO mapred.JobClient:     SPLIT_RAW_BYTES=37800
17/03/16 23:48:47 INFO mapred.JobClient:     Reduce input records=44643358
17/03/16 23:48:47 INFO mapred.JobClient:     Reduce input groups=25104128
17/03/16 23:48:47 INFO mapred.JobClient:     Combine output records=213612560
17/03/16 23:48:47 INFO mapred.JobClient:     Physical memory (bytes) snapshot=61459357696
17/03/16 23:48:47 INFO mapred.JobClient:     Reduce output records=25104128
17/03/16 23:48:47 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=216357117952
17/03/16 23:48:47 INFO mapred.JobClient:     Map output records=3030217179
```

## Wordcount normal with expiry interval of 30s and slowstart 0.5
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar wordcount outputtext outputtextcounted
17/03/17 00:50:19 INFO input.FileInputFormat: Total input paths to process : 40
17/03/17 00:50:19 INFO util.NativeCodeLoader: Loaded the native-hadoop library
17/03/17 00:50:19 WARN snappy.LoadSnappy: Snappy native library not loaded
17/03/17 00:50:20 INFO mapred.JobClient: Running job: job_201703170049_0001
17/03/17 00:50:21 INFO mapred.JobClient:  map 0% reduce 0%
17/03/17 00:50:34 INFO mapred.JobClient:  map 1% reduce 0%
17/03/17 00:50:41 INFO mapred.JobClient:  map 2% reduce 0%
17/03/17 00:50:52 INFO mapred.JobClient:  map 3% reduce 0%
17/03/17 00:50:59 INFO mapred.JobClient:  map 4% reduce 0%
17/03/17 00:51:09 INFO mapred.JobClient:  map 5% reduce 0%
17/03/17 00:51:17 INFO mapred.JobClient:  map 6% reduce 0%
17/03/17 00:51:27 INFO mapred.JobClient:  map 7% reduce 0%
17/03/17 00:51:33 INFO mapred.JobClient:  map 8% reduce 0%
17/03/17 00:51:46 INFO mapred.JobClient:  map 9% reduce 0%
17/03/17 00:51:50 INFO mapred.JobClient:  map 10% reduce 0%
17/03/17 00:51:58 INFO mapred.JobClient:  map 11% reduce 0%
17/03/17 00:52:08 INFO mapred.JobClient:  map 12% reduce 0%
17/03/17 00:52:15 INFO mapred.JobClient:  map 13% reduce 0%
17/03/17 00:52:26 INFO mapred.JobClient:  map 14% reduce 0%
17/03/17 00:52:33 INFO mapred.JobClient:  map 15% reduce 0%
17/03/17 00:52:44 INFO mapred.JobClient:  map 16% reduce 0%
17/03/17 00:52:50 INFO mapred.JobClient:  map 17% reduce 0%
17/03/17 00:53:01 INFO mapred.JobClient:  map 18% reduce 0%
17/03/17 00:53:07 INFO mapred.JobClient:  map 19% reduce 0%
17/03/17 00:53:19 INFO mapred.JobClient:  map 20% reduce 0%
17/03/17 00:53:26 INFO mapred.JobClient:  map 21% reduce 0%
17/03/17 00:53:34 INFO mapred.JobClient:  map 22% reduce 0%
17/03/17 00:53:44 INFO mapred.JobClient:  map 23% reduce 0%
17/03/17 00:53:51 INFO mapred.JobClient:  map 24% reduce 0%
17/03/17 00:54:01 INFO mapred.JobClient:  map 25% reduce 0%
17/03/17 00:54:08 INFO mapred.JobClient:  map 26% reduce 0%
17/03/17 00:54:17 INFO mapred.JobClient:  map 27% reduce 0%
17/03/17 00:54:24 INFO mapred.JobClient:  map 28% reduce 0%
17/03/17 00:54:35 INFO mapred.JobClient:  map 29% reduce 0%
17/03/17 00:54:43 INFO mapred.JobClient:  map 30% reduce 0%
17/03/17 00:54:51 INFO mapred.JobClient:  map 31% reduce 0%
17/03/17 00:55:00 INFO mapred.JobClient:  map 32% reduce 0%
17/03/17 00:55:09 INFO mapred.JobClient:  map 33% reduce 0%
17/03/17 00:55:17 INFO mapred.JobClient:  map 34% reduce 0%
17/03/17 00:55:26 INFO mapred.JobClient:  map 35% reduce 0%
17/03/17 00:55:34 INFO mapred.JobClient:  map 36% reduce 0%
17/03/17 00:55:45 INFO mapred.JobClient:  map 37% reduce 0%
17/03/17 00:55:52 INFO mapred.JobClient:  map 38% reduce 0%
17/03/17 00:56:01 INFO mapred.JobClient:  map 39% reduce 0%
17/03/17 00:56:10 INFO mapred.JobClient:  map 40% reduce 0%
17/03/17 00:56:20 INFO mapred.JobClient:  map 41% reduce 0%
17/03/17 00:56:27 INFO mapred.JobClient:  map 42% reduce 0%
17/03/17 00:56:36 INFO mapred.JobClient:  map 43% reduce 0%
17/03/17 00:56:44 INFO mapred.JobClient:  map 44% reduce 0%
17/03/17 00:56:53 INFO mapred.JobClient:  map 45% reduce 0%
17/03/17 00:57:01 INFO mapred.JobClient:  map 46% reduce 0%
17/03/17 00:57:09 INFO mapred.JobClient:  map 47% reduce 0%
17/03/17 00:57:19 INFO mapred.JobClient:  map 48% reduce 0%
17/03/17 00:57:28 INFO mapred.JobClient:  map 49% reduce 0%
17/03/17 00:57:36 INFO mapred.JobClient:  map 50% reduce 0%
17/03/17 00:57:46 INFO mapred.JobClient:  map 51% reduce 1%
17/03/17 00:57:49 INFO mapred.JobClient:  map 51% reduce 2%
17/03/17 00:57:52 INFO mapred.JobClient:  map 51% reduce 4%
17/03/17 00:57:53 INFO mapred.JobClient:  map 52% reduce 4%
17/03/17 00:57:56 INFO mapred.JobClient:  map 52% reduce 6%
17/03/17 00:57:59 INFO mapred.JobClient:  map 52% reduce 7%
17/03/17 00:58:02 INFO mapred.JobClient:  map 52% reduce 9%
17/03/17 00:58:03 INFO mapred.JobClient:  map 53% reduce 9%
17/03/17 00:58:05 INFO mapred.JobClient:  map 53% reduce 10%
17/03/17 00:58:08 INFO mapred.JobClient:  map 53% reduce 11%
17/03/17 00:58:10 INFO mapred.JobClient:  map 54% reduce 11%
17/03/17 00:58:12 INFO mapred.JobClient:  map 54% reduce 0%
17/03/17 00:58:12 INFO mapred.JobClient: Task Id : attempt_201703170049_0001_r_000000_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at sun.net.www.http.ChunkedInputStream.processRaw(ChunkedInputStream.java:363)
        at sun.net.www.http.ChunkedInputStream.readAheadNonBlocking(ChunkedInputStream.java:520)
        at sun.net.www.http.ChunkedInputStream.readAhead(ChunkedInputStream.java:611)
        at sun.net.www.http.ChunkedInputStream.hurry(ChunkedInputStream.java:768)
        at sun.net.www.http.ChunkedInputStream.closeUnderlying(ChunkedInputStream.java:221)
        at sun.net.www.http.ChunkedInputStream.close(ChunkedInputStream.java:749)
        at java.io.FilterInputStream.close(FilterInputStream.java:181)
        at sun.net.www.protocol.http.HttpURLConnection$HttpInputStream.close(HttpURLConnection.java:3137)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$ShuffleRamManager.reserve(ReduceTask.java:1132)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1671)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/17 00:58:20 INFO mapred.JobClient:  map 55% reduce 1%
17/03/17 00:58:23 INFO mapred.JobClient:  map 55% reduce 2%
17/03/17 00:58:27 INFO mapred.JobClient:  map 56% reduce 4%
17/03/17 00:58:30 INFO mapred.JobClient:  map 56% reduce 5%
17/03/17 00:58:33 INFO mapred.JobClient:  map 56% reduce 7%
17/03/17 00:58:36 INFO mapred.JobClient:  map 56% reduce 8%
17/03/17 00:58:37 INFO mapred.JobClient:  map 57% reduce 8%
17/03/17 00:58:39 INFO mapred.JobClient:  map 57% reduce 10%
17/03/17 00:58:42 INFO mapred.JobClient:  map 57% reduce 11%
17/03/17 00:58:45 INFO mapred.JobClient:  map 58% reduce 12%
17/03/17 00:58:49 INFO mapred.JobClient:  map 58% reduce 14%
17/03/17 00:58:52 INFO mapred.JobClient:  map 58% reduce 16%
17/03/17 00:58:55 INFO mapred.JobClient:  map 58% reduce 17%
17/03/17 00:58:56 INFO mapred.JobClient:  map 59% reduce 17%
17/03/17 00:58:58 INFO mapred.JobClient:  map 59% reduce 18%
17/03/17 00:59:01 INFO mapred.JobClient:  map 59% reduce 19%
17/03/17 00:59:03 INFO mapred.JobClient:  map 60% reduce 19%
17/03/17 00:59:12 INFO mapred.JobClient:  map 61% reduce 19%
17/03/17 00:59:16 INFO mapred.JobClient:  map 61% reduce 20%
17/03/17 00:59:21 INFO mapred.JobClient:  map 62% reduce 20%
17/03/17 00:59:28 INFO mapred.JobClient:  map 63% reduce 20%
17/03/17 00:59:38 INFO mapred.JobClient:  map 64% reduce 20%
17/03/17 00:59:40 INFO mapred.JobClient:  map 64% reduce 21%
17/03/17 00:59:45 INFO mapred.JobClient:  map 65% reduce 21%
17/03/17 00:59:55 INFO mapred.JobClient:  map 66% reduce 21%
17/03/17 01:00:03 INFO mapred.JobClient:  map 67% reduce 21%
17/03/17 01:00:10 INFO mapred.JobClient:  map 67% reduce 22%
17/03/17 01:00:14 INFO mapred.JobClient:  map 68% reduce 22%
17/03/17 01:00:20 INFO mapred.JobClient:  map 69% reduce 22%
17/03/17 01:00:31 INFO mapred.JobClient:  map 70% reduce 22%
17/03/17 01:00:39 INFO mapred.JobClient:  map 70% reduce 23%
17/03/17 01:00:41 INFO mapred.JobClient:  map 71% reduce 23%
17/03/17 01:00:50 INFO mapred.JobClient:  map 72% reduce 23%
17/03/17 01:00:57 INFO mapred.JobClient:  map 73% reduce 23%
17/03/17 01:01:03 INFO mapred.JobClient:  map 73% reduce 24%
17/03/17 01:01:04 INFO mapred.JobClient:  map 74% reduce 24%
17/03/17 01:01:15 INFO mapred.JobClient:  map 75% reduce 24%
17/03/17 01:01:22 INFO mapred.JobClient:  map 76% reduce 24%
17/03/17 01:01:24 INFO mapred.JobClient:  map 76% reduce 25%
17/03/17 01:01:32 INFO mapred.JobClient:  map 77% reduce 25%
17/03/17 01:01:40 INFO mapred.JobClient:  map 78% reduce 25%
17/03/17 01:01:49 INFO mapred.JobClient:  map 79% reduce 25%
17/03/17 01:01:54 INFO mapred.JobClient:  map 79% reduce 26%
17/03/17 01:01:58 INFO mapred.JobClient:  map 80% reduce 26%
17/03/17 01:02:06 INFO mapred.JobClient:  map 81% reduce 26%
17/03/17 01:02:15 INFO mapred.JobClient:  map 81% reduce 27%
17/03/17 01:02:16 INFO mapred.JobClient:  map 82% reduce 27%
17/03/17 01:02:23 INFO mapred.JobClient:  map 83% reduce 27%
17/03/17 01:02:32 INFO mapred.JobClient:  map 84% reduce 27%
17/03/17 01:02:41 INFO mapred.JobClient:  map 85% reduce 27%
17/03/17 01:02:45 INFO mapred.JobClient:  map 85% reduce 28%
17/03/17 01:02:51 INFO mapred.JobClient:  map 86% reduce 28%
17/03/17 01:02:58 INFO mapred.JobClient:  map 87% reduce 28%
17/03/17 01:03:08 INFO mapred.JobClient:  map 88% reduce 28%
17/03/17 01:03:13 INFO mapred.JobClient:  map 89% reduce 28%
17/03/17 01:03:15 INFO mapred.JobClient:  map 89% reduce 29%
17/03/17 01:03:16 INFO mapred.JobClient:  map 90% reduce 29%
17/03/17 01:03:20 INFO mapred.JobClient:  map 91% reduce 29%
17/03/17 01:03:24 INFO mapred.JobClient:  map 92% reduce 30%
17/03/17 01:03:25 INFO mapred.JobClient:  map 93% reduce 30%
17/03/17 01:03:30 INFO mapred.JobClient:  map 94% reduce 31%
17/03/17 01:03:31 INFO mapred.JobClient:  map 95% reduce 31%
17/03/17 01:03:36 INFO mapred.JobClient:  map 96% reduce 31%
17/03/17 01:03:37 INFO mapred.JobClient:  map 97% reduce 31%
17/03/17 01:03:39 INFO mapred.JobClient:  map 98% reduce 31%
17/03/17 01:03:43 INFO mapred.JobClient:  map 99% reduce 31%
17/03/17 01:03:44 INFO mapred.JobClient:  map 100% reduce 31%
17/03/17 01:03:46 INFO mapred.JobClient:  map 100% reduce 33%
17/03/17 01:04:01 INFO mapred.JobClient:  map 100% reduce 68%
17/03/17 01:04:03 INFO mapred.JobClient:  map 100% reduce 70%
17/03/17 01:04:06 INFO mapred.JobClient:  map 100% reduce 72%
17/03/17 01:04:09 INFO mapred.JobClient:  map 100% reduce 74%
17/03/17 01:04:12 INFO mapred.JobClient:  map 100% reduce 76%
17/03/17 01:04:15 INFO mapred.JobClient:  map 100% reduce 78%
17/03/17 01:04:18 INFO mapred.JobClient:  map 100% reduce 81%
17/03/17 01:04:21 INFO mapred.JobClient:  map 100% reduce 84%
17/03/17 01:04:25 INFO mapred.JobClient:  map 100% reduce 87%
17/03/17 01:04:28 INFO mapred.JobClient:  map 100% reduce 90%
17/03/17 01:04:31 INFO mapred.JobClient:  map 100% reduce 93%
17/03/17 01:04:34 INFO mapred.JobClient:  map 100% reduce 96%
17/03/17 01:04:38 INFO mapred.JobClient:  map 100% reduce 100%
17/03/17 01:04:38 INFO mapred.JobClient: Job complete: job_201703170049_0001
17/03/17 01:04:38 INFO mapred.JobClient: Counters: 30
17/03/17 01:04:38 INFO mapred.JobClient:   Job Counters
17/03/17 01:04:38 INFO mapred.JobClient:     Launched reduce tasks=2
17/03/17 01:04:38 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=6333753
17/03/17 01:04:38 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/17 01:04:38 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/17 01:04:38 INFO mapred.JobClient:     Rack-local map tasks=1
17/03/17 01:04:38 INFO mapred.JobClient:     Launched map tasks=364
17/03/17 01:04:38 INFO mapred.JobClient:     Data-local map tasks=363
17/03/17 01:04:38 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=385000
17/03/17 01:04:38 INFO mapred.JobClient:   File Output Format Counters
17/03/17 01:04:38 INFO mapred.JobClient:     Bytes Written=1203367645
17/03/17 01:04:38 INFO mapred.JobClient:   FileSystemCounters
17/03/17 01:04:38 INFO mapred.JobClient:     FILE_BYTES_READ=10555831669
17/03/17 01:04:38 INFO mapred.JobClient:     HDFS_BYTES_READ=44102118829
17/03/17 01:04:38 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=13418742165
17/03/17 01:04:38 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=1203367645
17/03/17 01:04:38 INFO mapred.JobClient:   File Input Format Counters
17/03/17 01:04:38 INFO mapred.JobClient:     Bytes Read=44102068429
17/03/17 01:04:38 INFO mapred.JobClient:   Map-Reduce Framework
17/03/17 01:04:38 INFO mapred.JobClient:     Map output materialized bytes=2844824603
17/03/17 01:04:38 INFO mapred.JobClient:     Map input records=4263299
17/03/17 01:04:38 INFO mapred.JobClient:     Reduce shuffle bytes=2844824603
17/03/17 01:04:38 INFO mapred.JobClient:     Spilled Records=444878974
17/03/17 01:04:38 INFO mapred.JobClient:     Map output bytes=60897778366
17/03/17 01:04:38 INFO mapred.JobClient:     Total committed heap usage (bytes)=68908220416
17/03/17 01:04:38 INFO mapred.JobClient:     CPU time spent (ms)=8825730
17/03/17 01:04:38 INFO mapred.JobClient:     Combine input records=4264052943
17/03/17 01:04:38 INFO mapred.JobClient:     SPLIT_RAW_BYTES=50400
17/03/17 01:04:38 INFO mapred.JobClient:     Reduce input records=59157342
17/03/17 01:04:38 INFO mapred.JobClient:     Reduce input groups=31799048
17/03/17 01:04:38 INFO mapred.JobClient:     Combine output records=284581597
17/03/17 01:04:38 INFO mapred.JobClient:     Physical memory (bytes) snapshot=81620508672
17/03/17 01:04:38 INFO mapred.JobClient:     Reduce output records=31799048
17/03/17 01:04:38 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=289617219584
17/03/17 01:04:38 INFO mapred.JobClient:     Map output records=4038628688
```

## Wordcount normal with expiry interval of 30s and slowstart 1
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar wordcount outputtext outputtextcounted
17/03/17 01:07:54 INFO input.FileInputFormat: Total input paths to process : 40
17/03/17 01:07:54 INFO util.NativeCodeLoader: Loaded the native-hadoop library
17/03/17 01:07:54 WARN snappy.LoadSnappy: Snappy native library not loaded
17/03/17 01:07:54 INFO mapred.JobClient: Running job: job_201703170107_0001
17/03/17 01:07:55 INFO mapred.JobClient:  map 0% reduce 0%
17/03/17 01:08:09 INFO mapred.JobClient:  map 1% reduce 0%
17/03/17 01:08:15 INFO mapred.JobClient:  map 2% reduce 0%
17/03/17 01:08:26 INFO mapred.JobClient:  map 3% reduce 0%
17/03/17 01:08:33 INFO mapred.JobClient:  map 4% reduce 0%
17/03/17 01:08:43 INFO mapred.JobClient:  map 5% reduce 0%
17/03/17 01:08:49 INFO mapred.JobClient:  map 6% reduce 0%
17/03/17 01:09:01 INFO mapred.JobClient:  map 7% reduce 0%
17/03/17 01:09:08 INFO mapred.JobClient:  map 8% reduce 0%
17/03/17 01:09:20 INFO mapred.JobClient:  map 9% reduce 0%
17/03/17 01:09:25 INFO mapred.JobClient:  map 10% reduce 0%
17/03/17 01:09:32 INFO mapred.JobClient:  map 11% reduce 0%
17/03/17 01:09:42 INFO mapred.JobClient:  map 12% reduce 0%
17/03/17 01:09:49 INFO mapred.JobClient:  map 13% reduce 0%
17/03/17 01:10:00 INFO mapred.JobClient:  map 14% reduce 0%
17/03/17 01:10:07 INFO mapred.JobClient:  map 15% reduce 0%
17/03/17 01:10:17 INFO mapred.JobClient:  map 16% reduce 0%
17/03/17 01:10:25 INFO mapred.JobClient:  map 17% reduce 0%
17/03/17 01:10:36 INFO mapred.JobClient:  map 18% reduce 0%
17/03/17 01:10:43 INFO mapred.JobClient:  map 19% reduce 0%
17/03/17 01:10:55 INFO mapred.JobClient:  map 20% reduce 0%
17/03/17 01:11:01 INFO mapred.JobClient:  map 21% reduce 0%
17/03/17 01:11:08 INFO mapred.JobClient:  map 22% reduce 0%
17/03/17 01:11:18 INFO mapred.JobClient:  map 23% reduce 0%
17/03/17 01:11:25 INFO mapred.JobClient:  map 24% reduce 0%
17/03/17 01:11:37 INFO mapred.JobClient:  map 25% reduce 0%
17/03/17 01:11:43 INFO mapred.JobClient:  map 26% reduce 0%
17/03/17 01:11:53 INFO mapred.JobClient:  map 27% reduce 0%
17/03/17 01:12:02 INFO mapred.JobClient:  map 28% reduce 0%
17/03/17 01:12:12 INFO mapred.JobClient:  map 29% reduce 0%
17/03/17 01:12:19 INFO mapred.JobClient:  map 30% reduce 0%
17/03/17 01:12:30 INFO mapred.JobClient:  map 31% reduce 0%
17/03/17 01:12:36 INFO mapred.JobClient:  map 32% reduce 0%
17/03/17 01:12:44 INFO mapred.JobClient:  map 33% reduce 0%
17/03/17 01:12:53 INFO mapred.JobClient:  map 34% reduce 0%
17/03/17 01:13:00 INFO mapred.JobClient:  map 35% reduce 0%
17/03/17 01:13:10 INFO mapred.JobClient:  map 36% reduce 0%
17/03/17 01:13:18 INFO mapred.JobClient:  map 37% reduce 0%
17/03/17 01:13:28 INFO mapred.JobClient:  map 38% reduce 0%
17/03/17 01:13:36 INFO mapred.JobClient:  map 39% reduce 0%
17/03/17 01:13:46 INFO mapred.JobClient:  map 40% reduce 0%
17/03/17 01:13:52 INFO mapred.JobClient:  map 41% reduce 0%
17/03/17 01:14:03 INFO mapred.JobClient:  map 42% reduce 0%
17/03/17 01:14:09 INFO mapred.JobClient:  map 43% reduce 0%
17/03/17 01:14:18 INFO mapred.JobClient:  map 44% reduce 0%
17/03/17 01:14:27 INFO mapred.JobClient:  map 45% reduce 0%
17/03/17 01:14:35 INFO mapred.JobClient:  map 46% reduce 0%
17/03/17 01:14:44 INFO mapred.JobClient:  map 47% reduce 0%
17/03/17 01:14:52 INFO mapred.JobClient:  map 48% reduce 0%
17/03/17 01:15:02 INFO mapred.JobClient:  map 49% reduce 0%
17/03/17 01:15:09 INFO mapred.JobClient:  map 50% reduce 0%
17/03/17 01:15:19 INFO mapred.JobClient:  map 51% reduce 0%
17/03/17 01:15:25 INFO mapred.JobClient:  map 52% reduce 0%
17/03/17 01:15:35 INFO mapred.JobClient:  map 53% reduce 0%
17/03/17 01:15:43 INFO mapred.JobClient:  map 54% reduce 0%
17/03/17 01:15:51 INFO mapred.JobClient:  map 55% reduce 0%
17/03/17 01:16:01 INFO mapred.JobClient:  map 56% reduce 0%
17/03/17 01:16:09 INFO mapred.JobClient:  map 57% reduce 0%
17/03/17 01:16:18 INFO mapred.JobClient:  map 58% reduce 0%
17/03/17 01:16:26 INFO mapred.JobClient:  map 59% reduce 0%
17/03/17 01:16:36 INFO mapred.JobClient:  map 60% reduce 0%
17/03/17 01:16:44 INFO mapred.JobClient:  map 61% reduce 0%
17/03/17 01:16:53 INFO mapred.JobClient:  map 62% reduce 0%
17/03/17 01:17:01 INFO mapred.JobClient:  map 63% reduce 0%
17/03/17 01:17:10 INFO mapred.JobClient:  map 64% reduce 0%
17/03/17 01:17:19 INFO mapred.JobClient:  map 65% reduce 0%
17/03/17 01:17:27 INFO mapred.JobClient:  map 66% reduce 0%
17/03/17 01:17:36 INFO mapred.JobClient:  map 67% reduce 0%
17/03/17 01:17:44 INFO mapred.JobClient:  map 68% reduce 0%
17/03/17 01:17:53 INFO mapred.JobClient:  map 69% reduce 0%
17/03/17 01:18:02 INFO mapred.JobClient:  map 70% reduce 0%
17/03/17 01:18:12 INFO mapred.JobClient:  map 71% reduce 0%
17/03/17 01:18:20 INFO mapred.JobClient:  map 72% reduce 0%
17/03/17 01:18:28 INFO mapred.JobClient:  map 73% reduce 0%
17/03/17 01:18:38 INFO mapred.JobClient:  map 74% reduce 0%
17/03/17 01:18:45 INFO mapred.JobClient:  map 75% reduce 0%
17/03/17 01:18:54 INFO mapred.JobClient:  map 76% reduce 0%
17/03/17 01:19:02 INFO mapred.JobClient:  map 77% reduce 0%
17/03/17 01:19:10 INFO mapred.JobClient:  map 78% reduce 0%
17/03/17 01:19:19 INFO mapred.JobClient:  map 79% reduce 0%
17/03/17 01:19:29 INFO mapred.JobClient:  map 80% reduce 0%
17/03/17 01:19:36 INFO mapred.JobClient:  map 81% reduce 0%
17/03/17 01:19:46 INFO mapred.JobClient:  map 82% reduce 0%
17/03/17 01:19:54 INFO mapred.JobClient:  map 83% reduce 0%
17/03/17 01:20:02 INFO mapred.JobClient:  map 84% reduce 0%
17/03/17 01:20:10 INFO mapred.JobClient:  map 85% reduce 0%
17/03/17 01:20:18 INFO mapred.JobClient:  map 86% reduce 0%
17/03/17 01:20:26 INFO mapred.JobClient:  map 87% reduce 0%
17/03/17 01:20:36 INFO mapred.JobClient:  map 88% reduce 0%
17/03/17 01:20:43 INFO mapred.JobClient:  map 89% reduce 0%
17/03/17 01:20:45 INFO mapred.JobClient:  map 90% reduce 0%
17/03/17 01:20:50 INFO mapred.JobClient:  map 91% reduce 0%
17/03/17 01:20:52 INFO mapred.JobClient:  map 92% reduce 0%
17/03/17 01:20:55 INFO mapred.JobClient:  map 93% reduce 0%
17/03/17 01:20:57 INFO mapred.JobClient:  map 94% reduce 0%
17/03/17 01:21:01 INFO mapred.JobClient:  map 95% reduce 0%
17/03/17 01:21:02 INFO mapred.JobClient:  map 96% reduce 0%
17/03/17 01:21:07 INFO mapred.JobClient:  map 97% reduce 0%
17/03/17 01:21:08 INFO mapred.JobClient:  map 98% reduce 0%
17/03/17 01:21:11 INFO mapred.JobClient:  map 99% reduce 0%
17/03/17 01:21:14 INFO mapred.JobClient:  map 100% reduce 0%
17/03/17 01:21:21 INFO mapred.JobClient:  map 100% reduce 1%
17/03/17 01:21:24 INFO mapred.JobClient:  map 100% reduce 2%
17/03/17 01:21:27 INFO mapred.JobClient:  map 100% reduce 4%
17/03/17 01:21:30 INFO mapred.JobClient:  map 100% reduce 6%
17/03/17 01:21:33 INFO mapred.JobClient:  map 100% reduce 7%
17/03/17 01:21:36 INFO mapred.JobClient:  map 100% reduce 9%
17/03/17 01:21:39 INFO mapred.JobClient:  map 100% reduce 11%
17/03/17 01:21:42 INFO mapred.JobClient:  map 100% reduce 12%
17/03/17 01:21:45 INFO mapred.JobClient:  map 100% reduce 14%
17/03/17 01:21:48 INFO mapred.JobClient:  map 100% reduce 15%
17/03/17 01:21:51 INFO mapred.JobClient:  map 100% reduce 17%
17/03/17 01:21:55 INFO mapred.JobClient:  map 100% reduce 18%
17/03/17 01:21:58 INFO mapred.JobClient:  map 100% reduce 20%
17/03/17 01:22:01 INFO mapred.JobClient:  map 100% reduce 22%
17/03/17 01:22:04 INFO mapred.JobClient:  map 100% reduce 23%
17/03/17 01:22:07 INFO mapred.JobClient:  map 100% reduce 25%
17/03/17 01:22:10 INFO mapred.JobClient:  map 100% reduce 26%
17/03/17 01:22:13 INFO mapred.JobClient:  map 100% reduce 28%
17/03/17 01:22:16 INFO mapred.JobClient:  map 100% reduce 30%
17/03/17 01:22:19 INFO mapred.JobClient:  map 100% reduce 33%
17/03/17 01:22:34 INFO mapred.JobClient:  map 100% reduce 68%
17/03/17 01:22:37 INFO mapred.JobClient:  map 100% reduce 70%
17/03/17 01:22:40 INFO mapred.JobClient:  map 100% reduce 72%
17/03/17 01:22:43 INFO mapred.JobClient:  map 100% reduce 74%
17/03/17 01:22:46 INFO mapred.JobClient:  map 100% reduce 76%
17/03/17 01:22:49 INFO mapred.JobClient:  map 100% reduce 78%
17/03/17 01:22:52 INFO mapred.JobClient:  map 100% reduce 81%
17/03/17 01:22:55 INFO mapred.JobClient:  map 100% reduce 83%
17/03/17 01:22:58 INFO mapred.JobClient:  map 100% reduce 86%
17/03/17 01:23:01 INFO mapred.JobClient:  map 100% reduce 90%
17/03/17 01:23:04 INFO mapred.JobClient:  map 100% reduce 93%
17/03/17 01:23:07 INFO mapred.JobClient:  map 100% reduce 95%
17/03/17 01:23:10 INFO mapred.JobClient:  map 100% reduce 98%
17/03/17 01:23:12 INFO mapred.JobClient:  map 100% reduce 100%
17/03/17 01:23:13 INFO mapred.JobClient: Job complete: job_201703170107_0001
17/03/17 01:23:13 INFO mapred.JobClient: Counters: 29
17/03/17 01:23:13 INFO mapred.JobClient:   Job Counters
17/03/17 01:23:13 INFO mapred.JobClient:     Launched reduce tasks=1
17/03/17 01:23:13 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=6286834
17/03/17 01:23:13 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/17 01:23:13 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/17 01:23:13 INFO mapred.JobClient:     Launched map tasks=365
17/03/17 01:23:13 INFO mapred.JobClient:     Data-local map tasks=365
17/03/17 01:23:13 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=118472
17/03/17 01:23:13 INFO mapred.JobClient:   File Output Format Counters
17/03/17 01:23:13 INFO mapred.JobClient:     Bytes Written=1203367645
17/03/17 01:23:13 INFO mapred.JobClient:   FileSystemCounters
17/03/17 01:23:13 INFO mapred.JobClient:     FILE_BYTES_READ=10592714862
17/03/17 01:23:13 INFO mapred.JobClient:     HDFS_BYTES_READ=44102118829
17/03/17 01:23:13 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=13455624596
17/03/17 01:23:13 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=1203367645
17/03/17 01:23:13 INFO mapred.JobClient:   File Input Format Counters
17/03/17 01:23:13 INFO mapred.JobClient:     Bytes Read=44102068429
17/03/17 01:23:13 INFO mapred.JobClient:   Map-Reduce Framework
17/03/17 01:23:13 INFO mapred.JobClient:     Map output materialized bytes=2844824603
17/03/17 01:23:13 INFO mapred.JobClient:     Map input records=4263299
17/03/17 01:23:13 INFO mapred.JobClient:     Reduce shuffle bytes=2844824603
17/03/17 01:23:13 INFO mapred.JobClient:     Spilled Records=446196096
17/03/17 01:23:13 INFO mapred.JobClient:     Map output bytes=60897778366
17/03/17 01:23:13 INFO mapred.JobClient:     Total committed heap usage (bytes)=68897734656
17/03/17 01:23:13 INFO mapred.JobClient:     CPU time spent (ms)=8681430
17/03/17 01:23:13 INFO mapred.JobClient:     Combine input records=4265897228
17/03/17 01:23:13 INFO mapred.JobClient:     SPLIT_RAW_BYTES=50400
17/03/17 01:23:13 INFO mapred.JobClient:     Reduce input records=58445456
17/03/17 01:23:13 INFO mapred.JobClient:     Reduce input groups=31799048
17/03/17 01:23:13 INFO mapred.JobClient:     Combine output records=285713996
17/03/17 01:23:13 INFO mapred.JobClient:     Physical memory (bytes) snapshot=81336971264
17/03/17 01:23:13 INFO mapred.JobClient:     Reduce output records=31799048
17/03/17 01:23:13 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=288823660544
17/03/17 01:23:13 INFO mapred.JobClient:     Map output records=4038628688
```

# Speculation disabled
## Normal
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 19:18:44 UTC 2017
17/03/16 19:18:44 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 19:18:44 INFO mapred.JobClient: Running job: job_201703161917_0002
17/03/16 19:18:45 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 19:18:52 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 19:18:55 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 19:18:58 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 19:19:01 INFO mapred.JobClient:  map 8% reduce 0%
17/03/16 19:19:02 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 19:19:04 INFO mapred.JobClient: Task Id : attempt_201703161917_0002_r_000003_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:19:06 INFO mapred.JobClient:  map 12% reduce 1%
17/03/16 19:19:07 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 19:19:09 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 19:19:13 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 19:19:15 INFO mapred.JobClient:  map 17% reduce 3%
17/03/16 19:19:16 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 19:19:19 INFO mapred.JobClient:  map 20% reduce 5%
17/03/16 19:19:20 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 19:19:22 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 19:19:23 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 19:19:26 INFO mapred.JobClient:  map 25% reduce 6%
17/03/16 19:19:27 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 19:19:28 INFO mapred.JobClient:  map 27% reduce 8%
17/03/16 19:19:30 INFO mapred.JobClient:  map 29% reduce 8%
17/03/16 19:19:33 INFO mapred.JobClient:  map 31% reduce 8%
17/03/16 19:19:34 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 19:19:36 INFO mapred.JobClient:  map 33% reduce 9%
17/03/16 19:19:37 INFO mapred.JobClient:  map 34% reduce 9%
17/03/16 19:19:40 INFO mapred.JobClient:  map 35% reduce 10%
17/03/16 19:19:41 INFO mapred.JobClient:  map 37% reduce 10%
17/03/16 19:19:42 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 19:19:44 INFO mapred.JobClient:  map 38% reduce 11%
17/03/16 19:19:45 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 19:19:49 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 19:19:50 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 19:19:52 INFO mapred.JobClient:  map 42% reduce 13%
17/03/16 19:19:53 INFO mapred.JobClient:  map 43% reduce 13%
17/03/16 19:19:54 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 19:19:57 INFO mapred.JobClient:  map 46% reduce 13%
17/03/16 19:19:58 INFO mapred.JobClient:  map 47% reduce 13%
17/03/16 19:20:00 INFO mapred.JobClient:  map 48% reduce 14%
17/03/16 19:20:01 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 19:20:04 INFO mapred.JobClient:  map 51% reduce 15%
17/03/16 19:20:05 INFO mapred.JobClient:  map 52% reduce 15%
17/03/16 19:20:06 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 19:20:07 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 19:20:08 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 19:20:10 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 19:20:11 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 19:20:12 INFO mapred.JobClient:  map 56% reduce 17%
17/03/16 19:20:14 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 19:20:15 INFO mapred.JobClient:  map 58% reduce 17%
17/03/16 19:20:16 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 19:20:18 INFO mapred.JobClient:  map 60% reduce 18%
17/03/16 19:20:20 INFO mapred.JobClient:  map 60% reduce 19%
17/03/16 19:20:21 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 19:20:22 INFO mapred.JobClient:  map 63% reduce 19%
17/03/16 19:20:25 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 19:20:26 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 19:20:27 INFO mapred.JobClient:  map 65% reduce 20%
17/03/16 19:20:28 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 19:20:29 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 19:20:31 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 19:20:33 INFO mapred.JobClient:  map 70% reduce 21%
17/03/16 19:20:34 INFO mapred.JobClient:  map 70% reduce 22%
17/03/16 19:20:36 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 19:20:37 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 19:20:38 INFO mapred.JobClient:  map 73% reduce 23%
17/03/16 19:20:40 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 19:20:41 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 19:20:43 INFO mapred.JobClient:  map 76% reduce 23%
17/03/16 19:20:44 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 19:20:45 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 19:20:46 INFO mapred.JobClient:  map 78% reduce 25%
17/03/16 19:20:47 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 19:20:49 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 19:20:50 INFO mapred.JobClient:  map 81% reduce 26%
17/03/16 19:20:52 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 19:20:54 INFO mapred.JobClient:  map 84% reduce 26%
17/03/16 19:20:55 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 19:20:56 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 19:20:58 INFO mapred.JobClient:  map 86% reduce 27%
17/03/16 19:20:59 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 19:21:00 INFO mapred.JobClient:  map 88% reduce 27%
17/03/16 19:21:01 INFO mapred.JobClient:  map 89% reduce 27%
17/03/16 19:21:02 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 19:21:03 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 19:21:05 INFO mapred.JobClient:  map 91% reduce 29%
17/03/16 19:21:06 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 19:21:07 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 19:21:08 INFO mapred.JobClient:  map 93% reduce 30%
17/03/16 19:21:09 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 19:21:11 INFO mapred.JobClient:  map 95% reduce 31%
17/03/16 19:21:12 INFO mapred.JobClient:  map 96% reduce 31%
17/03/16 19:21:14 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 19:21:15 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 19:21:16 INFO mapred.JobClient:  map 99% reduce 31%
17/03/16 19:21:18 INFO mapred.JobClient:  map 100% reduce 31%
17/03/16 19:21:20 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 19:21:25 INFO mapred.JobClient:  map 100% reduce 40%
17/03/16 19:21:26 INFO mapred.JobClient:  map 100% reduce 47%
17/03/16 19:21:28 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 19:21:29 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 19:21:30 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 19:21:31 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 19:21:32 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 19:21:34 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 19:21:36 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 19:21:37 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 19:21:39 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 19:21:42 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 19:21:45 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 19:21:47 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 19:21:50 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 19:21:53 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 19:21:56 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 19:21:57 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 19:22:00 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 19:22:03 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 19:22:05 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 19:22:08 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 19:22:09 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 19:22:15 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 19:22:32 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 19:22:42 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 19:22:51 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 19:23:03 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 19:23:09 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 19:23:14 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 19:23:21 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 19:23:29 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 19:23:34 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 19:23:42 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 19:23:53 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 19:24:00 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 19:24:01 INFO mapred.JobClient: Job complete: job_201703161917_0002
17/03/16 19:24:01 INFO mapred.JobClient: Counters: 30
17/03/16 19:24:01 INFO mapred.JobClient:   Job Counters
17/03/16 19:24:01 INFO mapred.JobClient:     Launched reduce tasks=7
17/03/16 19:24:01 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=852811
17/03/16 19:24:01 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 19:24:01 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 19:24:01 INFO mapred.JobClient:     Launched map tasks=243
17/03/16 19:24:01 INFO mapred.JobClient:     Data-local map tasks=243
17/03/16 19:24:01 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1437362
17/03/16 19:24:01 INFO mapred.JobClient:   File Input Format Counters
17/03/16 19:24:01 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 19:24:01 INFO mapred.JobClient:   File Output Format Counters
17/03/16 19:24:01 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 19:24:01 INFO mapred.JobClient:   FileSystemCounters
17/03/16 19:24:01 INFO mapred.JobClient:     FILE_BYTES_READ=94342466564
17/03/16 19:24:01 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 19:24:01 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126601838613
17/03/16 19:24:01 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 19:24:01 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 19:24:01 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 19:24:01 INFO mapred.JobClient:     Map input records=3068055
17/03/16 19:24:01 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 19:24:01 INFO mapred.JobClient:     Spilled Records=12042215
17/03/16 19:24:01 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 19:24:01 INFO mapred.JobClient:     Total committed heap usage (bytes)=49336025088
17/03/16 19:24:01 INFO mapred.JobClient:     CPU time spent (ms)=1574110
17/03/16 19:24:01 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 19:24:01 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 19:24:01 INFO mapred.JobClient:     Combine input records=0
17/03/16 19:24:01 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 19:24:01 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 19:24:01 INFO mapred.JobClient:     Combine output records=0
17/03/16 19:24:01 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52969574400
17/03/16 19:24:01 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 19:24:01 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=195928961024
17/03/16 19:24:01 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 19:24:01 UTC 2017
The job took 317 seconds.
```

## CPU stress (hanoi on one node)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 19:26:19 UTC 2017
17/03/16 19:26:19 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 19:26:19 INFO mapred.JobClient: Running job: job_201703161917_0003
17/03/16 19:26:20 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 19:26:26 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 19:26:29 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 19:26:32 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 19:26:33 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 19:26:35 INFO mapred.JobClient:  map 8% reduce 0%
17/03/16 19:26:36 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 19:26:38 INFO mapred.JobClient: Task Id : attempt_201703161917_0003_r_000000_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:26:38 INFO mapred.JobClient: Task Id : attempt_201703161917_0003_r_000001_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:26:39 INFO mapred.JobClient:  map 11% reduce 0%
17/03/16 19:26:40 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 19:26:43 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 19:26:46 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 19:26:49 INFO mapred.JobClient:  map 17% reduce 4%
17/03/16 19:26:50 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 19:26:52 INFO mapred.JobClient:  map 19% reduce 5%
17/03/16 19:26:53 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 19:26:55 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 19:26:57 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 19:27:00 INFO mapred.JobClient:  map 26% reduce 6%
17/03/16 19:27:01 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 19:27:03 INFO mapred.JobClient:  map 28% reduce 7%
17/03/16 19:27:04 INFO mapred.JobClient:  map 29% reduce 8%
17/03/16 19:27:06 INFO mapred.JobClient:  map 30% reduce 8%
17/03/16 19:27:07 INFO mapred.JobClient:  map 31% reduce 9%
17/03/16 19:27:08 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 19:27:11 INFO mapred.JobClient:  map 34% reduce 9%
17/03/16 19:27:13 INFO mapred.JobClient:  map 34% reduce 10%
17/03/16 19:27:14 INFO mapred.JobClient:  map 36% reduce 10%
17/03/16 19:27:16 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 19:27:18 INFO mapred.JobClient:  map 39% reduce 11%
17/03/16 19:27:20 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 19:27:22 INFO mapred.JobClient:  map 41% reduce 12%
17/03/16 19:27:25 INFO mapred.JobClient:  map 42% reduce 13%
17/03/16 19:27:26 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 19:27:29 INFO mapred.JobClient:  map 45% reduce 13%
17/03/16 19:27:30 INFO mapred.JobClient:  map 46% reduce 13%
17/03/16 19:27:31 INFO mapred.JobClient:  map 46% reduce 14%
17/03/16 19:27:32 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 19:27:33 INFO mapred.JobClient:  map 48% reduce 14%
17/03/16 19:27:34 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 19:27:35 INFO mapred.JobClient:  map 49% reduce 15%
17/03/16 19:27:37 INFO mapred.JobClient:  map 51% reduce 15%
17/03/16 19:27:40 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 19:27:41 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 19:27:44 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 19:27:45 INFO mapred.JobClient:  map 56% reduce 17%
17/03/16 19:27:47 INFO mapred.JobClient:  map 57% reduce 18%
17/03/16 19:27:48 INFO mapred.JobClient:  map 58% reduce 18%
17/03/16 19:27:49 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 19:27:51 INFO mapred.JobClient:  map 60% reduce 18%
17/03/16 19:27:52 INFO mapred.JobClient:  map 61% reduce 18%
17/03/16 19:27:53 INFO mapred.JobClient:  map 61% reduce 19%
17/03/16 19:27:55 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 19:27:57 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 19:27:59 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 19:28:00 INFO mapred.JobClient:  map 65% reduce 20%
17/03/16 19:28:01 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 19:28:02 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 19:28:04 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 19:28:05 INFO mapred.JobClient:  map 69% reduce 21%
17/03/16 19:28:07 INFO mapred.JobClient:  map 70% reduce 22%
17/03/16 19:28:08 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 19:28:10 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 19:28:11 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 19:28:13 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 19:28:14 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 19:28:15 INFO mapred.JobClient:  map 76% reduce 23%
17/03/16 19:28:17 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 19:28:19 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 19:28:20 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 19:28:22 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 19:28:23 INFO mapred.JobClient:  map 81% reduce 26%
17/03/16 19:28:25 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 19:28:26 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 19:28:27 INFO mapred.JobClient:  map 84% reduce 26%
17/03/16 19:28:29 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 19:28:31 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 19:28:32 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 19:28:35 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 19:28:36 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 19:28:38 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 19:28:39 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 19:28:42 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 19:28:43 INFO mapred.JobClient:  map 94% reduce 29%
17/03/16 19:28:44 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 19:28:46 INFO mapred.JobClient:  map 97% reduce 30%
17/03/16 19:28:47 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 19:28:49 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 19:28:50 INFO mapred.JobClient:  map 99% reduce 32%
17/03/16 19:28:52 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 19:28:58 INFO mapred.JobClient:  map 100% reduce 39%
17/03/16 19:28:59 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 19:29:03 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 19:29:06 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 19:29:08 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 19:29:08 INFO mapred.JobClient: Task Id : attempt_201703161917_0003_r_000002_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:29:09 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 19:29:11 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 19:29:12 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 19:29:17 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 19:29:20 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 19:29:21 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 19:29:23 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 19:29:26 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 19:29:29 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 19:29:32 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 19:29:35 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 19:29:36 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 19:29:38 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 19:29:41 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 19:29:50 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 19:29:59 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 19:30:08 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 19:30:15 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 19:30:23 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 19:30:29 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 19:30:37 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 19:30:47 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 19:30:52 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 19:31:00 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 19:31:12 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 19:31:19 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 19:31:25 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 19:31:25 INFO mapred.JobClient: Job complete: job_201703161917_0003
17/03/16 19:31:25 INFO mapred.JobClient: Counters: 30
17/03/16 19:31:25 INFO mapred.JobClient:   Job Counters
17/03/16 19:31:25 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 19:31:25 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=861723
17/03/16 19:31:25 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 19:31:25 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 19:31:25 INFO mapred.JobClient:     Launched map tasks=244
17/03/16 19:31:25 INFO mapred.JobClient:     Data-local map tasks=244
17/03/16 19:31:25 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1410270
17/03/16 19:31:25 INFO mapred.JobClient:   File Input Format Counters
17/03/16 19:31:25 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 19:31:25 INFO mapred.JobClient:   File Output Format Counters
17/03/16 19:31:25 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 19:31:25 INFO mapred.JobClient:   FileSystemCounters
17/03/16 19:31:25 INFO mapred.JobClient:     FILE_BYTES_READ=94314313380
17/03/16 19:31:25 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 19:31:25 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126573685429
17/03/16 19:31:25 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 19:31:25 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 19:31:25 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 19:31:25 INFO mapred.JobClient:     Map input records=3068055
17/03/16 19:31:25 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 19:31:25 INFO mapred.JobClient:     Spilled Records=12039673
17/03/16 19:31:25 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 19:31:25 INFO mapred.JobClient:     Total committed heap usage (bytes)=49354899456
17/03/16 19:31:25 INFO mapred.JobClient:     CPU time spent (ms)=1583180
17/03/16 19:31:25 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 19:31:25 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 19:31:25 INFO mapred.JobClient:     Combine input records=0
17/03/16 19:31:25 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 19:31:25 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 19:31:25 INFO mapred.JobClient:     Combine output records=0
17/03/16 19:31:25 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52965875712
17/03/16 19:31:25 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 19:31:25 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196011810816
17/03/16 19:31:25 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 19:31:25 UTC 2017
The job took 305 seconds.
```

## CPU stress (stress --cpu 16 on one node)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 19:37:50 UTC 2017
17/03/16 19:37:50 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 19:37:50 INFO mapred.JobClient: Running job: job_201703161917_0006
17/03/16 19:37:51 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 19:37:57 INFO mapred.JobClient:  map 1% reduce 0%
17/03/16 19:37:58 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 19:38:00 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 19:38:01 INFO mapred.JobClient:  map 4% reduce 0%
17/03/16 19:38:03 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 19:38:04 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 19:38:07 INFO mapred.JobClient:  map 8% reduce 0%
17/03/16 19:38:08 INFO mapred.JobClient:  map 9% reduce 0%
17/03/16 19:38:10 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 19:38:11 INFO mapred.JobClient:  map 11% reduce 0%
17/03/16 19:38:11 INFO mapred.JobClient: Task Id : attempt_201703161917_0006_r_000002_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:38:11 INFO mapred.JobClient: Task Id : attempt_201703161917_0006_r_000004_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:38:13 INFO mapred.JobClient:  map 11% reduce 1%
17/03/16 19:38:14 INFO mapred.JobClient:  map 13% reduce 1%
17/03/16 19:38:16 INFO mapred.JobClient:  map 14% reduce 1%
17/03/16 19:38:17 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 19:38:19 INFO mapred.JobClient:  map 16% reduce 2%
17/03/16 19:38:20 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 19:38:21 INFO mapred.JobClient:  map 18% reduce 2%
17/03/16 19:38:23 INFO mapred.JobClient:  map 19% reduce 3%
17/03/16 19:38:23 INFO mapred.JobClient: Task Id : attempt_201703161917_0006_r_000000_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:38:24 INFO mapred.JobClient:  map 20% reduce 3%
17/03/16 19:38:26 INFO mapred.JobClient:  map 20% reduce 4%
17/03/16 19:38:27 INFO mapred.JobClient:  map 22% reduce 4%
17/03/16 19:38:28 INFO mapred.JobClient:  map 23% reduce 5%
17/03/16 19:38:31 INFO mapred.JobClient:  map 25% reduce 5%
17/03/16 19:38:32 INFO mapred.JobClient:  map 25% reduce 6%
17/03/16 19:38:34 INFO mapred.JobClient:  map 26% reduce 6%
17/03/16 19:38:35 INFO mapred.JobClient:  map 28% reduce 7%
17/03/16 19:38:38 INFO mapred.JobClient:  map 29% reduce 8%
17/03/16 19:38:39 INFO mapred.JobClient:  map 30% reduce 8%
17/03/16 19:38:41 INFO mapred.JobClient:  map 30% reduce 9%
17/03/16 19:38:42 INFO mapred.JobClient:  map 31% reduce 9%
17/03/16 19:38:43 INFO mapred.JobClient:  map 33% reduce 9%
17/03/16 19:38:47 INFO mapred.JobClient:  map 34% reduce 10%
17/03/16 19:38:48 INFO mapred.JobClient:  map 35% reduce 10%
17/03/16 19:38:50 INFO mapred.JobClient:  map 35% reduce 11%
17/03/16 19:38:51 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 19:38:52 INFO mapred.JobClient:  map 38% reduce 11%
17/03/16 19:38:55 INFO mapred.JobClient:  map 39% reduce 11%
17/03/16 19:38:56 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 19:38:58 INFO mapred.JobClient:  map 41% reduce 12%
17/03/16 19:38:59 INFO mapred.JobClient:  map 42% reduce 13%
17/03/16 19:39:00 INFO mapred.JobClient:  map 43% reduce 13%
17/03/16 19:39:02 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 19:39:04 INFO mapred.JobClient:  map 45% reduce 13%
17/03/16 19:39:05 INFO mapred.JobClient:  map 46% reduce 14%
17/03/16 19:39:07 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 19:39:08 INFO mapred.JobClient:  map 48% reduce 14%
17/03/16 19:39:09 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 19:39:11 INFO mapred.JobClient:  map 50% reduce 15%
17/03/16 19:39:13 INFO mapred.JobClient:  map 51% reduce 15%
17/03/16 19:39:14 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 19:39:15 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 19:39:16 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 19:39:18 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 19:39:19 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 19:39:22 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 19:39:23 INFO mapred.JobClient:  map 58% reduce 18%
17/03/16 19:39:26 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 19:39:27 INFO mapred.JobClient:  map 60% reduce 18%
17/03/16 19:39:29 INFO mapred.JobClient:  map 61% reduce 19%
17/03/16 19:39:30 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 19:39:31 INFO mapred.JobClient:  map 63% reduce 19%
17/03/16 19:39:33 INFO mapred.JobClient:  map 64% reduce 20%
17/03/16 19:39:34 INFO mapred.JobClient:  map 65% reduce 20%
17/03/16 19:39:36 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 19:39:37 INFO mapred.JobClient:  map 67% reduce 20%
17/03/16 19:39:38 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 19:39:39 INFO mapred.JobClient:  map 69% reduce 21%
17/03/16 19:39:41 INFO mapred.JobClient:  map 69% reduce 22%
17/03/16 19:39:42 INFO mapred.JobClient:  map 70% reduce 22%
17/03/16 19:39:43 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 19:39:44 INFO mapred.JobClient:  map 72% reduce 23%
17/03/16 19:39:46 INFO mapred.JobClient:  map 73% reduce 23%
17/03/16 19:39:47 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 19:39:49 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 19:39:50 INFO mapred.JobClient:  map 76% reduce 23%
17/03/16 19:39:51 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 19:39:53 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 19:39:55 INFO mapred.JobClient:  map 79% reduce 24%
17/03/16 19:39:56 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 19:39:57 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 19:39:58 INFO mapred.JobClient:  map 82% reduce 25%
17/03/16 19:39:59 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 19:40:02 INFO mapred.JobClient:  map 84% reduce 26%
17/03/16 19:40:03 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 19:40:04 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 19:40:06 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 19:40:09 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 19:40:11 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 19:40:13 INFO mapred.JobClient:  map 91% reduce 28%
17/03/16 19:40:14 INFO mapred.JobClient:  map 91% reduce 29%
17/03/16 19:40:15 INFO mapred.JobClient:  map 92% reduce 30%
17/03/16 19:40:16 INFO mapred.JobClient:  map 93% reduce 30%
17/03/16 19:40:18 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 19:40:19 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 19:40:21 INFO mapred.JobClient:  map 96% reduce 31%
17/03/16 19:40:22 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 19:40:23 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 19:40:25 INFO mapred.JobClient:  map 99% reduce 31%
17/03/16 19:40:27 INFO mapred.JobClient:  map 99% reduce 32%
17/03/16 19:40:28 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 19:40:30 INFO mapred.JobClient:  map 100% reduce 33%
17/03/16 19:40:33 INFO mapred.JobClient:  map 100% reduce 46%
17/03/16 19:40:36 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 19:40:39 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 19:40:42 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 19:40:45 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 19:40:48 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 19:40:51 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 19:40:54 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 19:40:57 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 19:40:58 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 19:41:01 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 19:41:04 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 19:41:06 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 19:41:09 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 19:41:12 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 19:41:13 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 19:41:15 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 19:41:16 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 19:41:19 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 19:41:22 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 19:41:25 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 19:41:48 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 19:42:07 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 19:42:16 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 19:42:25 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 19:42:33 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 19:42:40 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 19:42:49 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 19:42:59 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 19:43:07 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 19:43:14 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 19:43:22 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 19:43:22 INFO mapred.JobClient: Job complete: job_201703161917_0006
17/03/16 19:43:22 INFO mapred.JobClient: Counters: 30
17/03/16 19:43:22 INFO mapred.JobClient:   Job Counters
17/03/16 19:43:22 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 19:43:22 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=884723
17/03/16 19:43:22 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 19:43:22 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 19:43:22 INFO mapred.JobClient:     Launched map tasks=243
17/03/16 19:43:22 INFO mapred.JobClient:     Data-local map tasks=243
17/03/16 19:43:22 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1492027
17/03/16 19:43:22 INFO mapred.JobClient:   File Input Format Counters
17/03/16 19:43:22 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 19:43:22 INFO mapred.JobClient:   File Output Format Counters
17/03/16 19:43:22 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 19:43:22 INFO mapred.JobClient:   FileSystemCounters
17/03/16 19:43:22 INFO mapred.JobClient:     FILE_BYTES_READ=94541381015
17/03/16 19:43:22 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 19:43:22 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126800753064
17/03/16 19:43:22 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 19:43:22 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 19:43:22 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 19:43:22 INFO mapred.JobClient:     Map input records=3068055
17/03/16 19:43:22 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 19:43:22 INFO mapred.JobClient:     Spilled Records=12060695
17/03/16 19:43:22 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 19:43:22 INFO mapred.JobClient:     Total committed heap usage (bytes)=49350180864
17/03/16 19:43:22 INFO mapred.JobClient:     CPU time spent (ms)=1600590
17/03/16 19:43:22 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 19:43:22 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 19:43:22 INFO mapred.JobClient:     Combine input records=0
17/03/16 19:43:22 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 19:43:22 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 19:43:22 INFO mapred.JobClient:     Combine output records=0
17/03/16 19:43:22 INFO mapred.JobClient:     Physical memory (bytes) snapshot=53120778240
17/03/16 19:43:22 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 19:43:22 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196348174336
17/03/16 19:43:22 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 19:43:22 UTC 2017
The job took 332 seconds.
```

## Disk stress (script provided on one node)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 19:51:49 UTC 2017
17/03/16 19:51:49 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 19:51:50 INFO mapred.JobClient: Running job: job_201703161917_0008
17/03/16 19:51:51 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 19:51:57 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 19:52:00 INFO mapred.JobClient:  map 4% reduce 0%
17/03/16 19:52:01 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 19:52:03 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 19:52:04 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 19:52:07 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 19:52:09 INFO mapred.JobClient: Task Id : attempt_201703161917_0008_r_000000_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:52:09 INFO mapred.JobClient: Task Id : attempt_201703161917_0008_r_000003_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:52:09 INFO mapred.JobClient: Task Id : attempt_201703161917_0008_r_000004_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:52:10 INFO mapred.JobClient:  map 11% reduce 0%
17/03/16 19:52:11 INFO mapred.JobClient:  map 12% reduce 1%
17/03/16 19:52:14 INFO mapred.JobClient:  map 15% reduce 1%
17/03/16 19:52:17 INFO mapred.JobClient:  map 16% reduce 1%
17/03/16 19:52:18 INFO mapred.JobClient:  map 17% reduce 1%
17/03/16 19:52:18 INFO mapred.JobClient: Task Id : attempt_201703161917_0008_r_000000_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:52:19 INFO mapred.JobClient: Task Id : attempt_201703161917_0008_r_000003_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:52:20 INFO mapred.JobClient:  map 18% reduce 2%
17/03/16 19:52:21 INFO mapred.JobClient:  map 19% reduce 2%
17/03/16 19:52:24 INFO mapred.JobClient:  map 21% reduce 3%
17/03/16 19:52:25 INFO mapred.JobClient:  map 22% reduce 3%
17/03/16 19:52:27 INFO mapred.JobClient:  map 23% reduce 4%
17/03/16 19:52:28 INFO mapred.JobClient:  map 24% reduce 4%
17/03/16 19:52:30 INFO mapred.JobClient:  map 24% reduce 5%
17/03/16 19:52:31 INFO mapred.JobClient:  map 27% reduce 5%
17/03/16 19:52:32 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 19:52:33 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 19:52:34 INFO mapred.JobClient:  map 28% reduce 7%
17/03/16 19:52:35 INFO mapred.JobClient:  map 29% reduce 7%
17/03/16 19:52:36 INFO mapred.JobClient:  map 29% reduce 8%
17/03/16 19:52:38 INFO mapred.JobClient:  map 31% reduce 8%
17/03/16 19:52:39 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 19:52:42 INFO mapred.JobClient:  map 34% reduce 9%
17/03/16 19:52:45 INFO mapred.JobClient:  map 36% reduce 10%
17/03/16 19:52:47 INFO mapred.JobClient:  map 37% reduce 10%
17/03/16 19:52:48 INFO mapred.JobClient:  map 38% reduce 11%
17/03/16 19:52:50 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 19:52:52 INFO mapred.JobClient:  map 41% reduce 12%
17/03/16 19:52:56 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 19:52:57 INFO mapred.JobClient:  map 43% reduce 12%
17/03/16 19:52:58 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 19:53:02 INFO mapred.JobClient:  map 46% reduce 14%
17/03/16 19:53:03 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 19:53:05 INFO mapred.JobClient:  map 48% reduce 14%
17/03/16 19:53:06 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 19:53:08 INFO mapred.JobClient:  map 49% reduce 15%
17/03/16 19:53:09 INFO mapred.JobClient:  map 50% reduce 15%
17/03/16 19:53:10 INFO mapred.JobClient:  map 52% reduce 15%
17/03/16 19:53:11 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 19:53:13 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 19:53:14 INFO mapred.JobClient:  map 54% reduce 17%
17/03/16 19:53:16 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 19:53:17 INFO mapred.JobClient:  map 56% reduce 17%
17/03/16 19:53:18 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 19:53:19 INFO mapred.JobClient:  map 58% reduce 17%
17/03/16 19:53:21 INFO mapred.JobClient:  map 59% reduce 17%
17/03/16 19:53:22 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 19:53:23 INFO mapred.JobClient:  map 60% reduce 19%
17/03/16 19:53:24 INFO mapred.JobClient:  map 61% reduce 19%
17/03/16 19:53:26 INFO mapred.JobClient:  map 63% reduce 19%
17/03/16 19:53:29 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 19:53:30 INFO mapred.JobClient:  map 66% reduce 19%
17/03/16 19:53:31 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 19:53:32 INFO mapred.JobClient:  map 66% reduce 21%
17/03/16 19:53:33 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 19:53:35 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 19:53:36 INFO mapred.JobClient:  map 69% reduce 21%
17/03/16 19:53:37 INFO mapred.JobClient:  map 70% reduce 21%
17/03/16 19:53:38 INFO mapred.JobClient:  map 70% reduce 22%
17/03/16 19:53:39 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 19:53:40 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 19:53:42 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 19:53:43 INFO mapred.JobClient:  map 74% reduce 22%
17/03/16 19:53:45 INFO mapred.JobClient:  map 76% reduce 23%
17/03/16 19:53:47 INFO mapred.JobClient:  map 76% reduce 24%
17/03/16 19:53:48 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 19:53:49 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 19:53:50 INFO mapred.JobClient:  map 79% reduce 24%
17/03/16 19:53:52 INFO mapred.JobClient:  map 80% reduce 24%
17/03/16 19:53:53 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 19:53:54 INFO mapred.JobClient:  map 81% reduce 25%
17/03/16 19:53:55 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 19:53:57 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 19:53:58 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 19:53:59 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 19:54:01 INFO mapred.JobClient:  map 86% reduce 27%
17/03/16 19:54:02 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 19:54:04 INFO mapred.JobClient:  map 88% reduce 27%
17/03/16 19:54:06 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 19:54:07 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 19:54:08 INFO mapred.JobClient:  map 91% reduce 28%
17/03/16 19:54:09 INFO mapred.JobClient:  map 92% reduce 28%
17/03/16 19:54:11 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 19:54:12 INFO mapred.JobClient:  map 94% reduce 29%
17/03/16 19:54:13 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 19:54:15 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 19:54:16 INFO mapred.JobClient:  map 97% reduce 30%
17/03/16 19:54:18 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 19:54:19 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 19:54:20 INFO mapred.JobClient:  map 99% reduce 31%
17/03/16 19:54:21 INFO mapred.JobClient:  map 99% reduce 32%
17/03/16 19:54:23 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 19:54:27 INFO mapred.JobClient:  map 100% reduce 33%
17/03/16 19:54:30 INFO mapred.JobClient:  map 100% reduce 39%
17/03/16 19:54:31 INFO mapred.JobClient:  map 100% reduce 46%
17/03/16 19:54:33 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 19:54:35 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 19:54:39 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 19:54:42 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 19:54:42 INFO mapred.JobClient: Task Id : attempt_201703161917_0008_r_000001_1, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 19:54:45 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 19:54:48 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 19:54:51 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 19:54:54 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 19:54:57 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 19:55:00 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 19:55:01 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 19:55:03 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 19:55:06 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 19:55:07 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 19:55:09 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 19:55:12 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 19:55:22 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 19:55:33 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 19:55:37 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 19:56:07 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 19:56:27 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 19:56:39 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 19:56:43 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 19:56:46 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 19:56:52 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 19:57:04 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 19:57:16 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 19:57:28 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 19:57:40 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 19:57:50 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 19:57:58 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 19:57:59 INFO mapred.JobClient: Job complete: job_201703161917_0008
17/03/16 19:57:59 INFO mapred.JobClient: Counters: 30
17/03/16 19:57:59 INFO mapred.JobClient:   Job Counters
17/03/16 19:57:59 INFO mapred.JobClient:     Launched reduce tasks=11
17/03/16 19:57:59 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=856634
17/03/16 19:57:59 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 19:57:59 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 19:57:59 INFO mapred.JobClient:     Launched map tasks=243
17/03/16 19:57:59 INFO mapred.JobClient:     Data-local map tasks=243
17/03/16 19:57:59 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1679777
17/03/16 19:57:59 INFO mapred.JobClient:   File Input Format Counters
17/03/16 19:57:59 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 19:57:59 INFO mapred.JobClient:   File Output Format Counters
17/03/16 19:57:59 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 19:57:59 INFO mapred.JobClient:   FileSystemCounters
17/03/16 19:57:59 INFO mapred.JobClient:     FILE_BYTES_READ=94420983251
17/03/16 19:57:59 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 19:57:59 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126680355300
17/03/16 19:57:59 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 19:57:59 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 19:57:59 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 19:57:59 INFO mapred.JobClient:     Map input records=3068055
17/03/16 19:57:59 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 19:57:59 INFO mapred.JobClient:     Spilled Records=12049510
17/03/16 19:57:59 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 19:57:59 INFO mapred.JobClient:     Total committed heap usage (bytes)=49323966464
17/03/16 19:57:59 INFO mapred.JobClient:     CPU time spent (ms)=1544580
17/03/16 19:57:59 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 19:57:59 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 19:57:59 INFO mapred.JobClient:     Combine input records=0
17/03/16 19:57:59 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 19:57:59 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 19:57:59 INFO mapred.JobClient:     Combine output records=0
17/03/16 19:57:59 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52978593792
17/03/16 19:57:59 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 19:57:59 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=197071351808
17/03/16 19:57:59 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 19:57:59 UTC 2017
The job took 369 seconds.
```

## Death during map (20%)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 20:03:24 UTC 2017
17/03/16 20:03:24 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 20:03:24 INFO mapred.JobClient: Running job: job_201703161917_0009
17/03/16 20:03:25 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 20:03:31 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 20:03:34 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 20:03:37 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 20:03:38 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 20:03:40 INFO mapred.JobClient:  map 8% reduce 0%
17/03/16 20:03:41 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 20:03:43 INFO mapred.JobClient: Task Id : attempt_201703161917_0009_r_000003_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 20:03:43 INFO mapred.JobClient: Task Id : attempt_201703161917_0009_r_000004_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 20:03:45 INFO mapred.JobClient:  map 12% reduce 0%
17/03/16 20:03:45 INFO mapred.JobClient: Task Id : attempt_201703161917_0009_r_000002_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 20:03:46 INFO mapred.JobClient:  map 12% reduce 1%
17/03/16 20:03:48 INFO mapred.JobClient:  map 13% reduce 1%
17/03/16 20:03:49 INFO mapred.JobClient:  map 15% reduce 1%
17/03/16 20:03:52 INFO mapred.JobClient:  map 16% reduce 1%
17/03/16 20:03:55 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 20:03:56 INFO mapred.JobClient:  map 18% reduce 2%
17/03/16 20:03:58 INFO mapred.JobClient:  map 18% reduce 3%
17/03/16 20:03:59 INFO mapred.JobClient:  map 19% reduce 3%
17/03/16 20:04:02 INFO mapred.JobClient:  map 21% reduce 3%
17/03/16 20:04:05 INFO mapred.JobClient:  map 22% reduce 3%
17/03/16 20:04:06 INFO mapred.JobClient:  map 23% reduce 3%
17/03/16 20:04:07 INFO mapred.JobClient:  map 23% reduce 4%
17/03/16 20:04:09 INFO mapred.JobClient:  map 24% reduce 4%
17/03/16 20:04:12 INFO mapred.JobClient:  map 26% reduce 4%
17/03/16 20:04:15 INFO mapred.JobClient:  map 27% reduce 4%
17/03/16 20:04:17 INFO mapred.JobClient:  map 28% reduce 4%
17/03/16 20:04:19 INFO mapred.JobClient:  map 29% reduce 5%
17/03/16 20:04:22 INFO mapred.JobClient:  map 30% reduce 5%
17/03/16 20:04:26 INFO mapred.JobClient:  map 32% reduce 5%
17/03/16 20:04:30 INFO mapred.JobClient:  map 34% reduce 6%
17/03/16 20:04:34 INFO mapred.JobClient:  map 35% reduce 6%
17/03/16 20:04:36 INFO mapred.JobClient:  map 36% reduce 6%
17/03/16 20:04:37 INFO mapred.JobClient:  map 37% reduce 6%
17/03/16 20:04:40 INFO mapred.JobClient:  map 38% reduce 7%
17/03/16 20:04:41 INFO mapred.JobClient:  map 39% reduce 7%
17/03/16 20:04:44 INFO mapred.JobClient:  map 40% reduce 7%
17/03/16 20:04:47 INFO mapred.JobClient:  map 41% reduce 7%
17/03/16 20:04:48 INFO mapred.JobClient:  map 42% reduce 7%
17/03/16 20:04:50 INFO mapred.JobClient:  map 43% reduce 7%
17/03/16 20:04:51 INFO mapred.JobClient:  map 43% reduce 8%
17/03/16 20:04:52 INFO mapred.JobClient:  map 44% reduce 8%
17/03/16 20:04:54 INFO mapred.JobClient:  map 45% reduce 8%
17/03/16 20:04:58 INFO mapred.JobClient:  map 47% reduce 8%
17/03/16 20:05:01 INFO mapred.JobClient:  map 47% reduce 9%
17/03/16 20:05:02 INFO mapred.JobClient:  map 49% reduce 9%
17/03/16 20:05:05 INFO mapred.JobClient:  map 50% reduce 9%
17/03/16 20:05:08 INFO mapred.JobClient:  map 51% reduce 9%
17/03/16 20:05:09 INFO mapred.JobClient:  map 52% reduce 9%
17/03/16 20:05:12 INFO mapred.JobClient:  map 52% reduce 10%
17/03/16 20:05:13 INFO mapred.JobClient:  map 54% reduce 10%
17/03/16 20:05:16 INFO mapred.JobClient:  map 55% reduce 10%
17/03/16 20:05:18 INFO mapred.JobClient:  map 56% reduce 10%
17/03/16 20:05:20 INFO mapred.JobClient:  map 57% reduce 10%
17/03/16 20:05:24 INFO mapred.JobClient:  map 59% reduce 10%
17/03/16 20:05:25 INFO mapred.JobClient:  map 59% reduce 11%
17/03/16 20:05:28 INFO mapred.JobClient:  map 61% reduce 11%
17/03/16 20:05:31 INFO mapred.JobClient:  map 62% reduce 11%
17/03/16 20:05:34 INFO mapred.JobClient:  map 63% reduce 11%
17/03/16 20:05:35 INFO mapred.JobClient:  map 64% reduce 12%
17/03/16 20:05:38 INFO mapred.JobClient:  map 65% reduce 12%
17/03/16 20:05:39 INFO mapred.JobClient:  map 66% reduce 12%
17/03/16 20:05:42 INFO mapred.JobClient:  map 67% reduce 12%
17/03/16 20:05:43 INFO mapred.JobClient:  map 67% reduce 13%
17/03/16 20:05:45 INFO mapred.JobClient:  map 68% reduce 13%
17/03/16 20:05:46 INFO mapred.JobClient:  map 69% reduce 13%
17/03/16 20:05:50 INFO mapred.JobClient:  map 71% reduce 13%
17/03/16 20:05:53 INFO mapred.JobClient:  map 72% reduce 13%
17/03/16 20:05:55 INFO mapred.JobClient:  map 72% reduce 14%
17/03/16 20:05:56 INFO mapred.JobClient:  map 73% reduce 14%
17/03/16 20:05:57 INFO mapred.JobClient:  map 74% reduce 14%
17/03/16 20:06:00 INFO mapred.JobClient:  map 75% reduce 14%
17/03/16 20:06:01 INFO mapred.JobClient:  map 76% reduce 14%
17/03/16 20:06:04 INFO mapred.JobClient:  map 77% reduce 14%
17/03/16 20:06:08 INFO mapred.JobClient:  map 79% reduce 15%
17/03/16 20:06:11 INFO mapred.JobClient:  map 80% reduce 15%
17/03/16 20:06:12 INFO mapred.JobClient:  map 81% reduce 15%
17/03/16 20:06:16 INFO mapred.JobClient:  map 82% reduce 15%
17/03/16 20:06:18 INFO mapred.JobClient:  map 82% reduce 16%
17/03/16 20:06:19 INFO mapred.JobClient:  map 83% reduce 16%
17/03/16 20:06:20 INFO mapred.JobClient:  map 84% reduce 16%
17/03/16 20:06:23 INFO mapred.JobClient:  map 85% reduce 16%
17/03/16 20:06:25 INFO mapred.JobClient:  map 86% reduce 16%
17/03/16 20:06:27 INFO mapred.JobClient:  map 87% reduce 16%
17/03/16 20:06:31 INFO mapred.JobClient:  map 89% reduce 16%
17/03/16 20:06:32 INFO mapred.JobClient:  map 89% reduce 17%
17/03/16 20:06:35 INFO mapred.JobClient:  map 90% reduce 17%
17/03/16 20:06:36 INFO mapred.JobClient:  map 91% reduce 17%
17/03/16 20:06:39 INFO mapred.JobClient:  map 92% reduce 17%
17/03/16 20:06:41 INFO mapred.JobClient:  map 93% reduce 17%
17/03/16 20:06:42 INFO mapred.JobClient:  map 94% reduce 17%
17/03/16 20:06:44 INFO mapred.JobClient:  map 94% reduce 18%
17/03/16 20:06:46 INFO mapred.JobClient:  map 96% reduce 18%
17/03/16 20:06:49 INFO mapred.JobClient:  map 97% reduce 18%
17/03/16 20:06:51 INFO mapred.JobClient:  map 98% reduce 19%
17/03/16 20:06:53 INFO mapred.JobClient:  map 99% reduce 19%
17/03/16 20:06:54 INFO mapred.JobClient:  map 100% reduce 19%
17/03/16 20:14:42 INFO mapred.JobClient:  map 98% reduce 19%
17/03/16 20:14:48 INFO mapred.JobClient:  map 99% reduce 19%
17/03/16 20:14:49 INFO mapred.JobClient:  map 98% reduce 19%
17/03/16 20:14:52 INFO mapred.JobClient:  map 99% reduce 19%
17/03/16 20:14:53 INFO mapred.JobClient:  map 100% reduce 19%
17/03/16 20:14:55 INFO mapred.JobClient:  map 100% reduce 20%
17/03/16 20:14:58 INFO mapred.JobClient:  map 100% reduce 21%
17/03/16 20:15:00 INFO mapred.JobClient:  map 100% reduce 28%
17/03/16 20:15:01 INFO mapred.JobClient:  map 100% reduce 36%
17/03/16 20:15:03 INFO mapred.JobClient:  map 100% reduce 43%
17/03/16 20:15:04 INFO mapred.JobClient:  map 100% reduce 45%
17/03/16 20:15:06 INFO mapred.JobClient:  map 100% reduce 46%
17/03/16 20:15:07 INFO mapred.JobClient:  map 100% reduce 47%
17/03/16 20:15:09 INFO mapred.JobClient:  map 100% reduce 48%
17/03/16 20:15:10 INFO mapred.JobClient:  map 100% reduce 49%
17/03/16 20:15:12 INFO mapred.JobClient:  map 100% reduce 50%
17/03/16 20:15:13 INFO mapred.JobClient:  map 100% reduce 51%
17/03/16 20:15:15 INFO mapred.JobClient:  map 100% reduce 52%
17/03/16 20:15:16 INFO mapred.JobClient:  map 100% reduce 53%
17/03/16 20:15:19 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 20:15:21 INFO mapred.JobClient:  map 100% reduce 55%
17/03/16 20:15:22 INFO mapred.JobClient:  map 100% reduce 56%
17/03/16 20:15:25 INFO mapred.JobClient:  map 100% reduce 58%
17/03/16 20:15:28 INFO mapred.JobClient:  map 100% reduce 59%
17/03/16 20:15:31 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 20:15:34 INFO mapred.JobClient:  map 100% reduce 62%
17/03/16 20:15:35 INFO mapred.JobClient:  map 100% reduce 63%
17/03/16 20:15:37 INFO mapred.JobClient:  map 100% reduce 64%
17/03/16 20:15:38 INFO mapred.JobClient:  map 100% reduce 65%
17/03/16 20:15:40 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 20:15:44 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 20:15:47 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 20:15:49 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 20:15:52 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 20:15:55 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 20:15:56 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 20:15:59 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 20:16:02 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 20:16:04 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 20:16:07 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 20:16:10 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 20:16:13 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 20:16:17 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 20:16:22 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 20:16:23 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 20:16:40 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 20:16:49 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 20:16:58 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 20:17:05 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 20:17:11 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 20:17:20 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 20:17:27 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 20:17:33 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 20:17:33 INFO mapred.JobClient: Job complete: job_201703161917_0009
17/03/16 20:17:33 INFO mapred.JobClient: Counters: 30
17/03/16 20:17:33 INFO mapred.JobClient:   Job Counters
17/03/16 20:17:33 INFO mapred.JobClient:     Launched reduce tasks=11
17/03/16 20:17:33 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=868438
17/03/16 20:17:33 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 20:17:33 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 20:17:33 INFO mapred.JobClient:     Launched map tasks=255
17/03/16 20:17:33 INFO mapred.JobClient:     Data-local map tasks=255
17/03/16 20:17:33 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=2411303
17/03/16 20:17:33 INFO mapred.JobClient:   File Input Format Counters
17/03/16 20:17:33 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 20:17:33 INFO mapred.JobClient:   File Output Format Counters
17/03/16 20:17:33 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 20:17:33 INFO mapred.JobClient:   FileSystemCounters
17/03/16 20:17:33 INFO mapred.JobClient:     FILE_BYTES_READ=94530972839
17/03/16 20:17:33 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 20:17:33 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126790344888
17/03/16 20:17:33 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 20:17:33 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 20:17:33 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 20:17:33 INFO mapred.JobClient:     Map input records=3068055
17/03/16 20:17:33 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 20:17:33 INFO mapred.JobClient:     Spilled Records=12060214
17/03/16 20:17:33 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 20:17:33 INFO mapred.JobClient:     Total committed heap usage (bytes)=49356996608
17/03/16 20:17:33 INFO mapred.JobClient:     CPU time spent (ms)=1501670
17/03/16 20:17:33 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 20:17:33 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 20:17:33 INFO mapred.JobClient:     Combine input records=0
17/03/16 20:17:33 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 20:17:33 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 20:17:33 INFO mapred.JobClient:     Combine output records=0
17/03/16 20:17:33 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52941742080
17/03/16 20:17:33 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 20:17:33 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=197169147904
17/03/16 20:17:33 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 20:17:33 UTC 2017
The job took 849 seconds.
```

## Death during map (20%) with expiry interval of 30s
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 21:49:23 UTC 2017
17/03/16 21:49:23 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 21:49:24 INFO mapred.JobClient: Running job: job_201703162147_0001
17/03/16 21:49:25 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 21:49:32 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 21:49:34 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 21:49:35 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 21:49:38 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 21:49:41 INFO mapred.JobClient:  map 8% reduce 0%
17/03/16 21:49:42 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 21:49:45 INFO mapred.JobClient:  map 12% reduce 1%
17/03/16 21:49:46 INFO mapred.JobClient:  map 12% reduce 3%
17/03/16 21:49:48 INFO mapred.JobClient:  map 14% reduce 3%
17/03/16 21:49:49 INFO mapred.JobClient:  map 15% reduce 3%
17/03/16 21:49:52 INFO mapred.JobClient:  map 17% reduce 3%
17/03/16 21:49:55 INFO mapred.JobClient:  map 19% reduce 5%
17/03/16 21:49:58 INFO mapred.JobClient:  map 20% reduce 5%
17/03/16 21:49:59 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 21:50:02 INFO mapred.JobClient:  map 23% reduce 5%
17/03/16 21:50:03 INFO mapred.JobClient:  map 24% reduce 5%
17/03/16 21:50:06 INFO mapred.JobClient:  map 25% reduce 6%
17/03/16 21:50:08 INFO mapred.JobClient:  map 26% reduce 6%
17/03/16 21:50:09 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 21:50:13 INFO mapred.JobClient:  map 29% reduce 7%
17/03/16 21:50:16 INFO mapred.JobClient:  map 30% reduce 7%
17/03/16 21:50:19 INFO mapred.JobClient:  map 32% reduce 7%
17/03/16 21:50:23 INFO mapred.JobClient:  map 33% reduce 7%
17/03/16 21:50:24 INFO mapred.JobClient:  map 34% reduce 7%
17/03/16 21:50:25 INFO mapred.JobClient:  map 34% reduce 8%
17/03/16 21:50:27 INFO mapred.JobClient:  map 35% reduce 8%
17/03/16 21:50:30 INFO mapred.JobClient:  map 36% reduce 8%
17/03/16 21:50:31 INFO mapred.JobClient:  map 37% reduce 9%
17/03/16 21:50:34 INFO mapred.JobClient:  map 39% reduce 9%
17/03/16 21:50:37 INFO mapred.JobClient:  map 39% reduce 7%
17/03/16 21:50:47 INFO mapred.JobClient:  map 39% reduce 8%
17/03/16 21:50:54 INFO mapred.JobClient:  map 39% reduce 9%
17/03/16 21:50:56 INFO mapred.JobClient:  map 40% reduce 9%
17/03/16 21:50:57 INFO mapred.JobClient:  map 41% reduce 10%
17/03/16 21:50:59 INFO mapred.JobClient:  map 42% reduce 10%
17/03/16 21:51:03 INFO mapred.JobClient:  map 44% reduce 10%
17/03/16 21:51:04 INFO mapred.JobClient:  map 44% reduce 11%
17/03/16 21:51:06 INFO mapred.JobClient:  map 45% reduce 11%
17/03/16 21:51:08 INFO mapred.JobClient:  map 46% reduce 11%
17/03/16 21:51:09 INFO mapred.JobClient:  map 47% reduce 11%
17/03/16 21:51:13 INFO mapred.JobClient:  map 49% reduce 12%
17/03/16 21:51:17 INFO mapred.JobClient:  map 50% reduce 12%
17/03/16 21:51:18 INFO mapred.JobClient:  map 51% reduce 12%
17/03/16 21:51:19 INFO mapred.JobClient:  map 51% reduce 13%
17/03/16 21:51:21 INFO mapred.JobClient:  map 52% reduce 13%
17/03/16 21:51:24 INFO mapred.JobClient:  map 53% reduce 13%
17/03/16 21:51:25 INFO mapred.JobClient:  map 54% reduce 13%
17/03/16 21:51:28 INFO mapred.JobClient:  map 55% reduce 14%
17/03/16 21:51:31 INFO mapred.JobClient:  map 57% reduce 14%
17/03/16 21:51:36 INFO mapred.JobClient:  map 58% reduce 15%
17/03/16 21:51:37 INFO mapred.JobClient:  map 59% reduce 15%
17/03/16 21:51:40 INFO mapred.JobClient:  map 60% reduce 15%
17/03/16 21:51:42 INFO mapred.JobClient:  map 61% reduce 15%
17/03/16 21:51:44 INFO mapred.JobClient:  map 62% reduce 15%
17/03/16 21:51:46 INFO mapred.JobClient:  map 62% reduce 16%
17/03/16 21:51:47 INFO mapred.JobClient:  map 63% reduce 16%
17/03/16 21:51:48 INFO mapred.JobClient:  map 64% reduce 16%
17/03/16 21:51:50 INFO mapred.JobClient:  map 65% reduce 16%
17/03/16 21:51:52 INFO mapred.JobClient:  map 66% reduce 17%
17/03/16 21:51:55 INFO mapred.JobClient:  map 67% reduce 17%
17/03/16 21:51:58 INFO mapred.JobClient:  map 68% reduce 17%
17/03/16 21:51:59 INFO mapred.JobClient:  map 69% reduce 17%
17/03/16 21:52:02 INFO mapred.JobClient:  map 70% reduce 17%
17/03/16 21:52:03 INFO mapred.JobClient:  map 71% reduce 17%
17/03/16 21:52:05 INFO mapred.JobClient:  map 72% reduce 18%
17/03/16 21:52:08 INFO mapred.JobClient:  map 73% reduce 18%
17/03/16 21:52:09 INFO mapred.JobClient:  map 74% reduce 18%
17/03/16 21:52:10 INFO mapred.JobClient:  map 74% reduce 19%
17/03/16 21:52:12 INFO mapred.JobClient:  map 75% reduce 19%
17/03/16 21:52:14 INFO mapred.JobClient:  map 76% reduce 19%
17/03/16 21:52:16 INFO mapred.JobClient:  map 77% reduce 19%
17/03/16 21:52:17 INFO mapred.JobClient:  map 77% reduce 20%
17/03/16 21:52:19 INFO mapred.JobClient:  map 78% reduce 20%
17/03/16 21:52:20 INFO mapred.JobClient:  map 79% reduce 20%
17/03/16 21:52:23 INFO mapred.JobClient:  map 80% reduce 20%
17/03/16 21:52:24 INFO mapred.JobClient:  map 81% reduce 20%
17/03/16 21:52:25 INFO mapred.JobClient:  map 81% reduce 21%
17/03/16 21:52:27 INFO mapred.JobClient:  map 82% reduce 21%
17/03/16 21:52:30 INFO mapred.JobClient:  map 83% reduce 21%
17/03/16 21:52:31 INFO mapred.JobClient:  map 84% reduce 21%
17/03/16 21:52:34 INFO mapred.JobClient:  map 86% reduce 21%
17/03/16 21:52:35 INFO mapred.JobClient:  map 86% reduce 22%
17/03/16 21:52:37 INFO mapred.JobClient:  map 87% reduce 22%
17/03/16 21:52:41 INFO mapred.JobClient:  map 89% reduce 23%
17/03/16 21:52:44 INFO mapred.JobClient:  map 90% reduce 23%
17/03/16 21:52:46 INFO mapred.JobClient:  map 91% reduce 23%
17/03/16 21:52:50 INFO mapred.JobClient:  map 92% reduce 24%
17/03/16 21:52:51 INFO mapred.JobClient:  map 93% reduce 24%
17/03/16 21:52:54 INFO mapred.JobClient:  map 94% reduce 24%
17/03/16 21:52:56 INFO mapred.JobClient:  map 95% reduce 24%
17/03/16 21:52:57 INFO mapred.JobClient:  map 96% reduce 24%
17/03/16 21:52:59 INFO mapred.JobClient:  map 96% reduce 25%
17/03/16 21:53:00 INFO mapred.JobClient:  map 97% reduce 25%
17/03/16 21:53:02 INFO mapred.JobClient:  map 98% reduce 25%
17/03/16 21:53:04 INFO mapred.JobClient:  map 99% reduce 25%
17/03/16 21:53:06 INFO mapred.JobClient:  map 100% reduce 25%
17/03/16 21:53:08 INFO mapred.JobClient:  map 100% reduce 26%
17/03/16 21:53:13 INFO mapred.JobClient:  map 100% reduce 40%
17/03/16 21:53:14 INFO mapred.JobClient:  map 100% reduce 53%
17/03/16 21:53:16 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 21:53:18 INFO mapred.JobClient:  map 100% reduce 55%
17/03/16 21:53:22 INFO mapred.JobClient:  map 100% reduce 56%
17/03/16 21:53:23 INFO mapred.JobClient:  map 100% reduce 57%
17/03/16 21:53:25 INFO mapred.JobClient:  map 100% reduce 58%
17/03/16 21:53:27 INFO mapred.JobClient:  map 100% reduce 59%
17/03/16 21:53:28 INFO mapred.JobClient:  map 100% reduce 60%
17/03/16 21:53:30 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 21:53:33 INFO mapred.JobClient:  map 100% reduce 62%
17/03/16 21:53:35 INFO mapred.JobClient:  map 100% reduce 63%
17/03/16 21:53:36 INFO mapred.JobClient:  map 100% reduce 64%
17/03/16 21:53:39 INFO mapred.JobClient:  map 100% reduce 65%
17/03/16 21:53:40 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 21:53:42 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 21:53:44 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 21:53:46 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 21:53:49 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 21:53:50 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 21:53:52 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 21:53:55 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 21:54:04 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 21:54:10 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 21:54:19 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 21:54:27 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 21:54:35 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 21:54:43 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 21:54:49 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 21:54:55 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 21:55:01 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 21:55:04 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 21:55:11 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 21:55:14 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 21:55:20 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 21:55:26 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 21:55:32 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 21:55:35 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 21:55:41 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 21:55:56 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 21:56:15 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 21:56:30 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 21:56:47 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 21:56:50 INFO mapred.JobClient: Job complete: job_201703162147_0001
17/03/16 21:56:50 INFO mapred.JobClient: Counters: 30
17/03/16 21:56:50 INFO mapred.JobClient:   Job Counters
17/03/16 21:56:50 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 21:56:50 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=893074
17/03/16 21:56:50 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 21:56:50 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 21:56:50 INFO mapred.JobClient:     Launched map tasks=261
17/03/16 21:56:50 INFO mapred.JobClient:     Data-local map tasks=261
17/03/16 21:56:50 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1299385
17/03/16 21:56:50 INFO mapred.JobClient:   File Input Format Counters
17/03/16 21:56:50 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 21:56:50 INFO mapred.JobClient:   File Output Format Counters
17/03/16 21:56:50 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 21:56:50 INFO mapred.JobClient:   FileSystemCounters
17/03/16 21:56:50 INFO mapred.JobClient:     FILE_BYTES_READ=94344933963
17/03/16 21:56:50 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 21:56:50 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126604305767
17/03/16 21:56:50 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 21:56:50 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 21:56:50 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 21:56:50 INFO mapred.JobClient:     Map input records=3068055
17/03/16 21:56:50 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 21:56:50 INFO mapred.JobClient:     Spilled Records=12042680
17/03/16 21:56:50 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 21:56:50 INFO mapred.JobClient:     Total committed heap usage (bytes)=49334452224
17/03/16 21:56:50 INFO mapred.JobClient:     CPU time spent (ms)=1530280
17/03/16 21:56:50 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 21:56:50 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 21:56:50 INFO mapred.JobClient:     Combine input records=0
17/03/16 21:56:50 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 21:56:50 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 21:56:50 INFO mapred.JobClient:     Combine output records=0
17/03/16 21:56:50 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52902445056
17/03/16 21:56:50 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 21:56:50 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=195693166592
17/03/16 21:56:50 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 21:56:50 UTC 2017
The job took 446 seconds.
```

## Death during map (20%) with expiry interval of 60s
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 22:36:00 UTC 2017
17/03/16 22:36:00 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 22:36:00 INFO mapred.JobClient: Running job: job_201703162234_0001
17/03/16 22:36:01 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 22:36:07 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 22:36:10 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 22:36:11 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 22:36:14 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 22:36:17 INFO mapred.JobClient:  map 8% reduce 0%
17/03/16 22:36:18 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 22:36:21 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 22:36:22 INFO mapred.JobClient:  map 12% reduce 3%
17/03/16 22:36:24 INFO mapred.JobClient:  map 14% reduce 3%
17/03/16 22:36:25 INFO mapred.JobClient:  map 15% reduce 3%
17/03/16 22:36:28 INFO mapred.JobClient:  map 17% reduce 3%
17/03/16 22:36:31 INFO mapred.JobClient:  map 19% reduce 5%
17/03/16 22:36:34 INFO mapred.JobClient:  map 20% reduce 5%
17/03/16 22:36:35 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 22:36:37 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 22:36:38 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 22:36:42 INFO mapred.JobClient:  map 25% reduce 6%
17/03/16 22:36:44 INFO mapred.JobClient:  map 26% reduce 6%
17/03/16 22:36:45 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 22:36:48 INFO mapred.JobClient:  map 28% reduce 6%
17/03/16 22:36:49 INFO mapred.JobClient:  map 29% reduce 7%
17/03/16 22:36:52 INFO mapred.JobClient:  map 30% reduce 7%
17/03/16 22:36:55 INFO mapred.JobClient:  map 32% reduce 7%
17/03/16 22:36:59 INFO mapred.JobClient:  map 33% reduce 7%
17/03/16 22:37:00 INFO mapred.JobClient:  map 34% reduce 7%
17/03/16 22:37:01 INFO mapred.JobClient:  map 34% reduce 8%
17/03/16 22:37:03 INFO mapred.JobClient:  map 35% reduce 8%
17/03/16 22:37:05 INFO mapred.JobClient:  map 36% reduce 8%
17/03/16 22:37:06 INFO mapred.JobClient:  map 37% reduce 8%
17/03/16 22:37:09 INFO mapred.JobClient:  map 38% reduce 8%
17/03/16 22:37:11 INFO mapred.JobClient:  map 39% reduce 8%
17/03/16 22:37:13 INFO mapred.JobClient:  map 39% reduce 9%
17/03/16 22:37:14 INFO mapred.JobClient:  map 40% reduce 9%
17/03/16 22:37:15 INFO mapred.JobClient:  map 41% reduce 9%
17/03/16 22:37:18 INFO mapred.JobClient:  map 42% reduce 9%
17/03/16 22:37:21 INFO mapred.JobClient:  map 43% reduce 9%
17/03/16 22:37:22 INFO mapred.JobClient:  map 44% reduce 9%
17/03/16 22:37:24 INFO mapred.JobClient:  map 45% reduce 9%
17/03/16 22:37:25 INFO mapred.JobClient:  map 45% reduce 10%
17/03/16 22:37:26 INFO mapred.JobClient:  map 46% reduce 10%
17/03/16 22:37:28 INFO mapred.JobClient:  map 47% reduce 10%
17/03/16 22:37:32 INFO mapred.JobClient:  map 48% reduce 10%
17/03/16 22:37:33 INFO mapred.JobClient:  map 49% reduce 10%
17/03/16 22:37:34 INFO mapred.JobClient:  map 49% reduce 11%
17/03/16 22:37:36 INFO mapred.JobClient:  map 50% reduce 11%
17/03/16 22:37:37 INFO mapred.JobClient:  map 51% reduce 11%
17/03/16 22:37:40 INFO mapred.JobClient:  map 52% reduce 10%
17/03/16 22:37:54 INFO mapred.JobClient:  map 52% reduce 11%
17/03/16 22:38:00 INFO mapred.JobClient:  map 52% reduce 12%
17/03/16 22:38:02 INFO mapred.JobClient:  map 53% reduce 12%
17/03/16 22:38:04 INFO mapred.JobClient:  map 54% reduce 12%
17/03/16 22:38:05 INFO mapred.JobClient:  map 54% reduce 13%
17/03/16 22:38:06 INFO mapred.JobClient:  map 55% reduce 13%
17/03/16 22:38:08 INFO mapred.JobClient:  map 56% reduce 13%
17/03/16 22:38:09 INFO mapred.JobClient:  map 56% reduce 14%
17/03/16 22:38:10 INFO mapred.JobClient:  map 57% reduce 14%
17/03/16 22:38:12 INFO mapred.JobClient:  map 58% reduce 14%
17/03/16 22:38:15 INFO mapred.JobClient:  map 59% reduce 14%
17/03/16 22:38:16 INFO mapred.JobClient:  map 60% reduce 15%
17/03/16 22:38:19 INFO mapred.JobClient:  map 61% reduce 15%
17/03/16 22:38:21 INFO mapred.JobClient:  map 62% reduce 15%
17/03/16 22:38:23 INFO mapred.JobClient:  map 63% reduce 15%
17/03/16 22:38:25 INFO mapred.JobClient:  map 63% reduce 16%
17/03/16 22:38:27 INFO mapred.JobClient:  map 64% reduce 16%
17/03/16 22:38:28 INFO mapred.JobClient:  map 65% reduce 16%
17/03/16 22:38:30 INFO mapred.JobClient:  map 66% reduce 17%
17/03/16 22:38:31 INFO mapred.JobClient:  map 67% reduce 17%
17/03/16 22:38:34 INFO mapred.JobClient:  map 68% reduce 17%
17/03/16 22:38:37 INFO mapred.JobClient:  map 69% reduce 17%
17/03/16 22:38:38 INFO mapred.JobClient:  map 70% reduce 17%
17/03/16 22:38:40 INFO mapred.JobClient:  map 71% reduce 17%
17/03/16 22:38:41 INFO mapred.JobClient:  map 71% reduce 18%
17/03/16 22:38:42 INFO mapred.JobClient:  map 72% reduce 18%
17/03/16 22:38:45 INFO mapred.JobClient:  map 73% reduce 18%
17/03/16 22:38:47 INFO mapred.JobClient:  map 74% reduce 18%
17/03/16 22:38:49 INFO mapred.JobClient:  map 75% reduce 19%
17/03/16 22:38:50 INFO mapred.JobClient:  map 76% reduce 19%
17/03/16 22:38:52 INFO mapred.JobClient:  map 77% reduce 19%
17/03/16 22:38:56 INFO mapred.JobClient:  map 78% reduce 20%
17/03/16 22:38:58 INFO mapred.JobClient:  map 79% reduce 20%
17/03/16 22:38:59 INFO mapred.JobClient:  map 80% reduce 20%
17/03/16 22:39:02 INFO mapred.JobClient:  map 80% reduce 21%
17/03/16 22:39:03 INFO mapred.JobClient:  map 82% reduce 21%
17/03/16 22:39:06 INFO mapred.JobClient:  map 83% reduce 21%
17/03/16 22:39:10 INFO mapred.JobClient:  map 85% reduce 21%
17/03/16 22:39:11 INFO mapred.JobClient:  map 85% reduce 22%
17/03/16 22:39:13 INFO mapred.JobClient:  map 86% reduce 22%
17/03/16 22:39:14 INFO mapred.JobClient:  map 87% reduce 22%
17/03/16 22:39:17 INFO mapred.JobClient:  map 88% reduce 22%
17/03/16 22:39:18 INFO mapred.JobClient:  map 88% reduce 23%
17/03/16 22:39:21 INFO mapred.JobClient:  map 90% reduce 23%
17/03/16 22:39:24 INFO mapred.JobClient:  map 91% reduce 23%
17/03/16 22:39:25 INFO mapred.JobClient:  map 92% reduce 23%
17/03/16 22:39:28 INFO mapred.JobClient:  map 93% reduce 23%
17/03/16 22:39:29 INFO mapred.JobClient:  map 93% reduce 24%
17/03/16 22:39:31 INFO mapred.JobClient:  map 94% reduce 24%
17/03/16 22:39:32 INFO mapred.JobClient:  map 95% reduce 24%
17/03/16 22:39:35 INFO mapred.JobClient:  map 96% reduce 24%
17/03/16 22:39:36 INFO mapred.JobClient:  map 97% reduce 25%
17/03/16 22:39:39 INFO mapred.JobClient:  map 98% reduce 25%
17/03/16 22:39:41 INFO mapred.JobClient:  map 99% reduce 25%
17/03/16 22:39:42 INFO mapred.JobClient:  map 100% reduce 26%
17/03/16 22:39:47 INFO mapred.JobClient:  map 100% reduce 39%
17/03/16 22:39:50 INFO mapred.JobClient:  map 100% reduce 40%
17/03/16 22:39:51 INFO mapred.JobClient:  map 100% reduce 47%
17/03/16 22:39:52 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 22:39:53 INFO mapred.JobClient:  map 100% reduce 55%
17/03/16 22:39:55 INFO mapred.JobClient:  map 100% reduce 56%
17/03/16 22:39:56 INFO mapred.JobClient:  map 100% reduce 57%
17/03/16 22:39:58 INFO mapred.JobClient:  map 100% reduce 58%
17/03/16 22:39:59 INFO mapred.JobClient:  map 100% reduce 59%
17/03/16 22:40:01 INFO mapred.JobClient:  map 100% reduce 60%
17/03/16 22:40:03 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 22:40:05 INFO mapred.JobClient:  map 100% reduce 62%
17/03/16 22:40:06 INFO mapred.JobClient:  map 100% reduce 63%
17/03/16 22:40:09 INFO mapred.JobClient:  map 100% reduce 64%
17/03/16 22:40:10 INFO mapred.JobClient:  map 100% reduce 65%
17/03/16 22:40:12 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 22:40:13 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 22:40:15 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 22:40:18 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 22:40:19 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 22:40:21 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 22:40:24 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 22:40:27 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 22:40:28 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 22:40:30 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 22:40:33 INFO mapred.JobClient:  map 100% reduce 77%
17/03/16 22:40:34 INFO mapred.JobClient:  map 100% reduce 78%
17/03/16 22:40:45 INFO mapred.JobClient:  map 100% reduce 79%
17/03/16 22:40:55 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 22:40:58 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 22:41:01 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 22:41:04 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 22:41:13 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 22:41:17 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 22:41:20 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 22:41:29 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 22:41:35 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 22:41:38 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 22:41:44 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 22:41:50 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 22:42:05 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 22:42:20 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 22:42:32 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 22:42:34 INFO mapred.JobClient: Job complete: job_201703162234_0001
17/03/16 22:42:34 INFO mapred.JobClient: Counters: 30
17/03/16 22:42:34 INFO mapred.JobClient:   Job Counters
17/03/16 22:42:34 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 22:42:34 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=895595
17/03/16 22:42:34 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 22:42:34 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 22:42:34 INFO mapred.JobClient:     Launched map tasks=262
17/03/16 22:42:34 INFO mapred.JobClient:     Data-local map tasks=262
17/03/16 22:42:34 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1146572
17/03/16 22:42:34 INFO mapred.JobClient:   File Input Format Counters
17/03/16 22:42:34 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 22:42:34 INFO mapred.JobClient:   File Output Format Counters
17/03/16 22:42:34 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 22:42:34 INFO mapred.JobClient:   FileSystemCounters
17/03/16 22:42:34 INFO mapred.JobClient:     FILE_BYTES_READ=94348284774
17/03/16 22:42:34 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 22:42:34 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126607656578
17/03/16 22:42:34 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 22:42:34 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 22:42:34 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 22:42:34 INFO mapred.JobClient:     Map input records=3068055
17/03/16 22:42:34 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 22:42:34 INFO mapred.JobClient:     Spilled Records=12042474
17/03/16 22:42:34 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 22:42:34 INFO mapred.JobClient:     Total committed heap usage (bytes)=49353326592
17/03/16 22:42:34 INFO mapred.JobClient:     CPU time spent (ms)=1536360
17/03/16 22:42:34 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 22:42:34 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 22:42:34 INFO mapred.JobClient:     Combine input records=0
17/03/16 22:42:34 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 22:42:34 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 22:42:34 INFO mapred.JobClient:     Combine output records=0
17/03/16 22:42:34 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52913545216
17/03/16 22:42:34 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 22:42:34 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=197277163520
17/03/16 22:42:34 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 22:42:34 UTC 2017
The job took 394 seconds.
```

## Death after map (reduce 32%)
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 20:20:11 UTC 2017
17/03/16 20:20:11 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 20:20:12 INFO mapred.JobClient: Running job: job_201703162019_0001
17/03/16 20:20:13 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 20:20:19 INFO mapred.JobClient:  map 1% reduce 0%
17/03/16 20:20:20 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 20:20:22 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 20:20:23 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 20:20:26 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 20:20:29 INFO mapred.JobClient:  map 9% reduce 0%
17/03/16 20:20:30 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 20:20:32 INFO mapred.JobClient: Task Id : attempt_201703162019_0001_r_000002_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 20:20:33 INFO mapred.JobClient:  map 12% reduce 0%
17/03/16 20:20:33 INFO mapred.JobClient: Task Id : attempt_201703162019_0001_r_000000_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 20:20:34 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 20:20:36 INFO mapred.JobClient:  map 14% reduce 2%
17/03/16 20:20:37 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 20:20:40 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 20:20:43 INFO mapred.JobClient:  map 19% reduce 3%
17/03/16 20:20:44 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 20:20:46 INFO mapred.JobClient:  map 20% reduce 4%
17/03/16 20:20:47 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 20:20:49 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 20:20:50 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 20:20:53 INFO mapred.JobClient:  map 26% reduce 6%
17/03/16 20:20:54 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 20:20:55 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 20:20:56 INFO mapred.JobClient:  map 27% reduce 8%
17/03/16 20:20:57 INFO mapred.JobClient:  map 29% reduce 8%
17/03/16 20:21:00 INFO mapred.JobClient:  map 31% reduce 8%
17/03/16 20:21:01 INFO mapred.JobClient:  map 31% reduce 9%
17/03/16 20:21:02 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 20:21:04 INFO mapred.JobClient:  map 33% reduce 10%
17/03/16 20:21:05 INFO mapred.JobClient:  map 34% reduce 10%
17/03/16 20:21:07 INFO mapred.JobClient:  map 35% reduce 10%
17/03/16 20:21:08 INFO mapred.JobClient:  map 36% reduce 10%
17/03/16 20:21:09 INFO mapred.JobClient:  map 37% reduce 10%
17/03/16 20:21:10 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 20:21:11 INFO mapred.JobClient:  map 38% reduce 11%
17/03/16 20:21:13 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 20:21:14 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 20:21:16 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 20:21:19 INFO mapred.JobClient:  map 43% reduce 12%
17/03/16 20:21:20 INFO mapred.JobClient:  map 44% reduce 12%
17/03/16 20:21:21 INFO mapred.JobClient:  map 45% reduce 13%
17/03/16 20:21:22 INFO mapred.JobClient:  map 45% reduce 14%
17/03/16 20:21:23 INFO mapred.JobClient:  map 46% reduce 14%
17/03/16 20:21:24 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 20:21:27 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 20:21:28 INFO mapred.JobClient:  map 49% reduce 15%
17/03/16 20:21:29 INFO mapred.JobClient:  map 50% reduce 15%
17/03/16 20:21:30 INFO mapred.JobClient:  map 51% reduce 15%
17/03/16 20:21:31 INFO mapred.JobClient:  map 52% reduce 15%
17/03/16 20:21:32 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 20:21:33 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 20:21:34 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 20:21:35 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 20:21:37 INFO mapred.JobClient:  map 56% reduce 17%
17/03/16 20:21:38 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 20:21:40 INFO mapred.JobClient:  map 58% reduce 18%
17/03/16 20:21:41 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 20:21:43 INFO mapred.JobClient:  map 60% reduce 18%
17/03/16 20:21:44 INFO mapred.JobClient:  map 61% reduce 18%
17/03/16 20:21:45 INFO mapred.JobClient:  map 61% reduce 19%
17/03/16 20:21:46 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 20:21:47 INFO mapred.JobClient:  map 63% reduce 19%
17/03/16 20:21:49 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 20:21:50 INFO mapred.JobClient:  map 65% reduce 19%
17/03/16 20:21:51 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 20:21:52 INFO mapred.JobClient:  map 66% reduce 21%
17/03/16 20:21:53 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 20:21:54 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 20:21:56 INFO mapred.JobClient:  map 69% reduce 21%
17/03/16 20:21:57 INFO mapred.JobClient:  map 70% reduce 21%
17/03/16 20:21:58 INFO mapred.JobClient:  map 71% reduce 21%
17/03/16 20:22:00 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 20:22:01 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 20:22:03 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 20:22:05 INFO mapred.JobClient:  map 75% reduce 23%
17/03/16 20:22:06 INFO mapred.JobClient:  map 75% reduce 24%
17/03/16 20:22:07 INFO mapred.JobClient:  map 76% reduce 24%
17/03/16 20:22:08 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 20:22:10 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 20:22:11 INFO mapred.JobClient:  map 79% reduce 24%
17/03/16 20:22:12 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 20:22:14 INFO mapred.JobClient:  map 82% reduce 25%
17/03/16 20:22:15 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 20:22:18 INFO mapred.JobClient:  map 83% reduce 27%
17/03/16 20:22:19 INFO mapred.JobClient:  map 84% reduce 27%
17/03/16 20:22:20 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 20:22:22 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 20:22:24 INFO mapred.JobClient:  map 87% reduce 28%
17/03/16 20:22:25 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 20:22:27 INFO mapred.JobClient:  map 90% reduce 29%
17/03/16 20:22:29 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 20:22:32 INFO mapred.JobClient:  map 94% reduce 29%
17/03/16 20:22:33 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 20:22:36 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 20:22:39 INFO mapred.JobClient:  map 99% reduce 31%
17/03/16 20:22:42 INFO mapred.JobClient:  map 100% reduce 31%
17/03/16 20:22:44 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 20:22:46 INFO mapred.JobClient:  map 100% reduce 33%
17/03/16 20:22:48 INFO mapred.JobClient:  map 100% reduce 40%
17/03/16 20:22:51 INFO mapred.JobClient:  map 100% reduce 47%
17/03/16 20:22:52 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 20:22:54 INFO mapred.JobClient:  map 100% reduce 55%
17/03/16 20:22:55 INFO mapred.JobClient:  map 100% reduce 56%
17/03/16 20:23:01 INFO mapred.JobClient:  map 100% reduce 58%
17/03/16 20:23:04 INFO mapred.JobClient:  map 100% reduce 59%
17/03/16 20:23:06 INFO mapred.JobClient:  map 100% reduce 60%
17/03/16 20:23:09 INFO mapred.JobClient:  map 100% reduce 61%
17/03/16 20:23:10 INFO mapred.JobClient:  map 100% reduce 62%
17/03/16 20:23:12 INFO mapred.JobClient:  map 100% reduce 63%
17/03/16 20:23:15 INFO mapred.JobClient:  map 100% reduce 64%
17/03/16 20:23:18 INFO mapred.JobClient:  map 100% reduce 65%
17/03/16 20:23:21 INFO mapred.JobClient:  map 100% reduce 67%
17/03/16 20:23:24 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 20:23:25 INFO mapred.JobClient:  map 100% reduce 69%
17/03/16 20:23:27 INFO mapred.JobClient:  map 100% reduce 70%
17/03/16 20:23:30 INFO mapred.JobClient:  map 100% reduce 71%
17/03/16 20:23:31 INFO mapred.JobClient:  map 100% reduce 72%
17/03/16 20:23:34 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 20:33:20 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 20:33:21 INFO mapred.JobClient:  map 98% reduce 68%
17/03/16 20:33:30 INFO mapred.JobClient:  map 100% reduce 68%
17/03/16 20:33:31 INFO mapred.JobClient:  map 98% reduce 68%
17/03/16 20:33:32 INFO mapred.JobClient:  map 98% reduce 69%
17/03/16 20:33:40 INFO mapred.JobClient:  map 99% reduce 69%
17/03/16 20:33:41 INFO mapred.JobClient:  map 98% reduce 69%
17/03/16 20:33:45 INFO mapred.JobClient:  map 98% reduce 70%
17/03/16 20:33:53 INFO mapred.JobClient:  map 99% reduce 70%
17/03/16 20:33:54 INFO mapred.JobClient:  map 98% reduce 70%
17/03/16 20:34:03 INFO mapred.JobClient:  map 99% reduce 71%
17/03/16 20:34:04 INFO mapred.JobClient:  map 98% reduce 71%
17/03/16 20:34:05 INFO mapred.JobClient:  map 99% reduce 71%
17/03/16 20:34:06 INFO mapred.JobClient:  map 98% reduce 71%
17/03/16 20:34:12 INFO mapred.JobClient:  map 99% reduce 71%
17/03/16 20:34:13 INFO mapred.JobClient:  map 98% reduce 71%
17/03/16 20:34:16 INFO mapred.JobClient:  map 99% reduce 71%
17/03/16 20:34:17 INFO mapred.JobClient:  map 98% reduce 72%
17/03/16 20:34:22 INFO mapred.JobClient:  map 99% reduce 72%
17/03/16 20:34:23 INFO mapred.JobClient:  map 98% reduce 72%
17/03/16 20:34:24 INFO mapred.JobClient:  map 99% reduce 72%
17/03/16 20:34:25 INFO mapred.JobClient:  map 98% reduce 72%
17/03/16 20:34:31 INFO mapred.JobClient:  map 99% reduce 72%
17/03/16 20:34:32 INFO mapred.JobClient:  map 99% reduce 73%
17/03/16 20:34:34 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 20:34:42 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 20:34:44 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 20:34:45 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 20:34:48 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 20:34:54 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 20:34:57 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 20:34:59 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 20:35:03 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 20:35:06 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 20:35:08 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 20:35:09 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 20:35:12 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 20:35:14 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 20:35:17 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 20:35:21 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 20:35:23 INFO mapred.JobClient: Job complete: job_201703162019_0001
17/03/16 20:35:23 INFO mapred.JobClient: Counters: 30
17/03/16 20:35:23 INFO mapred.JobClient:   Job Counters
17/03/16 20:35:23 INFO mapred.JobClient:     Launched reduce tasks=9
17/03/16 20:35:23 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=1106125
17/03/16 20:35:23 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 20:35:23 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 20:35:23 INFO mapred.JobClient:     Launched map tasks=325
17/03/16 20:35:23 INFO mapred.JobClient:     Data-local map tasks=325
17/03/16 20:35:23 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=2026330
17/03/16 20:35:23 INFO mapred.JobClient:   File Input Format Counters
17/03/16 20:35:23 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 20:35:23 INFO mapred.JobClient:   File Output Format Counters
17/03/16 20:35:23 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 20:35:23 INFO mapred.JobClient:   FileSystemCounters
17/03/16 20:35:23 INFO mapred.JobClient:     FILE_BYTES_READ=94233955178
17/03/16 20:35:23 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 20:35:23 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126493327227
17/03/16 20:35:23 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 20:35:23 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 20:35:23 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 20:35:23 INFO mapred.JobClient:     Map input records=3068055
17/03/16 20:35:23 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 20:35:23 INFO mapred.JobClient:     Spilled Records=12031821
17/03/16 20:35:23 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 20:35:23 INFO mapred.JobClient:     Total committed heap usage (bytes)=49356472320
17/03/16 20:35:23 INFO mapred.JobClient:     CPU time spent (ms)=1531170
17/03/16 20:35:23 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 20:35:23 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 20:35:23 INFO mapred.JobClient:     Combine input records=0
17/03/16 20:35:23 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 20:35:23 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 20:35:23 INFO mapred.JobClient:     Combine output records=0
17/03/16 20:35:23 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52883898368
17/03/16 20:35:23 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 20:35:23 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196032483328
17/03/16 20:35:23 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 20:35:23 UTC 2017
The job took 911 seconds.
```

## Death after map (reduce 31%) with expiry interval of 30s
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 21:58:59 UTC 2017
17/03/16 21:58:59 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 21:59:00 INFO mapred.JobClient: Running job: job_201703162158_0001
17/03/16 21:59:01 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 21:59:07 INFO mapred.JobClient:  map 1% reduce 0%
17/03/16 21:59:08 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 21:59:10 INFO mapred.JobClient:  map 3% reduce 0%
17/03/16 21:59:11 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 21:59:14 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 21:59:15 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 21:59:17 INFO mapred.JobClient:  map 9% reduce 0%
17/03/16 21:59:18 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 21:59:21 INFO mapred.JobClient:  map 12% reduce 0%
17/03/16 21:59:21 INFO mapred.JobClient: Task Id : attempt_201703162158_0001_r_000001_0, Status : FAILED
Error: java.lang.OutOfMemoryError: Java heap space
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.shuffleInMemory(ReduceTask.java:1703)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.getMapOutput(ReduceTask.java:1563)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.copyOutput(ReduceTask.java:1401)
        at org.apache.hadoop.mapred.ReduceTask$ReduceCopier$MapOutputCopier.run(ReduceTask.java:1333)

17/03/16 21:59:22 INFO mapred.JobClient:  map 12% reduce 2%
17/03/16 21:59:24 INFO mapred.JobClient:  map 14% reduce 2%
17/03/16 21:59:25 INFO mapred.JobClient:  map 15% reduce 2%
17/03/16 21:59:28 INFO mapred.JobClient:  map 17% reduce 2%
17/03/16 21:59:30 INFO mapred.JobClient:  map 17% reduce 3%
17/03/16 21:59:31 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 21:59:34 INFO mapred.JobClient:  map 20% reduce 5%
17/03/16 21:59:35 INFO mapred.JobClient:  map 22% reduce 5%
17/03/16 21:59:37 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 21:59:38 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 21:59:40 INFO mapred.JobClient:  map 24% reduce 7%
17/03/16 21:59:41 INFO mapred.JobClient:  map 25% reduce 7%
17/03/16 21:59:42 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 21:59:43 INFO mapred.JobClient:  map 27% reduce 8%
17/03/16 21:59:45 INFO mapred.JobClient:  map 29% reduce 8%
17/03/16 21:59:48 INFO mapred.JobClient:  map 30% reduce 8%
17/03/16 21:59:49 INFO mapred.JobClient:  map 31% reduce 8%
17/03/16 21:59:50 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 21:59:51 INFO mapred.JobClient:  map 33% reduce 9%
17/03/16 21:59:52 INFO mapred.JobClient:  map 34% reduce 9%
17/03/16 21:59:56 INFO mapred.JobClient:  map 36% reduce 10%
17/03/16 21:59:58 INFO mapred.JobClient:  map 37% reduce 10%
17/03/16 21:59:59 INFO mapred.JobClient:  map 38% reduce 11%
17/03/16 22:00:00 INFO mapred.JobClient:  map 39% reduce 11%
17/03/16 22:00:03 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 22:00:04 INFO mapred.JobClient:  map 41% reduce 12%
17/03/16 22:00:06 INFO mapred.JobClient:  map 43% reduce 12%
17/03/16 22:00:07 INFO mapred.JobClient:  map 44% reduce 12%
17/03/16 22:00:08 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 22:00:10 INFO mapred.JobClient:  map 46% reduce 13%
17/03/16 22:00:12 INFO mapred.JobClient:  map 46% reduce 14%
17/03/16 22:00:14 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 22:00:17 INFO mapred.JobClient:  map 50% reduce 14%
17/03/16 22:00:18 INFO mapred.JobClient:  map 50% reduce 15%
17/03/16 22:00:19 INFO mapred.JobClient:  map 51% reduce 15%
17/03/16 22:00:20 INFO mapred.JobClient:  map 51% reduce 16%
17/03/16 22:00:23 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 22:00:24 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 22:00:26 INFO mapred.JobClient:  map 55% reduce 16%
17/03/16 22:00:27 INFO mapred.JobClient:  map 56% reduce 17%
17/03/16 22:00:29 INFO mapred.JobClient:  map 57% reduce 17%
17/03/16 22:00:30 INFO mapred.JobClient:  map 58% reduce 17%
17/03/16 22:00:31 INFO mapred.JobClient:  map 59% reduce 17%
17/03/16 22:00:33 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 22:00:34 INFO mapred.JobClient:  map 61% reduce 18%
17/03/16 22:00:35 INFO mapred.JobClient:  map 61% reduce 19%
17/03/16 22:00:36 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 22:00:37 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 22:00:40 INFO mapred.JobClient:  map 66% reduce 19%
17/03/16 22:00:41 INFO mapred.JobClient:  map 66% reduce 20%
17/03/16 22:00:43 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 22:00:44 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 22:00:45 INFO mapred.JobClient:  map 69% reduce 21%
17/03/16 22:00:46 INFO mapred.JobClient:  map 69% reduce 22%
17/03/16 22:00:47 INFO mapred.JobClient:  map 70% reduce 22%
17/03/16 22:00:48 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 22:00:50 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 22:00:51 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 22:00:53 INFO mapred.JobClient:  map 73% reduce 23%
17/03/16 22:00:54 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 22:00:55 INFO mapred.JobClient:  map 76% reduce 24%
17/03/16 22:00:58 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 22:00:59 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 22:01:01 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 22:01:02 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 22:01:04 INFO mapred.JobClient:  map 81% reduce 25%
17/03/16 22:01:05 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 22:01:06 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 22:01:08 INFO mapred.JobClient:  map 84% reduce 26%
17/03/16 22:01:09 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 22:01:11 INFO mapred.JobClient:  map 86% reduce 27%
17/03/16 22:01:12 INFO mapred.JobClient:  map 87% reduce 27%
17/03/16 22:01:14 INFO mapred.JobClient:  map 88% reduce 27%
17/03/16 22:01:15 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 22:01:16 INFO mapred.JobClient:  map 89% reduce 28%
17/03/16 22:01:17 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 22:01:18 INFO mapred.JobClient:  map 91% reduce 28%
17/03/16 22:01:19 INFO mapred.JobClient:  map 92% reduce 28%
17/03/16 22:01:20 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 22:01:21 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 22:01:22 INFO mapred.JobClient:  map 93% reduce 30%
17/03/16 22:01:23 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 22:01:24 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 22:01:25 INFO mapred.JobClient:  map 96% reduce 31%
17/03/16 22:01:27 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 22:01:28 INFO mapred.JobClient:  map 98% reduce 31%
17/03/16 22:01:30 INFO mapred.JobClient:  map 99% reduce 31%
17/03/16 22:01:31 INFO mapred.JobClient:  map 100% reduce 31%
17/03/16 22:01:34 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 22:01:39 INFO mapred.JobClient:  map 100% reduce 39%
17/03/16 22:01:41 INFO mapred.JobClient:  map 100% reduce 46%
17/03/16 22:01:42 INFO mapred.JobClient:  map 100% reduce 47%
17/03/16 22:01:44 INFO mapred.JobClient:  map 100% reduce 48%
17/03/16 22:01:48 INFO mapred.JobClient:  map 100% reduce 49%
17/03/16 22:01:54 INFO mapred.JobClient:  map 100% reduce 50%
17/03/16 22:01:57 INFO mapred.JobClient:  map 100% reduce 51%
17/03/16 22:02:00 INFO mapred.JobClient:  map 100% reduce 53%
17/03/16 22:02:06 INFO mapred.JobClient:  map 100% reduce 40%
17/03/16 22:02:07 INFO mapred.JobClient:  map 98% reduce 42%
17/03/16 22:02:10 INFO mapred.JobClient:  map 98% reduce 43%
17/03/16 22:02:13 INFO mapred.JobClient:  map 98% reduce 45%
17/03/16 22:02:14 INFO mapred.JobClient:  map 99% reduce 45%
17/03/16 22:02:15 INFO mapred.JobClient:  map 98% reduce 45%
17/03/16 22:02:16 INFO mapred.JobClient:  map 98% reduce 46%
17/03/16 22:02:19 INFO mapred.JobClient:  map 98% reduce 48%
17/03/16 22:02:22 INFO mapred.JobClient:  map 98% reduce 49%
17/03/16 22:02:23 INFO mapred.JobClient:  map 98% reduce 50%
17/03/16 22:02:25 INFO mapred.JobClient:  map 99% reduce 50%
17/03/16 22:02:26 INFO mapred.JobClient:  map 98% reduce 50%
17/03/16 22:02:29 INFO mapred.JobClient:  map 98% reduce 51%
17/03/16 22:02:33 INFO mapred.JobClient:  map 99% reduce 51%
17/03/16 22:02:34 INFO mapred.JobClient:  map 98% reduce 51%
17/03/16 22:02:35 INFO mapred.JobClient:  map 98% reduce 52%
17/03/16 22:02:38 INFO mapred.JobClient:  map 98% reduce 53%
17/03/16 22:02:44 INFO mapred.JobClient:  map 98% reduce 54%
17/03/16 22:02:47 INFO mapred.JobClient:  map 98% reduce 55%
17/03/16 22:02:53 INFO mapred.JobClient:  map 98% reduce 56%
17/03/16 22:02:59 INFO mapred.JobClient:  map 98% reduce 57%
17/03/16 22:03:03 INFO mapred.JobClient:  map 99% reduce 57%
17/03/16 22:03:09 INFO mapred.JobClient:  map 98% reduce 57%
17/03/16 22:03:16 INFO mapred.JobClient:  map 99% reduce 57%
17/03/16 22:03:17 INFO mapred.JobClient:  map 98% reduce 57%
17/03/16 22:03:18 INFO mapred.JobClient:  map 98% reduce 58%
17/03/16 22:03:24 INFO mapred.JobClient:  map 99% reduce 58%
17/03/16 22:03:25 INFO mapred.JobClient:  map 98% reduce 58%
17/03/16 22:03:33 INFO mapred.JobClient:  map 99% reduce 59%
17/03/16 22:03:37 INFO mapred.JobClient:  map 100% reduce 59%
17/03/16 22:03:45 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 22:03:47 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 22:03:48 INFO mapred.JobClient:  map 100% reduce 74%
17/03/16 22:03:56 INFO mapred.JobClient:  map 100% reduce 75%
17/03/16 22:04:00 INFO mapred.JobClient:  map 100% reduce 76%
17/03/16 22:04:03 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 22:04:06 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 22:04:11 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 22:04:23 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 22:04:35 INFO mapred.JobClient:  map 100% reduce 87%
17/03/16 22:04:47 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 22:04:59 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 22:05:09 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 22:05:20 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 22:05:31 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 22:05:46 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 22:05:54 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 22:06:04 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 22:06:16 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 22:06:28 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 22:06:41 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 22:06:47 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 22:06:56 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 22:06:57 INFO mapred.JobClient: Job complete: job_201703162158_0001
17/03/16 22:06:57 INFO mapred.JobClient: Counters: 30
17/03/16 22:06:57 INFO mapred.JobClient:   Job Counters
17/03/16 22:06:57 INFO mapred.JobClient:     Launched reduce tasks=9
17/03/16 22:06:57 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=1185289
17/03/16 22:06:57 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 22:06:57 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 22:06:57 INFO mapred.JobClient:     Launched map tasks=325
17/03/16 22:06:57 INFO mapred.JobClient:     Data-local map tasks=325
17/03/16 22:06:57 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1398470
17/03/16 22:06:57 INFO mapred.JobClient:   File Input Format Counters
17/03/16 22:06:57 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 22:06:57 INFO mapred.JobClient:   File Output Format Counters
17/03/16 22:06:57 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 22:06:57 INFO mapred.JobClient:   FileSystemCounters
17/03/16 22:06:57 INFO mapred.JobClient:     FILE_BYTES_READ=94323058258
17/03/16 22:06:57 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 22:06:57 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126582430062
17/03/16 22:06:57 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 22:06:57 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 22:06:57 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 22:06:57 INFO mapred.JobClient:     Map input records=3068055
17/03/16 22:06:57 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 22:06:57 INFO mapred.JobClient:     Spilled Records=12040127
17/03/16 22:06:57 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 22:06:57 INFO mapred.JobClient:     Total committed heap usage (bytes)=49332355072
17/03/16 22:06:57 INFO mapred.JobClient:     CPU time spent (ms)=1556130
17/03/16 22:06:57 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 22:06:57 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 22:06:57 INFO mapred.JobClient:     Combine input records=0
17/03/16 22:06:57 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 22:06:57 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 22:06:57 INFO mapred.JobClient:     Combine output records=0
17/03/16 22:06:57 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52892078080
17/03/16 22:06:57 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 22:06:57 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196496920576
17/03/16 22:06:57 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 22:06:57 UTC 2017
The job took 477 seconds.
```

## Death after map (reduce 32%) with expiry interval of 60s
```
sbihel@paranoia-3 ~/hadoop-1.2.1
 % bin/hadoop jar hadoop-examples-1.2.1.jar sort output outputsorted
Running on 3 nodes to sort from hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/output into hdfs://paranoia-3.rennes.grid5000.fr:9000/user/sbihel/outputsorted with 5 reduces.
Job started: Thu Mar 16 22:46:51 UTC 2017
17/03/16 22:46:51 INFO mapred.FileInputFormat: Total input paths to process : 30
17/03/16 22:46:51 INFO mapred.JobClient: Running job: job_201703162245_0001
17/03/16 22:46:52 INFO mapred.JobClient:  map 0% reduce 0%
17/03/16 22:46:59 INFO mapred.JobClient:  map 2% reduce 0%
17/03/16 22:47:02 INFO mapred.JobClient:  map 5% reduce 0%
17/03/16 22:47:05 INFO mapred.JobClient:  map 6% reduce 0%
17/03/16 22:47:06 INFO mapred.JobClient:  map 7% reduce 0%
17/03/16 22:47:08 INFO mapred.JobClient:  map 8% reduce 0%
17/03/16 22:47:09 INFO mapred.JobClient:  map 10% reduce 0%
17/03/16 22:47:12 INFO mapred.JobClient:  map 11% reduce 0%
17/03/16 22:47:13 INFO mapred.JobClient:  map 12% reduce 3%
17/03/16 22:47:15 INFO mapred.JobClient:  map 13% reduce 3%
17/03/16 22:47:16 INFO mapred.JobClient:  map 15% reduce 3%
17/03/16 22:47:19 INFO mapred.JobClient:  map 16% reduce 3%
17/03/16 22:47:20 INFO mapred.JobClient:  map 17% reduce 3%
17/03/16 22:47:22 INFO mapred.JobClient:  map 19% reduce 4%
17/03/16 22:47:26 INFO mapred.JobClient:  map 21% reduce 4%
17/03/16 22:47:27 INFO mapred.JobClient:  map 22% reduce 4%
17/03/16 22:47:28 INFO mapred.JobClient:  map 22% reduce 6%
17/03/16 22:47:29 INFO mapred.JobClient:  map 24% reduce 6%
17/03/16 22:47:32 INFO mapred.JobClient:  map 25% reduce 6%
17/03/16 22:47:33 INFO mapred.JobClient:  map 27% reduce 6%
17/03/16 22:47:34 INFO mapred.JobClient:  map 27% reduce 7%
17/03/16 22:47:37 INFO mapred.JobClient:  map 29% reduce 7%
17/03/16 22:47:39 INFO mapred.JobClient:  map 30% reduce 7%
17/03/16 22:47:40 INFO mapred.JobClient:  map 31% reduce 8%
17/03/16 22:47:42 INFO mapred.JobClient:  map 32% reduce 9%
17/03/16 22:47:44 INFO mapred.JobClient:  map 34% reduce 9%
17/03/16 22:47:46 INFO mapred.JobClient:  map 34% reduce 10%
17/03/16 22:47:47 INFO mapred.JobClient:  map 36% reduce 10%
17/03/16 22:47:49 INFO mapred.JobClient:  map 37% reduce 11%
17/03/16 22:47:52 INFO mapred.JobClient:  map 38% reduce 12%
17/03/16 22:47:53 INFO mapred.JobClient:  map 39% reduce 12%
17/03/16 22:47:55 INFO mapred.JobClient:  map 40% reduce 12%
17/03/16 22:47:56 INFO mapred.JobClient:  map 42% reduce 12%
17/03/16 22:47:59 INFO mapred.JobClient:  map 43% reduce 12%
17/03/16 22:48:00 INFO mapred.JobClient:  map 44% reduce 12%
17/03/16 22:48:01 INFO mapred.JobClient:  map 44% reduce 13%
17/03/16 22:48:02 INFO mapred.JobClient:  map 45% reduce 13%
17/03/16 22:48:03 INFO mapred.JobClient:  map 46% reduce 13%
17/03/16 22:48:04 INFO mapred.JobClient:  map 47% reduce 14%
17/03/16 22:48:07 INFO mapred.JobClient:  map 49% reduce 14%
17/03/16 22:48:09 INFO mapred.JobClient:  map 50% reduce 14%
17/03/16 22:48:10 INFO mapred.JobClient:  map 51% reduce 15%
17/03/16 22:48:11 INFO mapred.JobClient:  map 52% reduce 15%
17/03/16 22:48:12 INFO mapred.JobClient:  map 52% reduce 16%
17/03/16 22:48:14 INFO mapred.JobClient:  map 53% reduce 16%
17/03/16 22:48:15 INFO mapred.JobClient:  map 54% reduce 16%
17/03/16 22:48:16 INFO mapred.JobClient:  map 55% reduce 16%
17/03/16 22:48:17 INFO mapred.JobClient:  map 55% reduce 17%
17/03/16 22:48:18 INFO mapred.JobClient:  map 56% reduce 17%
17/03/16 22:48:19 INFO mapred.JobClient:  map 57% reduce 18%
17/03/16 22:48:21 INFO mapred.JobClient:  map 59% reduce 18%
17/03/16 22:48:23 INFO mapred.JobClient:  map 60% reduce 18%
17/03/16 22:48:25 INFO mapred.JobClient:  map 61% reduce 19%
17/03/16 22:48:26 INFO mapred.JobClient:  map 62% reduce 19%
17/03/16 22:48:28 INFO mapred.JobClient:  map 63% reduce 19%
17/03/16 22:48:30 INFO mapred.JobClient:  map 64% reduce 19%
17/03/16 22:48:32 INFO mapred.JobClient:  map 65% reduce 20%
17/03/16 22:48:33 INFO mapred.JobClient:  map 66% reduce 21%
17/03/16 22:48:35 INFO mapred.JobClient:  map 67% reduce 21%
17/03/16 22:48:36 INFO mapred.JobClient:  map 68% reduce 21%
17/03/16 22:48:38 INFO mapred.JobClient:  map 69% reduce 22%
17/03/16 22:48:40 INFO mapred.JobClient:  map 71% reduce 22%
17/03/16 22:48:42 INFO mapred.JobClient:  map 72% reduce 22%
17/03/16 22:48:43 INFO mapred.JobClient:  map 73% reduce 22%
17/03/16 22:48:45 INFO mapred.JobClient:  map 74% reduce 23%
17/03/16 22:48:47 INFO mapred.JobClient:  map 76% reduce 23%
17/03/16 22:48:48 INFO mapred.JobClient:  map 76% reduce 24%
17/03/16 22:48:49 INFO mapred.JobClient:  map 77% reduce 24%
17/03/16 22:48:53 INFO mapred.JobClient:  map 78% reduce 24%
17/03/16 22:48:54 INFO mapred.JobClient:  map 78% reduce 25%
17/03/16 22:48:55 INFO mapred.JobClient:  map 79% reduce 25%
17/03/16 22:48:56 INFO mapred.JobClient:  map 80% reduce 25%
17/03/16 22:48:57 INFO mapred.JobClient:  map 81% reduce 26%
17/03/16 22:48:58 INFO mapred.JobClient:  map 82% reduce 26%
17/03/16 22:49:00 INFO mapred.JobClient:  map 83% reduce 26%
17/03/16 22:49:02 INFO mapred.JobClient:  map 85% reduce 26%
17/03/16 22:49:03 INFO mapred.JobClient:  map 85% reduce 27%
17/03/16 22:49:04 INFO mapred.JobClient:  map 86% reduce 27%
17/03/16 22:49:06 INFO mapred.JobClient:  map 87% reduce 28%
17/03/16 22:49:07 INFO mapred.JobClient:  map 88% reduce 28%
17/03/16 22:49:09 INFO mapred.JobClient:  map 90% reduce 28%
17/03/16 22:49:11 INFO mapred.JobClient:  map 91% reduce 28%
17/03/16 22:49:12 INFO mapred.JobClient:  map 92% reduce 29%
17/03/16 22:49:14 INFO mapred.JobClient:  map 93% reduce 29%
17/03/16 22:49:15 INFO mapred.JobClient:  map 94% reduce 29%
17/03/16 22:49:16 INFO mapred.JobClient:  map 94% reduce 30%
17/03/16 22:49:17 INFO mapred.JobClient:  map 95% reduce 30%
17/03/16 22:49:19 INFO mapred.JobClient:  map 97% reduce 31%
17/03/16 22:49:22 INFO mapred.JobClient:  map 99% reduce 31%
17/03/16 22:49:24 INFO mapred.JobClient:  map 100% reduce 32%
17/03/16 22:49:30 INFO mapred.JobClient:  map 100% reduce 39%
17/03/16 22:49:33 INFO mapred.JobClient:  map 100% reduce 46%
17/03/16 22:49:36 INFO mapred.JobClient:  map 100% reduce 47%
17/03/16 22:49:39 INFO mapred.JobClient:  map 100% reduce 48%
17/03/16 22:49:42 INFO mapred.JobClient:  map 100% reduce 49%
17/03/16 22:49:45 INFO mapred.JobClient:  map 100% reduce 51%
17/03/16 22:49:48 INFO mapred.JobClient:  map 100% reduce 52%
17/03/16 22:49:51 INFO mapred.JobClient:  map 100% reduce 53%
17/03/16 22:49:55 INFO mapred.JobClient:  map 100% reduce 54%
17/03/16 22:50:00 INFO mapred.JobClient:  map 100% reduce 55%
17/03/16 22:50:03 INFO mapred.JobClient:  map 100% reduce 56%
17/03/16 22:50:06 INFO mapred.JobClient:  map 100% reduce 57%
17/03/16 22:50:09 INFO mapred.JobClient:  map 100% reduce 58%
17/03/16 22:50:12 INFO mapred.JobClient:  map 100% reduce 59%
17/03/16 22:50:33 INFO mapred.JobClient:  map 98% reduce 53%
17/03/16 22:50:36 INFO mapred.JobClient:  map 99% reduce 53%
17/03/16 22:50:37 INFO mapred.JobClient:  map 98% reduce 53%
17/03/16 22:50:39 INFO mapred.JobClient:  map 98% reduce 54%
17/03/16 22:50:42 INFO mapred.JobClient:  map 98% reduce 55%
17/03/16 22:50:44 INFO mapred.JobClient:  map 99% reduce 55%
17/03/16 22:50:46 INFO mapred.JobClient:  map 98% reduce 55%
17/03/16 22:50:48 INFO mapred.JobClient:  map 98% reduce 56%
17/03/16 22:50:56 INFO mapred.JobClient:  map 99% reduce 56%
17/03/16 22:50:57 INFO mapred.JobClient:  map 98% reduce 56%
17/03/16 22:51:04 INFO mapred.JobClient:  map 98% reduce 57%
17/03/16 22:51:06 INFO mapred.JobClient:  map 99% reduce 57%
17/03/16 22:51:07 INFO mapred.JobClient:  map 98% reduce 57%
17/03/16 22:51:13 INFO mapred.JobClient:  map 99% reduce 57%
17/03/16 22:51:14 INFO mapred.JobClient:  map 98% reduce 57%
17/03/16 22:51:19 INFO mapred.JobClient:  map 98% reduce 58%
17/03/16 22:51:20 INFO mapred.JobClient:  map 99% reduce 58%
17/03/16 22:51:21 INFO mapred.JobClient:  map 98% reduce 58%
17/03/16 22:51:33 INFO mapred.JobClient:  map 98% reduce 59%
17/03/16 22:51:34 INFO mapred.JobClient:  map 99% reduce 59%
17/03/16 22:51:35 INFO mapred.JobClient:  map 98% reduce 59%
17/03/16 22:51:40 INFO mapred.JobClient:  map 99% reduce 59%
17/03/16 22:51:41 INFO mapred.JobClient:  map 98% reduce 59%
17/03/16 22:51:43 INFO mapred.JobClient:  map 99% reduce 59%
17/03/16 22:51:46 INFO mapred.JobClient:  map 100% reduce 59%
17/03/16 22:51:52 INFO mapred.JobClient:  map 100% reduce 66%
17/03/16 22:51:55 INFO mapred.JobClient:  map 100% reduce 73%
17/03/16 22:51:56 INFO mapred.JobClient:  map 100% reduce 80%
17/03/16 22:51:58 INFO mapred.JobClient:  map 100% reduce 81%
17/03/16 22:52:00 INFO mapred.JobClient:  map 100% reduce 82%
17/03/16 22:52:03 INFO mapred.JobClient:  map 100% reduce 83%
17/03/16 22:52:04 INFO mapred.JobClient:  map 100% reduce 84%
17/03/16 22:52:07 INFO mapred.JobClient:  map 100% reduce 85%
17/03/16 22:52:10 INFO mapred.JobClient:  map 100% reduce 86%
17/03/16 22:52:13 INFO mapred.JobClient:  map 100% reduce 88%
17/03/16 22:52:16 INFO mapred.JobClient:  map 100% reduce 89%
17/03/16 22:52:19 INFO mapred.JobClient:  map 100% reduce 90%
17/03/16 22:52:22 INFO mapred.JobClient:  map 100% reduce 91%
17/03/16 22:52:25 INFO mapred.JobClient:  map 100% reduce 92%
17/03/16 22:52:28 INFO mapred.JobClient:  map 100% reduce 93%
17/03/16 22:52:40 INFO mapred.JobClient:  map 100% reduce 94%
17/03/16 22:53:01 INFO mapred.JobClient:  map 100% reduce 95%
17/03/16 22:53:13 INFO mapred.JobClient:  map 100% reduce 96%
17/03/16 22:53:22 INFO mapred.JobClient:  map 100% reduce 97%
17/03/16 22:53:31 INFO mapred.JobClient:  map 100% reduce 98%
17/03/16 22:53:40 INFO mapred.JobClient:  map 100% reduce 99%
17/03/16 22:53:49 INFO mapred.JobClient:  map 100% reduce 100%
17/03/16 22:53:50 INFO mapred.JobClient: Job complete: job_201703162245_0001
17/03/16 22:53:50 INFO mapred.JobClient: Counters: 30
17/03/16 22:53:50 INFO mapred.JobClient:   Job Counters
17/03/16 22:53:50 INFO mapred.JobClient:     Launched reduce tasks=8
17/03/16 22:53:50 INFO mapred.JobClient:     SLOTS_MILLIS_MAPS=1119310
17/03/16 22:53:50 INFO mapred.JobClient:     Total time spent by all reduces waiting after reserving slots (ms)=0
17/03/16 22:53:50 INFO mapred.JobClient:     Total time spent by all maps waiting after reserving slots (ms)=0
17/03/16 22:53:50 INFO mapred.JobClient:     Launched map tasks=322
17/03/16 22:53:50 INFO mapred.JobClient:     Data-local map tasks=322
17/03/16 22:53:50 INFO mapred.JobClient:     SLOTS_MILLIS_REDUCES=1242091
17/03/16 22:53:50 INFO mapred.JobClient:   File Input Format Counters
17/03/16 22:53:50 INFO mapred.JobClient:     Bytes Read=32320091848
17/03/16 22:53:50 INFO mapred.JobClient:   File Output Format Counters
17/03/16 22:53:50 INFO mapred.JobClient:     Bytes Written=32318578178
17/03/16 22:53:50 INFO mapred.JobClient:   FileSystemCounters
17/03/16 22:53:50 INFO mapred.JobClient:     FILE_BYTES_READ=94428503464
17/03/16 22:53:50 INFO mapred.JobClient:     HDFS_BYTES_READ=32322364752
17/03/16 22:53:50 INFO mapred.JobClient:     FILE_BYTES_WRITTEN=126687875268
17/03/16 22:53:50 INFO mapred.JobClient:     HDFS_BYTES_WRITTEN=32318578178
17/03/16 22:53:50 INFO mapred.JobClient:   Map-Reduce Framework
17/03/16 22:53:50 INFO mapred.JobClient:     Map output materialized bytes=32254229872
17/03/16 22:53:50 INFO mapred.JobClient:     Map input records=3068055
17/03/16 22:53:50 INFO mapred.JobClient:     Reduce shuffle bytes=32254229872
17/03/16 22:53:50 INFO mapred.JobClient:     Spilled Records=12050182
17/03/16 22:53:50 INFO mapred.JobClient:     Map output bytes=32236975678
17/03/16 22:53:50 INFO mapred.JobClient:     Total committed heap usage (bytes)=49356472320
17/03/16 22:53:50 INFO mapred.JobClient:     CPU time spent (ms)=1541540
17/03/16 22:53:50 INFO mapred.JobClient:     Map input bytes=32318578838
17/03/16 22:53:50 INFO mapred.JobClient:     SPLIT_RAW_BYTES=29760
17/03/16 22:53:50 INFO mapred.JobClient:     Combine input records=0
17/03/16 22:53:50 INFO mapred.JobClient:     Reduce input records=3068055
17/03/16 22:53:50 INFO mapred.JobClient:     Reduce input groups=3068055
17/03/16 22:53:50 INFO mapred.JobClient:     Combine output records=0
17/03/16 22:53:50 INFO mapred.JobClient:     Physical memory (bytes) snapshot=52954566656
17/03/16 22:53:50 INFO mapred.JobClient:     Reduce output records=3068055
17/03/16 22:53:50 INFO mapred.JobClient:     Virtual memory (bytes) snapshot=196186230784
17/03/16 22:53:50 INFO mapred.JobClient:     Map output records=3068055
Job ended: Thu Mar 16 22:53:50 UTC 2017
The job took 419 seconds.
```
