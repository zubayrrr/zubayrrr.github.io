---
created: 1652622340718
desc: ''
id: 059kx1yxhp3rjgzxnqlddti
tags:
- '1'
- 14](https://youtube/DuDz6B4cqVc)
- 7)](https://wwwyoutubecom/watch?v=D6xkbGLQesk)
- '1:'
title: The Data Engineering Interview Study Guide
updated: 1652622340718
---
   
   
---   
created: 2022-02-16   
title: The Data Engineering Interview Study Guide   
tags:   
   
  - clips   
  - articles   
---   
   
The Data Engineering Interview Study Guide   
==========================================   
   
For your FAANG and other technical interviews   
   
---------------------------------------------   
   
Interviewing for any technical position generally requires preparing, studying, and long, all-day interviews.   
   
Data engineering interviews, like other technical interviews, require plenty of preparation. There are a number of subjects that need to be covered in order to ensure you are ready for back-to-back questions.   
   
Some positions require [Hadoop](https://hadoop.apache.org/), others [SQL](https://en.wikipedia.org/wiki/SQL). Some roles require understanding statistics, while still others require heavy amounts of system design.   
   
We have gathered many of the resources that we have used to study and get jobs at companies in the FAANG family as well as other major tech companies. We have yet to find one that requires you to know anything about Hadoop during the interview, so that has not been included in this study guide.   
   
We recommend asking the recruiter if you aren’t sure which type of interview you will be facing. Some companies are very good at keeping interviews consistent, but even then, teams can deviate depending on what they are looking for. Here are some examples of what we have noticed about some companies' data engineering interviews.   
   
**Amazon —** SQL- and database-design heavy as well as general ETL design. Surprisingly, no Python.   
   
**Netflix —**SQL- and code-heavy, with the expectation that you can not only write SQL and code but can optimize them.   
   
> _“They asked about SQL queries to find time difference between two events given certain condition. ” — Netflix data engineer on Glassdoor_   
   
**Expedia** — Big Data questions, like what is Spark and RDDs, as well as SQL and Python.   
   
Due to this variance, we’ve created a checklist to keep track of what subject areas you have already studied and what you still need to cover: [data engineering study checklist](https://docs.google.com/spreadsheets/d/1GOO4s1NcxCR8a44F0XnsErz5rYDxNbHAHznu4pJMRkw/edit#gid=0).   
   
Also, I recently created a [video guide](https://www.youtube.com/watch?v=2lloOlnSzSs&t=1s) to walk through the data engineering interview study guide.   
   
Let’s get started with SQL.   
   
SQL   
===   
   
As a data engineer, it is almost inevitable that you will get some SQL questions. As someone who has participated in many interviews for a lot of top tech companies, like Amazon and Capital One, I know that they usually follow some similar patterns.   
   
Typically there will be at least one question that requires an aggregation with a filter, another that requires a few joins, and then one that requires a subquery. Along with that, there might be a few curveball questions that require self-joins, recursions, and analytic functions. So let’s look at a couple of concepts that are good to cover.   
   
Pre-video SQL problems   
   
----------------------   
   
These first few problems will help you gauge where you are on different concepts. That way you can take notes on the study guide, and go back and review what you feel you were not comfortable with.   
   
1.  [262\. Trips and Users](https://leetcode.com/problems/trips-and-users/)   
2.  [601\. Human Traffic of Stadium](https://leetcode.com/problems/human-traffic-of-stadium/)   
3.  [185\. Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/)   
4.  [197\. Rising Temperature](https://leetcode.com/problems/rising-temperature/)   
5.  [626\. Exchange Seats](https://leetcode.com/problems/exchange-seats/)   
6.  [The Report](https://www.hackerrank.com/challenges/the-report/problem)   
7.  [177\. Nth Highest Salary](https://leetcode.com/problems/nth-highest-salary/)   
8.  [Symmetric Pairs](https://www.hackerrank.com/challenges/symmetric-pairs/problem)   
9.  [Occupations](https://www.hackerrank.com/challenges/occupations/problem)   
10.  [Ollivander’s Inventory](https://www.hackerrank.com/challenges/harry-potter-and-wands/problem)   
11.  [Placements](https://www.hackerrank.com/challenges/placements/problem)   
   
Videos   
   
------   
   
[Learning about ROW\_NUMBER and Analytic Functions](https://www.youtube.com/watch?v=QFj-hZi8MKk)   
   
[Advanced Implementation Of Analytic Functions Running Total](https://www.youtube.com/watch?v=G3kYPzLWtpo&t=4s)   
   
[Advanced Implementation Of Analytic Functions Median](https://www.youtube.com/watch?v=XecU6Ieyu-4&t=54s)   
   
[Wise Owl SQL Videos](https://www.youtube.com/watch?v=2-1XQHAgDsM&list=PL6EDEB03D20332309)   
   
Post-video SQL problems   
   
-----------------------   
   
Once you have finished watching the SQL videos above, consider trying the new problems below. Try to see if you feel like you are improving. Again, note down any specific topics you feel weak on.   
   
1.  [Binary Tree Nodes](https://www.hackerrank.com/challenges/binary-search-tree-1/problem)   
2.  [595\. Big Countries](https://leetcode.com/problems/big-countries/)   
3.  [626\. Exchange Seats](https://leetcode.com/problems/exchange-seats/)   
4.  [Weather Observation Station 18](https://www.hackerrank.com/challenges/weather-observation-station-18/problem)   
5.  [Challenges](https://www.hackerrank.com/challenges/challenges/problem)   
6.  [Print Prime Numbers](https://www.hackerrank.com/challenges/print-prime-numbers/problem)   
7.  [SQL Interview Questions: 3 Tech Screening Exercises (For Data Analysts)](https://data36.com/sql-interview-questions-tech-screening-data-analysts/)   
   
Databases, ETL, and Data Warehouses   
===================================   
   
Source: [Stackoverflow](https://stackoverflow.com/questions/20346850/sql-movie-database-diagram)   
   
For database, [ETL](https://seattledataguy.substack.com/p/what-are-etls-and-why-we-use-them), and [data warehouse](https://www.theseattledataguy.com/what-are-the-benefits-of-cloud-data-warehousing-and-why-you-should-migrate/#page-content) design questions, we have gathered some books and videos we hope will help you out when it comes to explaining your design in an interview. In addition, we have listed a few plausible database/DW concepts you could attempt to design out on your own.   
   
We recommend going through the videos and at least skimming the Data Warehouse Toolkit before attempting the self-practice problems.   
   
[The Data Warehouse Toolkit](https://www.kimballgroup.com/data-warehouse-business-intelligence-resources/books/data-warehouse-dw-toolkit/)  by Ralph Kimball   
   
[Designing a Traditional Relational Database Video](https://www.youtube.com/watch?v=I_rxqSJAj6U)   
   
[Data Warehouse Design Video](https://www.youtube.com/watch?v=--OJpdPeH80)   
   
Self-practice problems   
   
----------------------   
   
For this part of your interview practice, we are going to list a few business systems that you can try to design out. First, we recommend designing a relational database, then thinking about how you would design an ETL and DW that rely on that relational DB.   
   
**Note:** In addition, we have found it very common that interviewers will base their interview questions on your design. So think about some of the questions you could answer with your DB and list them.   
   
Design a database/ETL and DW for a:   
   
*   dating app   
*   bicycle rental service   
*   music streaming app   
*   job search website   
*   Udemy-like website   
   
These are just a few ideas. We hope they help you have a clearer idea of what you can practice modeling and designing. Take some time to think about how users interact with these websites before getting started.   
   
Programming Problems   
====================   
   
Data engineers do a significant amount of programming in their daily life. There are several specific languages data engineers use. Python is arguably the most common.   
   
If the role requires a lot of Hadoop work, then [Java](https://www.java.com/en/) is also a useful language to have. There are a few other useful languages, like Java and [PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.1) (if you work at a Microsoft shop).   
   
There are two types of questions we have experienced. Some interviewers will ask you more operational questions. Others will ask classic algorithm and data structure questions.   
   
Operational Programming Problems   
================================   
   
Operational interview questions are harder to prep for. There are no “classic” interview questions here. However, they are also often easier to figure out on the spot. Algorithm interview questions usually have some sort of trick. Like the balanced brackets problem: If you don’t know you need to use queues, it will be very difficult to get to the correct answer.   
   
Operational problems, however, will be more focused on workflows and business processes. So as long as you are good at walking through real problems, this should be easier. Here are some problems that are great for prepping. We find it is helpful to know how to use arrays and dictionaries. Beyond that, there isn’t too much more required.   
   
1.  [Kangaroo problem](https://www.hackerrank.com/challenges/kangaroo/problem)   
2.  [Breaking records](https://www.hackerrank.com/challenges/breaking-best-and-worst-records/problem)   
3.  [Find a string](https://www.hackerrank.com/challenges/find-a-string/problem)   
4.  [itertools.permutations()](https://www.hackerrank.com/challenges/itertools-permutations/problem)   
5.  [No idea!](https://www.hackerrank.com/challenges/no-idea/problem)   
6.  [Days of the programmer](https://www.hackerrank.com/challenges/day-of-the-programmer/problem)   
7.  [Leaderboard](https://www.hackerrank.com/challenges/climbing-the-leaderboard/problem)   
8.  [Word order](https://www.hackerrank.com/challenges/word-order/problem)   
9.  [Sherlock and squares](https://www.hackerrank.com/challenges/sherlock-and-squares/problem)   
10.  [Equalize the array](https://www.hackerrank.com/challenges/equality-in-a-array/problem)   
11.  [Apples and oranges](https://www.hackerrank.com/challenges/apple-and-orange/problem)   
12.  [More operational style questions](https://www.hackerrank.com/domains/python)   
   
Algorithms and Data Structures   
==============================   
   
Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)   
   
Before going too deep into data structure and algorithms, let’s do a quick check to see how you are currently doing in this area. We have listed eight LeetCode problems that vary in difficulty. Try these out and try to gauge yourself on how long it takes you, as well as how many hints you needed. If you are following along with the study guide, then note this down. At the end of this list are a few more questions. So once you have watched all the videos, consider doing those problems, and see if you feel like you are improving!   
   
Pre-study problems   
   
------------------   
   
1.  [985\. Sum of even numbers after queries](https://leetcode.com/problems/sum-of-even-numbers-after-queries/)   
2.  [657\. Robot return to origin](https://leetcode.com/problems/robot-return-to-origin/)   
3.  [961\. N-repeated element in size 2N array](https://leetcode.com/problems/n-repeated-element-in-size-2n-array/)   
4.  [110\. Balanced binary tree](https://leetcode.com/problems/balanced-binary-tree/)   
5.  [3\. Longest substring without repeating characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)   
6.  [19\. Remove Nth node from end of list](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)   
7.  [23\. Merge k sorted lists](https://leetcode.com/problems/merge-k-sorted-lists/)   
8.  [31\. Next permutation](https://leetcode.com/problems/next-permutation/)   
   
Now that you have gone through these eight questions and shaken off the rust, let’s start reviewing these concepts.   
   
**Data structures**   
   
-------------------   
   
1.  [Data Structures & Algorithms `{_obsidian_pattern_tag_1}` — What Are Data Structures?](https://www.youtube.com/watch?v=bum_19loj9A)   
2.  [Data Structures: Linked Lists](https://youtu.be/njTh_OwMljA)   
3.  [Data Structures: Trees](https://youtu.be/oSWTXtMglKE)   
4.  [Data Structures: Heaps](https://youtu.be/t0Cq6tVNRBA)   
5.  [Data Structures: Hash Tables](https://youtu.be/shs0KM3wKv8)   
6.  [Data Structures: Stacks and Queues](https://youtu.be/wjI1WNcIntg)   
7.  [Data Structures: Crash Course Computer Science `{_obsidian_pattern_tag_1}`4](https://youtu.be/DuDz6B4cqVc)   
8.  [Data Structures: Tries](https://www.youtube.com/watch?v=zIjfhVPRZCg)   
   
**Algorithms**   
   
--------------   
   
1.  [Python Algorithms for Interviews](https://www.youtube.com/watch?v=p65AHm9MX80)   
2.  [Algorithms: Graph Search, DFS, and BFS](https://www.youtube.com/watch?v=zaBhtODEL0w&list=PLX6IKgS15Ue02WDPRCmYKuZicQHit9kFt)   
3.  [Algorithms: Binary Search](https://youtu.be/P3YID7liBug)   
4.  [Algorithms: Recursion](https://youtu.be/KEEKn7Me-ms)   
5.  [Algorithms: Bubble Sort](https://youtu.be/6Gv8vg0kcHc)   
6.  [Algorithms: Merge Sort](https://youtu.be/KF2j-9iSf4Q)   
7.  [Algorithms: Quicksort](https://youtu.be/SLauY6PpjW4)   
   
**Big O notation**   
   
------------------   
   
[Introduction to Big O Notation and Time Complexity (Data Structures & Algorithms `{_obsidian_pattern_tag_7)](https://wwwyoutubecom/watch?v=D6xkbGLQesk)}`   
   
**Some interview walk-throughs**   
   
--------------------------------   
   
[Amazon Coding Interview Question — Recursive Staircase Problem](https://www.youtube.com/watch?v=5o-kdjv7FD0)   
   
[Google Coding Interview — Universal Value Tree Problem](https://www.youtube.com/watch?v=7HgsS8bRvjo)   
   
[Google Coding Interview Question and Answer `{_obsidian_pattern_tag_1}`: First Recurring Character](https://www.youtube.com/watch?v=GJdiM-muYqc)   
   
Post-video problems   
   
-------------------   
   
Once you have finished the videos above, consider trying the algorithm and data structure problems below. Make sure you keep track of how comfortable you felt when working on the problems.   
   
1.  [Bigger is greater](https://www.hackerrank.com/challenges/bigger-is-greater/problem)   
2.  [6\. Zigzag conversion](https://leetcode.com/problems/zigzag-conversion/)   
3.  [7\. Reverse integer](https://leetcode.com/problems/reverse-integer/)   
4.  [40\. Combination sum II](https://leetcode.com/problems/combination-sum-ii/)   
5.  [43\. Multiply strings](https://leetcode.com/problems/multiply-strings/)   
6.  [Larry’s array](https://www.hackerrank.com/challenges/larrys-array/problem)   
7.  [Short palindrome](https://www.hackerrank.com/challenges/short-palindrome/problem)   
8.  [65\. Valid number](https://leetcode.com/problems/valid-number/)   
   
If you still feel like you need help, then consider taking a [course on algorithms and data structures](https://www.udemy.com/course/coding-interview-bootcamp-algorithms-and-data-structure/).   
   
Big Data Frameworks   
===================   
   
Back in 2020, I made a video about practicing for a data engineering interview. Funny thing was, a person commented about the video and pointed back to my original data engineering study guide. Just by happenstance!   
   
Small world.   
   
They also added another section. In this case, they added [Spark](https://en.wikipedia.org/wiki/Apache_Spark). So for those of you out there needing to study for Spark, here is what Paul Russel added to the checklist. What would you add?   
   
[Architecture Overview & Use Cases](https://www.toptal.com/spark/introduction-to-apache-spark)   
   
[Spark by Examples (tutorial documentation)](https://sparkbyexamples.com/spark/)   
   
[PySpark Syntax Cheat Sheet](https://s3.amazonaws.com/assets.datacamp.com/blog_assets/PySpark_SQL_Cheat_Sheet_Python.pdf)