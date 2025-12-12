---
author: Taro Gray
pubDatetime: 2025-12-12T15:00:00.00Z
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

## Network

In order to see the network IPAddress

```
docker container inspect --format '{ .NetworkSettings.IPAddress }' webhost
```

quick port check

```
docker container port <container name>
```

show networks to look up network id

```
docker network ls
```

```
docker network inspect <network id>
```

create a network

```
docker network create --driver
```

attach a network to container

```
docker network connect
```

detach a network from container

```
docker network disconect
```

creeate a container with specifying the network

```
docker run -d -p 8080:80 --name nginx --network network nginx
```

static ip address is not recommended by Docker, but rather Docker DNS is containers use by default
docker-dameon has a buit in DNS sever

create the nginx2 with the network, "docker_gogo"

```
docker run -d -p 8081:80 --network=docker_gogog --name nginx2 nginx
2b8c57408b88351ee678b2c501be2f598cfe4978ca9d809438975957a5a61059
```

within the docker_go network, add nginx2.

```
docker network connect docker_go  nginx2
```

check network id

```
 docker network ls
NETWORK ID     NAME                 DRIVER    SCOPE
9f1599995a4a   bridge               bridge    local
72331596c3b7   docker_go            bridge    local
b10dd591683a   docker_gogog         bridge    local
baa1f5aaaef3   freecodegram_sail    bridge    local
05f3b787a558   host                 host      local
343227fd7b74   none                 null      local
fc4e18c5d80c   turtorial-app_sail   bridge    local
```

inspect docker_go to make sure nginx2 is in the docker_go network or not

```
docker network inspect 72331596c3b7
```

made sure the containers are 2 within the network docker_go

```
  "Containers": {
            "2b8c57408b88351ee678b2c501be2f598cfe4978ca9d809438975957a5a61059": {
                "Name": "nginx2",
                "EndpointID": "b1ea409de8f9b32ad64e5f38220c66fcdd7f872657154c8cc3552333c645ddcc",
                "MacAddress": "f6:35:9c:f5:a5:55",
                "IPv4Address": "172.20.0.3/16",
                "IPv6Address": ""
            },
            "4f791e59270a5e4e9efd494c15aaf673b69747a59e4fdd7481a615679baf5deb": {
                "Name": "nginx",
                "EndpointID": "a75ee81060fa268ab73c0a1e854812d26f48564371c2984a0ec422e86019234c",
                "MacAddress": "8e:bb:84:50:55:d0",
                "IPv4Address": "172.20.0.2/16",
                "IPv6Address": ""
            }
```

ping is successfully done

```
 docker exec -it nginx ping nginx2
PING nginx2 (172.20.0.3) 56(84) bytes of data.
64 bytes from nginx2.docker_go (172.20.0.3): icmp_seq=1 ttl=64 time=0.117 ms
64 bytes from nginx2.docker_go (172.20.0.3): icmp_seq=2 ttl=64 time=0.234 ms
64 bytes from nginx2.docker_go (172.20.0.3): icmp_seq=3 ttl=64 time=0.181 ms
^C
--- nginx2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2078ms
rtt min/avg/max/mdev = 0.117/0.177/0.234/0.047 ms
```
