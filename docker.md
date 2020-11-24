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
