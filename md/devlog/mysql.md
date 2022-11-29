---
created: 1655989813131
desc: ''
id: ypszfixe0p3s5k0inqs5g08
title: MySql
updated: 1658169178236
---
   
## Remove all those previous dangling MySQL packages   
   
```bash
sudo service mysql stop  #or mysqld
sudo killall -9 mysql
sudo killall -9 mysqld
sudo apt-get remove --purge mysql-server mysql-client mysql-common
sudo apt-get autoremove
sudo apt-get autoclean
sudo deluser mysql
sudo rm -rf /var/lib/mysql
sudo apt-get purge mysql-server-core-5.5
sudo apt-get purge mysql-client-core-5.5

sudo apt remove --purge mysql-server
sudo apt purge mysql-server
sudo apt autoremove
sudo apt autoclean
sudo apt remove dbconfig-mysql
```
   
   
## Install MySQL Server   
   
```bash
sudo apt update
sudo apt upgrade
sudo apt install mysql-server

mysql --version # check your mysql version
sudo mysql_secure_installation
```
   
   
## Test MySQL & Check if it’s Running   
   
```bash
systemctl status mysql.service

sudo mysql -u root # Log in to your MySQL Server
```
   
   
## Troubleshooting   
   
If it `sudo mysql_secure_installation` throws an error when setting up password such as:   
   
```
... Failed! Error: SET PASSWORD has no significance for user 'root'@'localhost' as the authentication method used doesn't store authentication data in the MySQL server. Please consider using ALTER USER instead if you want to change authentication parameters.
```
   
   
Do   
   
```bash
sudo mysql
```
   
   
```sql
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'your_password';
mysql> exit
```
   
   
and then proceed with `sudo mysql_secure_installation`   
   
## MySQL Workbench   
   
Download the package and install it.   
   
Store the `root` password in the keychain and test the connection.