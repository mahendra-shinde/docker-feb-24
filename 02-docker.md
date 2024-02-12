# Docker : Container Platform

- Docker is a popular container platform (SDK)
- Docker is Available for Windows, Linux and Mac 
    - Docker Containers support Linux and Windows
    - On Mac, Docker runs linux containers

- Docker is available in TWO flavours

    - Docker Community edition (OSS and Free)

    - Docker Enterprise Editition (Managed by Mirantis) (Paid)

- Docker Desktop : Easier to use development platform

    - Supports Windows & Linux containers
    - Docker Desktop is available on Windows, Linux and Mac

    - Pre-requisites for Docker Desktop on Windows

        1. Windows 10/11 PRO or ENT 
        1. Enable `Virtualization` from System BIOS / EUFI
        1. Must Enable Windows Optional Features
            i. Containers (For Windows Server Containers)
            i. Virtual Machine Platform ( For WSL )
            i. Windows Subsystem for Linux (WSL)

    - Download and Install Docker Desktop on Machine

## Common Docker Commands

No. | Command | Description | Example Usage
----|---------|-------------|--------------
1  | info | Print all the details from Docker Daemon / Engine | docker info
2  | version | Print the version of docker client and server | docker version
3  | images | Print list of all `downloaded` images | docker images `or` docker image ls
4 | pull | Download image from registry | docker pull mahendrshinde/cowsay
5 | run | Launch a new instance from an image | docker run mahendrshinde/cowsay
6 | rmi | Remove a local image | docker rmi openjdk:11-jre-buster `or` docker image rm openjdk:11-jre-buster


## Demo 1 : Images and Layers

1.  Make sure there are no local images of OpenJDK

    ```bash
    docker rmi openjdk:11-jre-buster
    docker rmi openjdk:11-jdk-buster
    ```
1.  Try Downloading the JRE image

    ```
    docker pull openjdk:11-jre-buster
    ```

1.  Expected : Docker need to download SIX layers

1.  Try downloading the JDK image

    ```bash
    docker pull openjdk:11-jdk-buster
    ```

1.  Expected : Three layers are SKIPPED (Shared Layers with JRE)

1.  Delete all the images

    ```bash
    docker rmi openjdk:11-jre-buster
    docker rmi openjdk:11-jdk-buster
    ```


## Demo 2 : Launch a new instance from image

1. Method 1 : Basic RUN Command

    ```bash
    # Syntax : docker run IMAGENAME
    docker run mahendrshinde/cowsay
    ```

2. Method 2 : Execution mode : default / terminal

    ```bash
    # Syntax : docker run -t IMAGENAME
    docker run -t mahendrshinde/cowsay
    ```

    > Both with and without "-t" your output should be same.

3.  Method 3 : Execution mode : Detached / Background

    ```bash
    # Syntax : docker run -d IMAGENAME
    docker run -d mahendrshinde/cowsay
    ```

4.  Method 4 : Execution mode "Detached" with Logical name

    ```bash
    # Syntax : docker run --name CNAME -d IMAGENAME
    docker run --name c1 -d mahendrshinde/cowsay
    docker logs c1
    ```

5. Method 5 : Set port-forwarding to access containerized application from local port

    ```bash
    # Syntax : docker run -p HostPort:ContainerPort -d --name CNAME IMAGENAME
    docker run --name c1 -d -p 5000:8080 mahendrshinde/image-resizer
    ```

6. Using web-browser visit page http://localhost:5000

7.  Clean-up: stop and delete the recently created container

    ```bash
    docker stop c1
    docker rm c1
    ```

## Env Demo : Passing Environment Variables to Container

> Syntax

    docker run -e ENV1=VALUE1 -e ENV2=VALUE2 ... -e ENV1000=VALUE1000 IMAGENAME

1. Try creating MySQL Database instance without environment variables.

    ```bash
    docker run -d -p 3306 --name db1 mysql:8.0
    docker logs db1
    ```

    > Container failed to start, due to missing Environment variables

1.  Delete the failed container and create a new one with Environment variables

    ```bash
    docker rm db1

    docker run -d -p 3306 --name db1 -e MYSQL_ROOT_PASSWORD=Pass1234 -e MYSQL_USER=mahendra -e MYSQL_PASSWORD=pass1234 -e MYSQL_DATABASE=sample  mysql:8.0

    ```

    Alternative Method to pass Multiple Environment Variables through TEXT file

    ```bash
    docker run --name c2 -p 3306 -d --env-file db.txt mysql:8.0
    ```
    Where, db.txt should contain all variables like this:

    ```ini
    MYSQL_USER=mahendra
    MYSQL_DATABASE=sample
    MYSQL_PASSWORD=pass1234
    MYSQL_ROOT_PASSWORD=pass1234
    ```

1.  Test the database using `docker exec`

    ```bash
    docker exec -it db1 bash
    mysql -umahendra -ppass1234 
    use sample
    show tables;
    ## Empty set
    create table emp ( ename varchar(20), eid int primary key );
    show tables;
    exit
    exit
    ```

1.  Delete the container

    ```bash
    docker stop db1
    docker rm db1
    ```
