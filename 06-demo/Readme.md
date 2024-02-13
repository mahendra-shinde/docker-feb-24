# Build using Dockerfile 

1. Must create a new directory / folder for Dockerfile
1. Create a Dockerfile with no extension
1. To Build, make sure to get INSIDE the directory

    ```bash
    cd 06-demo
    ls
    docker build -t cow . 
    ```

1.  Test the image by creating containers

    ```bash
    docker run cow 
    docker run cow "The quick brown fox jumps over the lazy dog."
    ```