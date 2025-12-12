---
author: Taro Gray
pubDatetime: 2025-12-12T00:00:00.00Z
title: Docker Commands I've learned so far
postSlug: docker-commands
featured: true
draft: false
tags:
  - docker
description: Here is docker commands which was useful and efificinet.
---

## Table of contents

## to check running containers

```
docker ps
```

```
docker container ls -a
```

## nginx, httpd, mysql

```
docker run -d -p 8080:80 nginx
docker run -d -p 80:80 httpd
```

in order to run mysql on port 3306

```
docker run -d \
  --name mysql \
  -d \
  -p 3306:3306 \
  -e MYSQL_RANDOM_PASSWORD=true \
  mysql
```

or

```
docker run -d \
  --name mysql \
  -p 3307:3306 \
  -e MYSQL_ROOT_PASSWORD=rootpass \
  mysql:8.0
```

login to mysql

```
docker exec -it mysql mysql -uroot -prootpass
```

## Docker is not the vm it is just a process

it's just a process

```
docker top <image name>
```

in order to see a process

```
ps aux | grep mongo
```

in order to check the port

```
lsof -i :80
```

## Docker list, details and status

process list of container

```
docker container top
```

details of container config

```
docker container inspect
```

performance stats for all containers

```
docker container stats
```
