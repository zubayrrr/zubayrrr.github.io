---
created: 20211028203452220
desc: ''
id: oteklwrg0wgbzwqyjey8ijy
title: jobs
updated: 1653437796447
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`jobs` command is used to list the jobs that you are running in the background and in the foreground. If the prompt is returned with no information no jobs are present. All shells are not capable of running this command. This command is only available in the [csh](/not_created.md), [languages.bash](../devlog/languages.bash.md), [tcsh](/not_created.md), and [ksh](/not_created.md) shells.   
   
Jobs are maintained only by the current shell, hence the Job IDs are local to the current shell, you can have same Job IDs in different shells but the [PID](../devlog/pid.md) is maintained by the kernel and has global scope.   
   
### Options   
   
<table>   
<thead>   
<tr class="header">   
<th>JOB</th>   
<th>Job name or number</th>   
</tr>   
</thead>   
<tbody>   
<tr class="odd">   
<td>-l</td>   
<td>Lists process IDs in addition to the normal information.</td>   
</tr>   
<tr class="even">   
<td>-n</td>   
<td>List only processes that have changed status since the last notification.</td>   
</tr>   
<tr class="odd">   
<td>-p</td>   
<td>Lists process IDs only.</td>   
</tr>   
<tr class="even">   
<td>-r</td>   
<td>Restrict output to running jobs.</td>   
</tr>   
<tr class="odd">   
<td>-s</td>   
<td>Restrict output to stopped jobs.</td>   
</tr>   
</tbody>   
</table>   
   
### Process Control Commands   
   
`fg` command moves a [background process](../devlog/background%20process.md)in the current shell environment into the [foreground process](../devlog/foreground%20process.md). Use the job ID parameter to indicate a specific job to be run in the foreground. If this parameter is not supplied, the `fg` command uses the job most recently suspended, placed in the background, or run as a background job.   
   
`fg %JobID`   
   
`bg` is a job control command. It resumes suspended [[jobs] in the [background process](../devlog/background%20process.md), returning the user to the shell prompt while the job runs.   
   
`bg %Job_ID`