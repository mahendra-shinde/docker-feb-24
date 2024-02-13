# Docker Compose : Manage Multi-container Applications

1. docker-compose is used for managing multi-container applications.

1. Valid compose file names 

    - compose.yaml
    - compose.yml
    - docker-compose.yaml
    - docker-compose.yml


1. Typical Syntax for docker-compose

    ```yml
    version: '3.5'
    
    volumes:
        vol_name:

    networks:
        net_name:

    services:
        app_name:
            image:
            env:
    ```

1.  Run entire solution

    ```
    docker-compose up -d
    docker-compose ps
    ```

> For more compose demos visit https://github.com/mahendra-shinde/docker-compose-demos 