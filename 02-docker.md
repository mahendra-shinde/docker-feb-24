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

