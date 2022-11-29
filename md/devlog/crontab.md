---
created: '2022-05-14T00:00:00.000Z'
desc: ''
id: odlpzat6rl1hbfz3ph8xhil
title: crontab
updated: 1653306030627
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`crontab` has three different meanings:   
   
1. The text file that contains the users cron jobs can be called as user’s `crontabs`   
   
   - It is located at `/var/spool/cron/crontabs`   
2. The command `crontab` is used to manage the user’s crontabs files.   
3. It can also refer to the configuration file for the system-wide cron jobs called crontab located at `/etc/crontab`   
   
There are two types of cron jobs.   
   
   
- System-wide   
- Individual user cron jobs   
   
## Individual user cron jobs   
   
Each user has a crontab file which is short for crontable, where all scheduled cron jobs for that user are specified. These files are located at `/var/spool/cron/crontabs` (the exact location can differ from distros to distros).   
   
You edit these directly with a text editor or using the `crontab` command (recommended).   
   
To display the contents of the crontab file of the current user.   
   
```
crontab -l
```
   
   
To edit the current user’s crontab file   
   
```
crontab -e
```
   
   
To task to run has to be defined through a single line that consists of six fields separated by white space. The first five fields will define when the task will run and the last field will define the command or script to be run.   
   
```
m h dom mon dow command
```
   
   
If you use an `*` for a field it will represent “always” or “any value” for that field.   
   
Minimum time limit used is minute. If you want to run a task for every 15 seconds, cron cannot be used for such a job.   
   
### Examples   
   
   
- Run a backup script everyday at 6 AM (use 24 hours format)   
   
```
0 6 * * * /root/backup.sh

# specify dow as sunday

0 6 * * 0 /root/backup.sh
```
   
   
   
- Runs a script that monitors free disk space every minute.   
   
```
* * * * * /root/check_space.sh
```
   
   
If you want to specify a list of discreet values in a field use comma operator to separate.   
   
   
- Run a task at 4,6,10 AM   
   
```
0 4,6,10 * * * /root/check_space.sh
```
   
   
If you want to specify a range of values use hyphen operator.   
   
   
- Run a task on weekdays between 9 and 5 PM, once per hour. (during working days and hours)   
   
```
0 9-17 * * 1-5 /root/script.sh
```
   
   
You can use the slash operator to specify values that will be repeated over a certain interval.   
   
   
- Run a task every 3 days at 4 and 21 hours at 10 minutes   
   
```
10 4,21 */3 * * /root/script.sh
```
   
   
Common cron macros   
   
   
- `@yearly` - will run the task every year at 1st January midnight   
- `@monthly` - will run the task first day of every month   
- `@week` - will run the task weekly at midnight on the Sunday   
- `@daily` - will run the task once a day at midnight   
- `@hourly` - will run the task once every hour at the beginning of the hour   
- `@reboot` - will run the task at boot time   
   
```
*/2 * * * * date >> /tmp/date_and_time.txt
```
   
   
Monitor cron jobs via the cron log   
   
```
tail -f /var/log/syslog
```
   
   
To remove crontab file   
   
```
crontab -r
```
   
   
Edit/remove other user’s crontab   
   
```
sudo crontab -e -u userName
sudo crontab -r -u userName
```
   
   
### Footnotes   
   
   
- Use absolute path of the script in the crontab   
- `/etc/cron.allow` and `/etc/cron.deny` will decide which user is allowed to use crontab command.   
- [Crontab.guru - The cron schedule expression editor](https://crontab.guru/)   
- [Crontab Generator - Generate crontab syntax](https://crontab-generator.org/)   
   
## System-wide cron jobs   
   
   
- Simple move your scripts inside `/etc/cron.daily` `cron.hourly` `cron.monthly` `cron.weekly`   
   
### Footnotes   
   
   
- cronjobs are intended for machines and servers that run continuously, if the system is down when the cronjob is scheduled to run the task is lost. It will not be run when the machine runs.   
- [anacron](../devlog/anacron.md)