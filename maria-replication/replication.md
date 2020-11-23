# Create first the folder holding the data

    mkdir /tmp/mariadb/ && chmod 777 /tmp/mariadb/

then you can docker-compose up -d.

# Scale the number of slaves using:

    $ docker-compose up --detach --scale mariadb-master=1 --scale mariadb-slave=3

# Connect to master with a mysql client:

    docker run -it --network maria-replication_default imega/mysql-client mysql --host=maria-replication_mariadb-master_1 -uroot -pmaster_root_password -D my_database

# Connect to slave with a mysql client

    docker run -it --network maria-replication_default imega/mysql-client mysql --host=maria-replication_mariadb-slave_1 -uroot -pmaster_root_password -D my_database

# Connect to the master with bash:

    docker exec -it maria-replication_mariadb-master_1 bash

# Tell a slave to not replicate a group of tables:

First [connect to the slave](#connect-to-slave-with-a-mysql-client), then ignore what you want:

    STOP SLAVE;
    SET GLOBAL replicate_wild_ignore_table='my_database.example%';
    START SLAVE;

Then check if it works: [connect to the master](#connect-to-master-with-a-mysql-client) and add an example1 table:

    CREATE TABLE my_database.example1 (test varchar(128));
    CREATE TABLE my_database.test1 (test varchar(128));

Check what tables have been synchronized:

    docker run -it --network maria-replication_default imega/mysql-client mysql --host=maria-replication_mariadb-slave_1 -uroot -pmaster_root_password -D my_database --execute='show tables;'

You should see only test1

[see doc for more tricks](https://mariadb.com/kb/en/replication-filters/)

Or you can set the MARIADB_EXTRA_FLAGS environment variable in the docker-compose file:

    MARIADB_EXTRA_FLAGS='--replicate-wild-ignore-table=my_database.example%'

# Troubleshooting

    docker-compose logs -f mariadb-master