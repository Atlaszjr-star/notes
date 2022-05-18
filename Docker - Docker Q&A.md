---
tags: [Docker]
title: Docker Q&A
created: '2022-05-09T21:15:39.038Z'
modified: '2022-05-10T09:54:44.622Z'
---

# Docker Q&A

* How to mount a volume from network drive to container/dir in host
```shell
docker volume create --driver local --opt type=cifs --opt device=//network-drive-ip-address/mounted_dir --opt o=user=username, password=userpwd volume_name
docker run --name=container_name -dit -v volume_name:/container/dir image_name
#enter the /bash in container
docker exec -it container_name /bin/bash
```  
* How to remove all containers
```shell
docker rm -f $(docker ps -aq)
```
* Check the 8080 ports and all ports
```
sudo netstat -ntlp | grep :8080
# tcp        0      0 127.0.0.1:8080          0.0.0.0:*               LISTEN      131801/puma 5.3.2 ( 
sudo lsof -i -P -n | grep :8080
```
* Check the ip address of running container
```
sudo docker inspect container_id
sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' 9292ba15652a
```
* Docker overrules UFW!
[docker overruls UFW](https://chjdev.com/2016/06/08/docker-ufw/)

* Some ufw checking
```
 sudo ufw enable
 sudo ufw disable
 sudo ufw allow port/tcp
 sudo ufw status verbose
```
* Clean a port in host
```
netstat -tulnap        // list all ports and processes
netstat -anp|grep "port_number"     // show port details
sudo fuser -k Port_Number/tcp       // free the port needed
# or
lsof -n -i :'port-number' | grep LISTEN  // get port details
# sample  response:  java   4744 (PID)  test  364u  IP0 asdasdasda   0t0  TCP *:port-number (LISTEN)
kill -9 PID  // free port
```

* How to allow the ports of services in nginx (config with ufw), because nginx always follows the ufw rules, if the port is not allowed in ufw, then not accessable from outside machine in the LAN
 ```
 # option 0: disable ufw
 sudo ufw disable
 # option 1: allow the specific port in ufw
 sudo ufw allow port_num/tcp
 sudo ufw status numbered
 # option 2: add nginx to ufw
 sudo cd /etc/ufw/application.d/nginx
 #[Nginx xxx]
 #title=Nginx Web Server (HTTP + HTTPS)
 #description=Small, but very powerful and efficient web server
 #ports=new_port_num, 80,443/tcp
 sudo ufw app update Nginx xxx
 sudo ufw allow "Nginx xxx"
 # then Nginx can be seen in:
 sudo ufw status
 
 ```
