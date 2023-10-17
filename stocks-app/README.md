# Stocks App
Microservices Stock Application

![Stocks App](/docs/stocks.png)

## Build Instructions

1. Build the `cloudacademydevops/stocks-app` frontend UI container image. Run the multi-stage Dockerfile:

    ```
    docker build -t cloudacademydevops/stocks-app .
    ```

## Container Launch Instructions

The UI container image can be launched using the following commands:

- Starts the container instance with Nginx `proxy_pass` enabled for the `/api/stocks/csv` path, useful for demonstrating service discovery on downstream components etc:

    ```
    docker run --rm -it --name stock-app --env NGINX_APP_APIHOSTPORT=api.10.0.0.100.nip.io:8000 --env NGINX_DNS_RESOLVER=8.8.8.8 -p 8080:8080 cloudacademydevops/stocks-app
    ```

- Starts the container instance **without** the Nginx `proxy_pass` enabled for the `/api/stocks/csv` path:

    ```
    docker run --rm -it --name stock-app -p 8080:8080 cloudacademydevops/stocks-app:v2
    ```
