# Keep a container running inside a docker-compose file

    version: "3"
    services:
    ubuntu:
        image: ubuntu:latest
        tty: true # THIS PREVENT THE CONTAINER TO SHUT DOWN AUTOMATICALLY

# Connect to a container already running

    docker exec -it container_already_running bash