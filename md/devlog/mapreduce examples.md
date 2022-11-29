---
created: 20211124203330456
desc: ''
id: rttao2ttrcnyce4qro7cku2
title: MapReduce Examples
updated: 1653318643718
---
   
Topics::  [Data Engineering](/not_created.md)   
   
   
---   
   
### Working Example of Word Count   
   
`yarn jar $EXAMPLES/hadoop-mapreduce-examples-3.3.0.jar > words.txt`   
   
`yarn jar $EXAMPLES/hadoop-mapreduce-examples-3.3.0.jar wordcount wordcount/in wordcount/out`   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.vkmgyisvvbc.png)   
   
Check the output that was created   
   
`hdfs dfs -cat wordcount/out/part-r-00000`   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.8velr6e7whs.png)   
   
### Calculate pi   
   
   
- Simple MapReduce program to run, good for quick tests.   
- The following is run on the 4-node cluster   
   
`yarn jar $EXAMPLES/hadoop-mapreduce-examples-3.3.0.jar pi 16 100000`     
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.ip1wh7ittuc.png)   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.op5t2hnmh7l.png)   
   
   
- The following is a short test that will run on the LHM-VM (If you increase   
- the number of maps (8) or the number of guesses (1000) then the   
- application will take longer.   
   
`yarn jar $EXAMPLES/hadoop-mapreduce-examples-3.3.0.jar pi 8 1000`   
   
### The Terasort Benchmark   
   
**IMPORTANT: The test will not run on the LHM-VM. Indeed, as run below,   
the Teragen portion will create a 50GB file (by default the LHM-VM has   
70 GB of file space. The actual Terasort step will create another   
50 GB file. You can try to reduce the file size from 500000000 to   
5000 so the application can finish.**   
Terasort is used to measure the raw sorting power of Hadoop MapReduce, though it is of no practical use, it can provide an indication of how fast your cluster can process data.   
   
The following steps are for the the 4-node cluster mentioned above, using the HDFS account `/user/deadline`.   
   
There are three steps required to run the complete test:   
   
1.  Generate the table   
2.  Sort the table   
3.  Validate the sort   
   
<!-- end list -->   
   
   
- rows are 100 bytes long, thus the total amount of data written is 100 times the   
- number of rows (i.e. to write a 100 GBytes of data, use 1000000000 rows). You   
- will also need to specify input and output directories in HDFS.   
   
   
- 1\. Run teragen to generate 500 MB of data, 500,000 rows of random data to sort   
   
`yarn jar $$EXAMPLES/hadoop-mapreduce-examples-3.3.0.jar teragen 5000000 /user/hands-on/TeraGen-500MB`   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.dhhwu16cazc.png) \* Check if the data was created; this will be your input for the next step in the terasort benchmark   
`hdfs dfs -ls TeraGen-500MB`   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.brz6odys9hv.png)   
   
   
- 2\. Run terasort to sort the database   
   
`yarn jar $EXAMPLES/hadoop-mapreduce-examples-3.3.0.jar terasort /user/hands-on/TeraGen-500MB /user/hands-on/TeraSort-500MB`   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.idartp3zxj.png)   
Check the output that was created for `TeraSort-500MB` (which was the output dir)   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.bohj41tce1a.png)   
   
A combined single file was created   
   
   
- 3\. Run teravalidate to validate the sort Teragen   
   
`yarn jar $EXAMPLES/hadoop-mapreduce-examples-3.3.0.jar teravalidate /user/hands-on/TeraSort-500MB /user/hands-on/TeraValid-500MB`   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.m6uaknqoch.png)   
Check the results that was created and the checksum of the file   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.4ch3o9j2lo7.png) \* Interpret the results: \* Measure the time it takes to complete the terasort application. Results are \* usually reported in Database Size in Seconds (or Minutes).   
   
   
- The performance can be increased by increasing the number of reducers (default is one)   
- add the option -Dmapred.reduce.tasks=NUMBER_OF_REDUCERS   
- The command below uses 4 reducers.   
   
`yarn jar $EXAMPLES/hadoop-mapreduce-examples-3.3.0.jar terasort -Dmapred.reduce.tasks=4 /user/hands-on/TeraGen-500MB /user/hands-on/TeraSort-500MB`   
   
   
- Don't for get to delete you files in HDFS before the next run\!   
   
`hdfs dfs -rm -r -skipTrash Tera*`   
   
### Miscellaneous notes   
   
[hadoop](../devlog/hadoop.md) and [apache spark](../topics/apache%20spark.md) usually work with "INPUT DIRECTORIES" not files. Note that the argument given to word count in the above example was a directory NOT the "words.txt" file. We can add more files to the input directory and `wordcount` will ingest all the files in finds.