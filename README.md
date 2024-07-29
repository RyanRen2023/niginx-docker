
# Nginx-Docker Example

This project demonstrates how to run Nginx as a web server in a Docker environment. The setup includes a Dockerfile for building a custom Nginx image, a docker-compose file for orchestrating the services, and example HTML content to be served by Nginx.

## Table of Contents

- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Setup](#setup)
  - [Step 1: Clone the Repository](#step-1-clone-the-repository)
  - [Step 2: Build the Docker Image](#step-2-build-the-docker-image)
  - [Step 3: Start the Docker Compose](#step-3-start-the-docker-compose)
- [Accessing the Web Server](#accessing-the-web-server)
- [Stopping the Services](#stopping-the-services)

## Project Structure

```plaintext
nginx-docker
├── docker-compose.yml
├── Dockerfile
├── html
│   └── index.html
└── nginx
    └── nginx.conf

  • docker-compose.yml: Defines the Docker services.
  • Dockerfile: Custom Docker image for Nginx.
  • html/index.html: Example HTML file to be served by Nginx.
  • nginx/nginx.conf: Configuration file for Nginx.
```

## Requirements

  • Docker
  • Docker Compose

## Setup

### Step 1: Clone the Repository

Clone this repository to your local machine:

```sh
git clone https://github.com/RyanRen2023/niginx-docker.git
cd nginx-docker
```

### Step 2: Build the Docker Image

Build the custom Nginx Docker image using the provided Dockerfile:

```sh
docker build -t custom-nginx .
```

### Step 3: Start the Docker Compose

Start the Nginx service using Docker Compose:

```sh
docker-compose up -d
```

## Accessing the Web Server

Once the services are up and running, you can access the web server by opening your web browser and navigating to:

```plaintext
http://localhost
```

You should see a message saying “Success! Nginx is running in a Docker container.”

## Stopping the Services

To stop the running services, use the following command:

```sh
docker-compose down
```

## Example Configuration Files

### docker-compose.yml

```yaml
version: '3'
services:
  nginx:
    image: custom-nginx:latest
    container_name: nginx_server
    ports:
      - "80:80"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./html:/usr/share/nginx/html
```

### Dockerfile

```Dockerfile
FROM nginx:latest
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./html /usr/share/nginx/html
```

### html/index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to Nginx on Docker!</title>
</head>
<body>
    <h1>Success! Nginx is running in a Docker container.</h1>
</body>
</html>
```

### nginx/nginx.conf

```conf
events {
    worker_connections 1024;
}

http {
    server {
        listen 80;
        server_name localhost;

        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }
}
```

Feel free to customize the files and configurations to fit your needs. If you encounter any issues or have any questions, please open an issue on the repository.
