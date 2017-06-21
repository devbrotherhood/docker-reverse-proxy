# Docker Reverse Proxy

### About

This solutions is used to bind multiple domains in specific port to docker contained applications, making it possible to have multiple containers running on different ports but responding to a standard port such as 80 for example.

### How to use

In this solution we use the "docker-compose" tool. To do this work just run the command below and add your host domain to "/etc/hosts":

```
    docker-compose up
```

### Create Your Own Reverse Proxy

The settings used by docker-compose are located inside the file "docker-compose.yml".

You can customise "docker-compose.yml" and create according to your need.

Below is an example of "docker-compose.yml" using reverse proxy.


```
version: '2'

services:
  nginx-proxy:
    image: jwilder/nginx-proxy
    ports:
      - "80:80"
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock
      - ./conf/my_proxy.conf:/etc/nginx/conf.d/my_proxy.conf:ro

  webapp1:
    image: 'wordpress'
    container_name: 'blog1'
    expose:
      - "81"
    environment:
      - "VIRTUAL_HOST=teste.local"
    links:
      - "nginx-proxy"
```


