# Building Application Image (PHP)

- Choose / select Base Image for application 
- Write Dockerfile 
- build using Docker CLI

    `docker build -t phpapp . `

- test by running a new container

    ```bash
    docker run --name p1 -d -p 30010:80 phpapp
    curl http://localhost:30010
    ```

- Clean up

    `docker rm -f p1`
