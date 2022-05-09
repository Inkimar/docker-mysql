# docker-mysql

## login
1. docker exec -it mysql bash

## erase volume

1. docker volume rm docker-mysql_dbmysql8 

## Map in SQL-files

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
