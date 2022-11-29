---
created: 20211122214632356
desc: ''
id: j6kfx6ziqg91r356nur9cwy
tags:
- '!/usr/bin/env'
- '!/bin/bash'
- '!/usr/bin/env'
title: MapReduce
updated: 1653305310654
---
   
   
- MapReduce is a simple algorithm   
- It uses distinct steps and one-way communication   
- **Map** first then **Reduce**, can be combined into multiple layers   
   
### Example of MapReduce (but non parallel)   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.uyhzcdyhtl.png)   
   
### MapReduce Design Principles   
   
**"Can we read parts(_slices_) of the file at the same time on different systems?"**   
   
   
- For certain types of problems the answer is "Yes"   
- Slice data and spread across multiple HDDs on multiple servers ([hdfs](../devlog/hdfs.md))   
- Obtain performance from reading slices at the same time   
- Moving computation to data, if possible(cheaper than moving data to computation)   
- Allows scalable software that can hide (most) execution details from the user   
- The ability to be fault tolerant (map steps crashing, restarting) which can be extended to reducers.   
   
### MapReduce Big Picture   
   
   
- Slice data and place each part on a different server(node)?   
- Improve performance by mapping (processing) each slice independently   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.2eclq7p550p.png)   
   
   
- Slicing happens automatically, the administrator can change the size of the slice   
- Slice is blind to the data that is inside the file(s), we're not slicing based on structure but based on size.   
   
### Slices and Splits   
   
   
- Each slice has programmatically defined data splits that independent of slice boundaries.   
- **A map is applied to each split in the slice.**   
- Edge splits may span two slices.   
- There can be multiple maps occuring on the same slice.   
  - If a split doesn't fit on a slice, edge splits may span to other slices(not a lot of data and MapReduce algo will account for it automagically)   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.wstyvft6d0s.png)   
   
### Scalable Mapping Step   
   
1.  Slice data into parts   
2.  Apply the same Mapping function to **Input list** (user defined splits)   
3.  Each step provides a separate set of results(**Output list**)   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.2glgo0k8cyt.png)   
   
### Reduction Step   
   
   
- Results from each map(as applied to each split) are combined and reduced to a single Output value.   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.w1uoldg3if.png)   
   
### Summary   
   
   
- [hadoop](../devlog/hadoop.md) provides a MapReduce engine as part of the core components ([hdfs](../devlog/hdfs.md), [yarn](../devlog/yarn.md) and [mapreduce](../devlog/mapreduce.md))   
- Hadoop MapReduce can be used directly or by higher level applications(e.g. [hive](../devlog/hive.md))   
- Original MapReduce was somewhat slow because intermediate results are written to disk.   
- Current MapReduce uses [Tez](../devlog/tez.md) acceleration to keep intermediate results in memory (very fast)   
- Operate on "Bigger than Database" amounts of data.   
   
### Advantages of Hadoop MapReduce   
   
   
- Uses a functional approach (original data is unchanged)   
- Restricted to one-way communication path   
- Provides the following features:   
  - Highly scalable(same user code)   
  - Easily managed workflow   
  - Hardware fault tolerant   
- MapReduce is powerful paradigm for solving problems   
- Often referred to as a "Data Parallel" or **S**ingle **I**nstrution **M**ultiple **D**ata problem (SIMD)   
   
### Programming Hadoop MapReduce   
   
   
- **Program Natively** using Java API (Either [Tez](../devlog/tez.md) or MapReduce)   
- Uses other languages like Python with the Streaming interface(stdin, stdout and text only)   
- Use the C++ Pipes interface.   
- Use higher level tools (e.g., [hive](../devlog/hive.md), Pig) on top of MapReduce or Tez acceleration   
- MapReduce applications can scale with no change to the application   
- Computation is moved close to the data in HDFS   
- There is no need to manage side-effects or process state   
- SW/HW faults in HDFS and YARN are handled by automatic restart of tasks, transparent to the application.   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.bnsj6fk5m18.png)   
   
## Examples (MapReduce in Parallel)   
   
### Word Count   
   
Determine how many times unique words are used in the following text.   
   
   
- `see spot run`   
- `run spot run`   
- `see the cat`   
   
A trivial task. How does MapReduce perform this at scale when a collection of document has 50 billion words?   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.upf9zn7wm2.png)   
   
We can add improvements to our mapper using a combiner   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.x9crxdaozq.png)   
   
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
   
## Simulating Map and Reduce using Python and Bash scripts   
   
Source: <[https://www.michael-noll.com/tutorials/writing-an-hadoop-mapreduce-program-in-python/>](https://www.michael-noll.com/tutorials/writing-an-hadoop-mapreduce-program-in-python/>)   
   
There are several methods to program a Hadoop MapReduce. The most direct and lowest level is using the Java Hadoop API or the C++ Pipes library.   
   
Many users prefer the flexibility of the Streams Interface that allows a variety of programming language to be used.   
   
This method will work with any program that can read and write TEXT DATA to [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md) and [stdout](../devlog/stdout.md).   
   
### Developing a Hadoop Streaming word counting application.   
   
   
- pymapper.py - a python word count mapper   
- shuffer.sh - a simulated shuffle step using bash script   
- pyreducer.py - a python word count reducer   
   
<!-- end list -->   
   
`{_obsidian_pattern_tag_!/usr/bin/env}` python   
    """pymapper.py"""   
   
    import sys   
   
# input comes from STDIN (standard input)   
    for line in sys.stdin:   
# remove leading and trailing whitespace   
        line = line.strip()   
# split the line into words   
        words = line.split()   
# increase counters   
        for word in words:   
# write the results to STDOUT (standard output);   
# what we output here will be the input for the   
# Reduce step, i.e. the input for reducer.py   
#   
# tab-delimited; the trivial word count is 1   
            print '%s\t%s' % (word, 1)   
   
`{_obsidian_pattern_tag_!/bin/bash}`   
# shuffle.sh   
    sort -k1,1   
   
`{_obsidian_pattern_tag_!/usr/bin/env}` python   
    """pyreducer.py"""   
   
    from operator import itemgetter   
    import sys   
   
    current_word = None   
    current_count = 0   
    word = None   
   
# input comes from STDIN   
    for line in sys.stdin:   
# remove leading and trailing whitespace   
        line = line.strip()   
   
# parse the input we got from mapper.py   
        word, count = line.split('\t', 1)   
   
# convert count (currently a string) to int   
        try:   
            count = int(count)   
        except ValueError:   
# count was not a number, so silently   
# ignore/discard this line   
            continue   
   
# this IF-switch only works because Hadoop sorts map output   
# by key (here: word) before it is passed to the reducer   
        if current_word == word:   
            current_count += count   
        else:   
            if current_word:   
# write result to STDOUT   
                print ('%s\t%s' % (current_word, current_count))   
            current_count = count   
            current_word = word   
   
# do not forget to output the last word if needed!   
    if current_word == word:   
        print ('%s\t%s' % (current_word, current_count))   
   
1\. Run the `pymapper.py` with some simple data and change the input words to key value pairs.   
   
    echo "see spot run run spot run see the cat" | ./pymapper.py   
   
2\. Sort the data passed through `pymapper.py`   
   
    echo "see spot run run spot run see the cat" | ./pymapper.py | ./shuffle.sh   
   
3\. Add the reducer stage and count all the same keys   
   
    echo "see spot run run spot run see the cat" | ./pymapper.py | ./shuffle.sh | ./pyreducer.py   
   
See also: [Tez](../devlog/tez.md), [apache spark](../topics/apache%20spark.md)