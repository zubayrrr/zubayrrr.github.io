---
created: 1658681068587
desc: ''
id: im2u3jgpjxpzdutxmkd6gbw
title: Website Monitoring
updated: 1659958490512
---
   
Related::  [languages.python](../devlog/languages.python.md)   
   
   
---   
   
1. Create a Server (maybe on Linode).   
2. Install Docker on the Server.   
3. Run [Ngnix](/not_created.md) container.   
   
   - Which will give you access to an application running in the browser.   
4. Write a Python program to check the endpoint of the application. Checks status of the application.   
5. Send email when website is down.   
6. Automatically restart Docker container or restart the Server.   
   
   
---   
   
## 1. Create Server & Run Ngnix Container   
   
1. Create a Linode server   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1659938531/wiki/vdqdsm7nrdv6ovpcb4oh.png)   
   
2. [SSH](../devlog/ssh.md) into that server from your local machine   
3. Install [docker](../devlog/docker.md)   
4. Run `ngnix` container   
   
   - `docker run -d -p 8080:80 ngnix`   
5. Access the application running on the server using it’s public IP.   
   
## 2. Website Request   
   
```python
# pip install requests smtplib os paramiko linode_api4 time schedule

import requests
import smtplib
import os
import paramiko
import linode_api4
import time
import schedule

EMAIL_ADDRESS = os.environ.get('EMAIL_ADDRESS')
EMAIL_PASSWORD = os.environ.get('EMAIL_PASSWORD')
LINODE_TOKEN = os.environ.get('LINODE_TOKEN')


def restart_server_and_container():
    # restart linode server
    print('Rebooting the server...')
    client = linode_api4.LinodeClient(LINODE_TOKEN)
    nginx_server = client.load(linode_api4.Instance, 24920590)
    nginx_server.reboot()

    # restart the application
    while True:
        nginx_server = client.load(linode_api4.Instance, 24920590)
        if nginx_server.status == 'running':
            time.sleep(5)
            restart_container()
            break


def send_notification(email_msg):
    print('Sending an email...')
    with smtplib.SMTP('smtp.gmail.com', 587) as smtp:
        smtp.starttls()
        smtp.ehlo()
        smtp.login(EMAIL_ADDRESS, EMAIL_PASSWORD)
        message = f"Subject: SITE DOWN\n{email_msg}"
        smtp.sendmail(EMAIL_ADDRESS, EMAIL_ADDRESS, message)


def restart_container():
    print('Restarting the application...')
    ssh = paramiko.SSHClient()
    ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    ssh.connect(hostname='139.162.130.236', username='root', key_filename='/Users/nanajanashia/.ssh/id_rsa')
    stdin, stdout, stderr = ssh.exec_command('docker start c3e706bc905e')
    print(stdout.readlines())
    ssh.close()


def monitor_application():
    try:
        response = requests.get('http://li1388-236.members.linode.com:8080/')
        if response.status_code == 200:
            print('Application is running successfully!')
        else:
            print('Application Down. Fix it!')
            msg = f'Application returned {response.status_code}'
            send_notification(msg)
            restart_container()
    except Exception as ex:
        print(f'Connection error happened: {ex}')
        msg = 'Application not accessible at all'
        send_notification(msg)
        restart_server_and_container()


schedule.every(5).minutes.do(monitor_application)

while True:
    schedule.run_pending()
```
