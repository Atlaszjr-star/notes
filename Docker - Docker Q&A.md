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

 
