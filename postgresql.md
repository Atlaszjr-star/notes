* check the postgresql service on ubuntu
 ```
sudo systemctl status postgresql.service

 ```
* enter postgresql server without docker container
 ```
 # switch the user to postgres
 sudo su - postgres
 postgres@machine: 
 # default connection:
 psql # connect database postgres with postgres username
 # specific connection
 psql -d db_name -U user_name # connect specific database with user_name
 db_name-#: \l # check all databases at server
 db_name-#: \d + check all table in db_name
 db_name-#: SELECT * from table_name;
 db_name-#: \q # exit
 
 ```
 * enter posegresql server in docker container
 ```
 # enter the terminal of container as root user
 docker exec -it container_name /bin/bash
 # check the users list, if postgres exits
 cut -d :f1 /etc/passwd
 # switch user to postgres
 su - postgres
 postgres@container_name:
 psql -d db_name -U user_name # connect specific database with user_name
 db_name-#: \l # check all databases at server
 db_name-#: \d + check all table in db_name
 db_name-#: SELECT * from table_name;
 db_name-#: \q # exit
 ```
