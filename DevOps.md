* VS Code connect to the container in remote server
1. in the remote server
```shell
# create new container from image but add port mapping 22 in container to 5050 in server host
docker run -d ....... -p 5050:22 ......
# enter the container
docker exec -it container_name /bin/bash
```
2. in the container of remote server
```shell
# install openssh and ssh
apt-get update
apt-get install openssh-server
apt-get install openssh-client
apt-get install ssh
apt-get install nano

# change the config file of ssh
nano /etc/ssh/sshd_config
# add following lines
Port 22
PermitRootLogin yes # allow root user login with ssh
  
# restart ssh service
/etc/init.d/ssh restart
# keep ssh service always running
systemctl enable ssh
#(check ssh status and restart)
sudo service ssh status    
sudo service ssh start
# assign password for root
passwd
# exit the container
exit
```
  
3. in the local machine
```
# ssh connection test
ssh root@ip_address_server -p 5050
```
4. in VS Code of local machine<br>
  
&emsp; 4.1 install remote ssh extension in VS code, then Click **REMOTE EXPLORER** and select SSH target <br>
&emsp; 4.2 open the config file and type:
  ```
  Host any_host_name
    HostName ip_address_remote_server
    Port 5050
    User root
  ```
&emsp; 4.3 Connect to host in new window, select OS (Linux Server)<br>
&emsp; 4.4 Open Folder, then you can connect to the container in remote server<br>
