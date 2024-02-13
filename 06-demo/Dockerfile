# MANDATORY : Set the Base image 
FROM ubuntu:latest

# Update the package cache and then install package cowsay
RUN apt update -y && apt install cowsay -y

# Set application/process/shell for auto-start on new containers
# USE 'ENTRYPOINT' of base image if this line is missing from Dockerfile
ENTRYPOINT [ "/usr/games/cowsay" ]

# An Argument passed to ENTRYPOINT
CMD ["hello world"]
