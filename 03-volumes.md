# Volumes

- Container Volumes are "Independent" of container instances.
- Volumes May / May not be attached to any container.
- A Single container may have Zero or More volumes.
- A Single volume might be attached to more than ONE instance.


# Kind of Volume mounts

1. Local `Named` volumes

    docker volume create db_vol

    docker volume rm db_vol

    > You cant delete volume which is attached to atleast ONE instance.

## Local volume demo

    1. Create a new Named volume 'vol1'

        `docker volume create vol1`
    
    1.  Create a new instance named 'c1' to use 'vol1'

        ```bash
        docker volume inspect vol1
        docker run --name c1 -v vol1:/data -d nginx:alpine
        ```

    1.  Get inside the instance and create files in /data directory

        ```bash
        docker exec -it c1 sh
        cd /data
        echo "Hello World" > file1.txt
        ls -l
        exit
        ```

    1.  Delete the container and recreate it

        ```bash
        docker stop c1
        docker rm c1
        docker run --name c2 -v vol1:/data -d nginx:alpine
        docker exec -it c2 sh
        ls /data
        exit
        ```

1.  Host-Path containers (Ad-Hoc)

    > Syntax:
        
        docker run -v HOST-PATH:GUEST-PATH <Image>

    > Example:
        
        docker run --name c2 -v D:\mysite:/usr/share/nginx/html -p 30003:80 -d nginx:alpine

    > Make sure folder d:\mysite exists and has one HTML file `index.html`
            
