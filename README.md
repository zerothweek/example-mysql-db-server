## initial project directory settings
1. choose mysql base image
    - eg. `mysql:8.2.0`

2. create docker volume
    ```bash
    docker volume create example-mysql-db-data
    docker volume ls
    ```
    ```callout
    - the above created volumes should be mounted on "/var/lib/mysql directory as specified in MySQL image docs.  
    - any databases  or tables created inside "example_mysql_db_data" will be persisted locally, even after the container is stopped or removed.
    ```
3. make a configuration file(directory)
    ```bash
    mkdir conf.d
    cd conf.d
    vim my.cnf # the standard file name and extension for a config file in the mysql image series is my.cnf
    ```

4. make `.env`

5. make `docker-compose.yml` 

## db-server & db-manager network connection
### same computer(way1)
1. create shared network for both containers
    ```bash
    docker network create example-mysql-db-network
    ```
2. add network settings in docker-compose.yml (both yaml files in server and manager container)
    ```yaml
    services:
    app:
        ...
        
        networks:
        - mysql-net

    networks:
    mysql-net:
        external: true
        name: example-mysql-db-network

    ```
### same computer(way2)

### different computer(way1)

### different computer(way2)


## basic mysql server usage
1. access the mysql cli inside docker container
    ```bash
    docker exec -it example_mysql_db_data mysql -u root -p
    ```
2. verify and select database
    ```sql
    mysql > SHOW DATABASES;
    mysql > USE my_db;
    ```