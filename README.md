# docker-mysql

## login
1. docker exec -it mysql bash

## erase volume

1. docker volume rm docker-mysql_dbmysql8 

## Map in SQL-files
- Addt this directory to your host-system - `sql-script` 
- AND add that  directory to the volumes in the docker-compose.yml-file
- `- ./sql-script:/docker-entrypoint-initdb.d`
- put your sql-scripts in the `sql-script`-directory

## ability to change the logs from mysql 
- https://geshan.com.np/blog/2022/02/mysql-docker-compose/ - using docker-compose version 3.8
- see -> he cap_add set to SYS_NICE suppresses some not useful error messages. 

```
version: '3.8'
services:
  db:
    image: mysql:8.0
    cap_add:
      - SYS_NICE
```


# The docker-compose.yml-file

**docker-compose.yml-file**

```
version: '3.7'

services:
  db:
      image: mysql:5.7.30 
      container_name: mysql
      ports:
        - "3306:3306"
      restart: always
      volumes:
        - dbmysql:/var/lib/mysql
        - ./conf/my.cnf:/etc/mysql/my.cnf
      environment:
        - MYSQL_ROOT_PASSWORD=ingimar
      env_file:
        - ./.db.env
volumes:
  dbmysql:
```
