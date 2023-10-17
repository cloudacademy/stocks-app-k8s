# Stocks API
Microservices Stock Application API

![Stocks App](/docs/stocks.png)

## Build Instructions

1. Build API container image:

    ```
    docker build -t cloudacademydevops/stocks-api:v2 .
    ```

## Container Launch Instructions

The API container image can be launched using the following commands:

- Starts the container instance with MYSQL connection and authentication details:

    ```
    docker run --rm -it --name stock-api --env DB_CONNSTR=jdbc:mysql://db_server:3306/cloudacademy --env DB_USER=admin --env DB_PASSWORD=secret123 -p 8080:8080 cloudacademydevops/stocks-api:v2
    ```
