# nginx-load-balancer

### Create docker container with nginx and configer load balancer

**Setup Upstream & proxy_pass in config file**

```
upstream my-app {
    server <your first server ip>:<first server port> weight=1;
    server <your second server ip>:<first second port> weight=1;
}

```

```

server {
    listen 80;
    location / {
        proxy_pass http://my-app;
    }
}

```

**Create docker file which take nginx docker image and set custom config file into nginx server**

```

FROM nginx:1.13.8-alpine
RUN rm /etc/nginx/conf.d/default.conf
COPY config/nginx.conf /etc/nginx/conf.d/

```

**Create nginx server container image**

```

docker build -t nginx-balancer .

```

**Run container image(nginx server)**

```

docker run -p 8080:80 -d nginx-balancer

```

**Note:** First docker need to setup into your system 
