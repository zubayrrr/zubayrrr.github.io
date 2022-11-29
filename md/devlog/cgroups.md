---
created: 1655733625294
desc: ''
id: kgtifubcsyxu0xja4llap2q
title: Cgroups
updated: 1655733818570
---
   
cgroups (abbreviated from control groups)   
   
Cgroup is a linux feature to limit, police, and account the resource usage for a set of processes. It provides mechanism to limit and monitor system resources like CPU time, system memory, disk bandwidth, network bandwidth, etc.   
   
The cgroups works by dividing resources into groups and then assigning tasks to those groups.   
   
Docker uses cgroups to limit the system resources.   
   
When you install Docker binary on a linux box like ubuntu it will install cgroup related packages and create subsystem directories. You can list all the subsystems that you can manage using cgroups via the `lscgroup` command.   
   
```bash
$ lscgroup
cpuset:/
cpu:/
cpuacct:/
memory:/
devices:/
freezer:/
blkio:/
perf_event:/
hugetlb:/
```
   
   
If `lscgroup` is not installed, then you can install it using sudo apt-get install cgroup-bin command.   
   
Via - [How Docker uses cgroups to set resource limits? – Shekhar Gulati](https://shekhargulati.com/2019/01/03/how-docker-uses-cgroups-to-set-resource-limits/)