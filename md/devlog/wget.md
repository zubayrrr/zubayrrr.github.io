---
created: '2022-05-12T00:00:00.000Z'
desc: ''
id: zt6hnpeyl30i6jlbwa48eth
title: wget
updated: 1652815757654
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
GNU Wget is a command-line utility for downloading files from the web. With Wget, you can download files using HTTP, HTTPS, and FTP protocols. Wget provides a number of options allowing you to download multiple files, resume downloads, limit the bandwidth, recursive downloads, download in the background, mirror a website, and much more.   
   
The `wget` utility expressions take the following form:   
   
```sh
wget [options] [url]
```
   
   
Copy   
   
   
- `options` - The [Wget options](https://linux.die.net/man/1/wget)   
- `url` - URL of the file or directory you want to download or synchronize.   
   
## How to Download a File with `wget`   
   
In its simplest form, when used without any option, `wget` will download the resource specified in the [url] to the current directory.   
   
In the following example, we are downloading the Linux kernel tar archive:   
   
```
wget https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.17.2.tar.xz
```
   
   
During the download, `wget` shows the progress bar alongside the file name, file size, download speed, and the estimated time to complete the download. Once the download is complete, you can find the downloaded file in your current working directory .   
   
To turn off the output, use the `-q` option.   
If the file already exists, `wget` will add `.N` (number) at the end of the file name.   
   
## Saving the Downloaded File Under Different Name   
   
To save the downloaded file under a different name, pass the `-O` option followed by the chosen name:   
   
```
wget -O latest-hugo.zip https://github.com/gohugoio/hugo/archive/master.zip
```
   
   
## Downloading a File to a Specific Directory   
   
By default, `wget` will save the downloaded file in the current working directory. To save the file to a specific location, use the `-P` option:   
   
```
wget -P /mnt/iso http://mirrors.mit.edu/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1804.iso
```
   
   
The command above tells `wget` to save the CentOS 7 iso file to the `/mnt/iso` directory.   
   
## Limiting the Download Speed   
   
To limit the download speed, use the `--limit-rate` option. By default, the speed is measured in bytes/second. Append `k` for kilobytes, `m` for megabytes, and `g` for gigabytes.   
   
The following command will download the Go binary and limit the download speed to 1MB:   
   
```
wget --limit-rate=1m https://dl.google.com/go/go1.10.3.linux-amd64.tar.gz
```
   
   
This option is useful when you don’t want `wget` to consume all the available bandwidth.   
   
## Resuming a Download   
   
You can resume a download using the `-c` option. This is useful if your connection drops during a download of a large file, and instead of starting the download from scratch, you can continue the previous one.   
   
In the following example, we are resuming the download of the Ubuntu 18.04 iso file:   
   
```
wget -c http://releases.ubuntu.com/18.04/ubuntu-18.04-live-server-amd64.iso
```
   
   
If the remote server does not support resuming downloads, `wget` will start the download from the beginning and overwrite the existing file.   
   
## Downloading in Background   
   
To download in the background, use the `-b` option. In the following example, we are downloading the OpenSuse iso file in the background:   
   
```
wget -b https://download.opensuse.org/tumbleweed/iso/openSUSE-Tumbleweed-DVD-x86_64-Current.iso
```
   
   
By default, the output is redirected to `wget-log` file in the current directory. To watch the status of the download, use the [`tail`](https://linuxize.com/post/linux-head-command/) command:   
   
```
tail -f wget-log
```
   
   
## Changing the Wget User-Agent   
   
Sometimes when downloading a file, the remote server may be set to block the Wget User-Agent. In situations like this, to emulate a different browser, pass the `-U` option.   
   
```
wget --user-agent="Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" http://wget-forbidden.com/
```
   
   
The command above will emulate Firefox 60 requesting the page from `wget-forbidden.com`   
   
## Downloading Multiple Files   
   
If you want to download multiple files at once, use the `-i` option followed by the path to a local or external file containing a list of the URLs to be downloaded. Each URL needs to be on a separate line.   
   
The following example shows how to download the Arch Linux, Debian, and Fedora iso files using the URLs specified in the `linux-distros.txt` file:   
   
```
wget -i linux-distros.txt
```
   
   
linux-distros.txt   
   
```txt
http://mirrors.edge.kernel.org/archlinux/iso/2018.06.01/archlinux-2018.06.01-x86_64.iso
https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-9.4.0-amd64-netinst.iso
https://download.fedoraproject.org/pub/fedora/linux/releases/28/Server/x86_64/iso/Fedora-Server-dvd-x86_64-28-1.1.iso
```
   
   
Copy   
   
If you specify `-` as a filename, URLs will be read from the standard input.   
   
## Downloading via FTP   
   
To download a file from a password-protected FTP server, specify the username and password as shown below:   
   
```
wget --ftp-user=FTP_USERNAME --ftp-password=FTP_PASSWORD ftp://ftp.example.com/filename.tar.gz
```
   
   
## Creating a Mirror of a Website   
   
To create a mirror of a website with `wget`, use the `-m` option. This will create a complete local copy of the website by following and downloading all internal links as well as the website resources (JavaScript, CSS, Images).   
   
```
wget -m https://example.com
```
   
   
If you want to use the downloaded website for local browsing, you will need to pass a few extra arguments to the command above.   
   
```
wget -m -k -p https://example.com
```
   
   
The `-k` option will cause `wget` to convert the links in the downloaded documents to make them suitable for local viewing. The `-p` option will tell `wget` to download all necessary files for displaying the HTML page.   
   
or   
   
```
wget --mirror --convert-links --adjust-extension --page-requisites --no-parent https://example.com

# or

wget -mKEpnp https://example.com

```
   
   
## Skipping Certificate Check   
   
If you want to download a file over HTTPS from a host that has an invalid SSL certificate, use the `--no-check-certificate` option:   
   
```
wget --no-check-certificate https://domain-with-invalid-ss.com
```
   
   
## Downloading to the Standard Output   
   
In the following example, `wget` will quietly ( flag `-q`) download and output the latest WordPress version to stdout ( flag `-O -`) and pipe it to the `tar` utility, which will extract the archive to the `/var/www` directory.   
   
```
wget -q -O - "http://wordpress.org/latest.tar.gz" | tar -xzf - -C /var/www
```
   
   
> via - [Wget Command in Linux with Examples | Linuxize](https://linuxize.com/post/wget-command-examples/)