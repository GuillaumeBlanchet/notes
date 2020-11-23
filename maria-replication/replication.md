# Create first the folder holding the data

    mkdir /tmp/mariadb/

# Scale the number of slaves using:

    $ docker-compose up --detach --scale mariadb-master=1 --scale mariadb-slave=3

# Connect to master with a mysql client:

    docker run -it --network maria-replication_default imega/mysql-client mysql --host=maria-replication_mariadb-master_1 -uroot -pmaster_root_password -D my_database

# Connect to slave with a mysql client:

    docker run -it --network maria-replication_default imega/mysql-client mysql --host=maria-replication_mariadb-slave_1 -uroot -pmaster_root_password -D my_database

# Connect to the master with bash:

    docker exec -it maria-replication_mariadb-master_1 bash

# Troubleshooting

    docker-compose logs -f mariadb-master