---
created: '2022-05-12T00:00:00.000Z'
desc: ''
id: htsjiw0s9846otcxm6k9v4l
title: APT
updated: 1653304975752
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
**Apt** stands for **Advanced Package Tool**. It doesn’t deal with ‘**deb**‘ package and works directly, but works with ‘**deb**‘ archive from the location specified in the “**/etc/apt/sources.list**” file.   
   
   
- In the latest version of Ubuntu the `apt-get` and `apt-cache` tools were merged into a single command called `apt`   
- Unlike [dpkg](../devlog/dpkg.md), `apt` does not understand .deb files. It works with packages that are downloaded from repositories and calls dpkg directly after downloading the .deb archives.   
- An APT repository is a web server which contains a collection of packages with metadata that is readable by the apt tool.   
- A special kind of repository hosted on servers like Launchpad are [ppa](../devlog/ppa.md)s - such repositories are maintained by unofficial developers.   
   
The APT package index is basically a database that holds records of available packages from the repositories enabled in your system.   
   
To update the package index run the command below. This will pull the latest changes from the APT repositories:   
   
```
sudo apt update
```
   
   
## Install a local .deb file using `apt`   
   
```
sudo apt install /path-to-file/packageName.deb
```
   
   
## List upgradable packages   
   
```
sudo apt list --upgradable
```
   
   
## Upgrade the installed packages to their latest versions run   
   
```
sudo apt upgrade
```
   
   
## Full Upgrading (`apt full-upgrade`)   
   
The difference between `upgrade` and `full-upgrade` is that the latter will remove the installed packages if that is needed to upgrade the whole system.   
   
```
sudo apt full-upgrade
```
   
   
Be extra careful when using this command.   
   
## Remove an installed package   
   
```
sudo apt remove package_name
```
   
   
The `remove` command will uninstall the given packages, but it may leave some configuration files behind. If you want to remove the package including all configuration files, use `purge` instead of `remove` :   
   
```
sudo apt purge package_name
```
   
   
## Remove the unneeded dependencies   
   
```
sudo apt autoremove
```
   
   
## Clearing cache   
   
`/var/cache/apt/archives/`   
   
Contains all installed and upgraded packages   
   
```
ls -l /var/cache/apt/archives/
du -sh /var/cache/apt/archives/

sudo apt clean
```
   
   
## Listing Packages   
   
The `list` command allows you to list the available, installed and, upgradeable packages.   
   
To list all available packages use the following command:   
   
```
sudo apt list
```
   
   
## Search a package’s description   
   
```
apt search "search term"
```
   
   
## Get list of installed packages   
   
```
apt list --installed | wc -l
```
   
   
## Get package info   
   
```
apt show packageName
```
   
   
## Graphic package managers   
   
   
- Synaptic   
- Aptitude