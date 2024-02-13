# Container Network

Two or more containers could be member of single shared container network.

Linux Container hosts supports THREE container network drivers

Driver Name | Network Name | Allow user-defined network | Usage
-----------|---------------|---------------------------|---
Null  |   None   | Does not allow | Disable networking, allows air-tight containers
Host  |   host   | Does not allow | Containers directly exposed to HOST network
Bridge |  bridge | Does allow ! | Used for user-defined network and network isolation



## Demo 1 : Test `NONE` network

```bash
docker rm m1 -f
docker run --name m1 -d --net none nginx:alpine
docker exec -it m1 ping google.com
## Expect PING to fail !
## Press CTRL+C to stop execution
docker exec -it m1 hostname
docker rm m1 -f
```



## Demo 2 : Test `default bridge` network

```bash
docker rm m2 -f
docker run --name m2 -d  nginx:alpine
docker exec -it m1 ping google.com
## Expect PING to work !
## Press CTRL+C to stop execution
docker exec -it m1 hostname
## Expect an IP address
docker rm m2 -f
```


## Demo 3 : Test `Host` network

```bash
docker rm m3
docker run --name m3 -d --net host nginx:alpine
docker run --name m4 -d --net host nginx:alpine
## Expect m4 to fail 
docker rm m3 m4 -f
```

## Demo 4 : Test User defined bridge network

```bash
docker network create net1 --subnet 10.0.10.0/24
docker network create net2 --subnet 10.0.20.0/24
# Deploy TWO containers in net1
docker run --name m1 -d --net net1 nginx:alpine
docker run --name m2 -d --net net1 nginx:alpine
# Test the connectivity between two containers in SAME network
docker exec -t  m1 ping m2 -c 5
docker exec -t  m2 ping m1 -c 5
# Create ONE container in second network
docker run --name m3 -d --net net2 nginx:alpine
# Test the connectivity between TWO network
docker exec -t  m1 ping m3 -t 5
## EXPECTED FAILURE !!!
docker stop m1 m2 m3
docker rm m1 m2 m3
docker network rm net1 net2
```
