# Building Container Images

- Container image could be built from an existing BASE image.
- Image could be built using `Declarative` approach, which uses `Dockerfile`
- Or `Imperative` approach which uses `docker commit` command

## Building Image using `docker commit`

```bash
# Create a new TEMP container from base image `nginx:alpine`
docker run --name t1 -d -p 30005:80 nginx:alpine
# Test the container
curl http://localhost:30005
# Get inside the t1 container and make changes
docker exec -it t1 sh
cd /usr/share/nginx/html
# Delete the original webpage
rm index.html
echo "<h2>Hello World</h2>" > index.html
exit
# Test the container
curl http://localhost:30005
# Expect different response 'Hello World'
# Stop and Capture container t1
# To create new image "myapp"
docker stop t1
docker commit t1 myapp
docker images myapp
# Delete the TEMP container t1
docker rm t1
# Test the container
docker run --name t1 -d -p 30006:80 myapp
curl http://localhost:30006
```