---
created: 20211124223442420
desc: ''
id: hmo5i20x0zc85t21ig14vnk
tags:
- '!/usr/bin/env'
- '!/bin/bash'
- '!/usr/bin/env'
title: MapReduce in Python
updated: 1653318643780
---
   
Topics::  [Data Engineering](/not_created.md)   
   
   
---   
   
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