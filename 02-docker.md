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

