---
category: '2022'
created: 2022-12-15 15:16:52.794000+00:00
id: 1e958b8c-27e3-41e8-a14e-212f745c1510
tags:
- devlog
title: Compare Two Csv Files
updated: 2022-12-15 15:16:53.370000+00:00
---
   
Topics:: [languages.python](../devlog/languages.python.md)   
   
   
---   
   
Here is a simple script that you can use to compare the differences between two `.csv` files containing security group information.   
   
```python
# Import the necessary libraries
import csv
import sys

# Define the names of the two files to compare
file1 = "quarterly_report.csv"
file2 = "monthly_report.csv"

# Read the contents of the first file into a list
with open(file1, 'r') as f:
  data1 = [row for row in csv.reader(f)]

# Read the contents of the second file into a list
with open(file2, 'r') as f:
  data2 = [row for row in csv.reader(f)]

# Compare the contents of the two files and print any differences
for i in range(len(data1)):
  for j in range(len(data1[i])):
    if data1[i][j] != data2[i][j]:
      print("Difference at row {} column {}:".format(i, j))
      print("  File 1: {}".format(data1[i][j]))
      print("  File 2: {}".format(data2[i][j]))
```
   
   
To use this script, simply save it to a file (e.g. "compare_csv.py") and run it from the command line using `python compare_csv.py`. This will compare the two .csv files specified in the `file1` and `file2` variables, and print out any differences that it finds.