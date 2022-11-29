---
created: '2022-05-14T00:00:00.000Z'
desc: ''
id: rlcdhrpciu8t7lesnwerjw7
title: anacron
updated: 1653306024464
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
**Anacron** is used to run commands periodically with a frequency defined in days. It works a little different from [crontab](../devlog/crontab.md); assumes that a machine will not be powered on all the time.   
   
It is appropriate for running daily, weekly, and monthly scheduled jobs normally run by cron, on machines that will not run 24-7 such as laptops and desktops machines.   
   
Assuming you have a scheduled task (such as a **backup script**) to be run using cron every midnight, possibly when your asleep, and your desktop/laptop is off by that time. Your backup script will not be executed.   
   
However, if you use **anacron**, you can be assured that the next time you power on the desktop/laptop again, the backup script will be executed.   
   
Anacron is run automatically when the system starts. The tasks will have root privileges. The frequency of the jobs is expressed in days not in minutes.   
   
The file that specifies anacron jobs is located at `/etc/anacrontab`   
   
`run-parts` will run all the executable files found in a directory.   
   
There are four fields that define an anacron job.   
   
1. Period in days   
   
   - `1` will specify everyday, `7` specifies every week.   
2. Delay in minutes   
   
   - Specifies how long anacron will wait before executing a job.   
3. Job identifier - must be unique   
   
   - Is the name of the file that is created under `/var/spool/anacron` - job timestamp file. Will indicate the last time the job was run. It also identifies the jobs in messages and logs.   
4. The command to be executed   
   
## Examples   
   
```
2    1    backup    /root/backup.sh
2    1    backup    date >> /tmp/anacron.txt
```
   
   
Check for errors in the anacrontab file using   
   
```
anacron -T
```
   
   
To run a anacron job in foreground or check status   
   
```
anacron -d
```
