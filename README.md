# docker-compose-yml-example
version: "3.8"
services:

    redis:
        image: redis:latest
        container_name: "redis"
        ports:
            - 8080:80
        environment:
          MYSQL_ROOT_PASSWORD: 1q2w3e4r5t
        networks:
          - default
    db:
      image: mysql:8.0
      container_name: 'mysql'
      ports:
         - 3306:3306
      command: --default-authentication-plugin=mysql_native_password
      networks:
          - default
      environment:
            MYSQL_ROOT_PASSWORD: 1q2w3e4r5t 
        volumes:
          - ./database/mysql:/var/lib/mysql
          - ./database/logs:/var/log/mysql
        networks:
            - default
    mariadb:
      image: mariadb:latest
      container_name: 'mariadb'
      ports:
         - 8080:3306
      command: --default-authentication-plugin=mysql_native_password
      networks:
          - default
      environment:
            MARIADB_ROOT_PASSWORD: 1q2w3e4r5t 
        volumes:
          - ./database/mariadb:/var/lib/mariadb
          - ./database/logs:/var/log/mariadb
        networks:
            - default
    mongodb:
      image: mongodb:latest
      container_name: 'mongo'
      ports:
         - 27017>27017
      command: --default-authentication-plugin=mysql_native_password
      networks:
          - default
      environment:
        MONGO_INITDB_ROOT_USERNAME: root
        MONGO_INITDB_ROOT_PASSWORD: 1q2w3e4r5t
        volumes:
          - ./database/mariadb:/var/configdb
        networks:
            - default
networks:
    default:
        driver: bridge
