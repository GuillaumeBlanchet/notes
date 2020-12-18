# Keep a container running inside a docker-compose file

    version: "3"
    services:
    ubuntu:
        image: ubuntu:latest
        tty: true # THIS PREVENT THE CONTAINER TO SHUT DOWN AUTOMATICALLY

# Connect to a container already running

    docker exec -it container_already_running bash

# Connect to db with a mysql client:

    docker run -it --network {{net}} imega/mysql-client mysql --host={{host_name/container_name/ip address}} -uroot -p{{root_password}} -D {{my_database}}

# Connect to centos8

    docker run -it centos:8 bash

# Docker registry

## Create a local registry with a volume in the current directory

    docker container run -d -p 5000:5000 --name registry -v $(pwd)/registry-data:/var/lib/registry registry

## Push an image to your new local registry

    docker tag hello-world 127.0.0.1:5000/hello-world
    docker push 127.0.0.1:5000/hello-world
    

