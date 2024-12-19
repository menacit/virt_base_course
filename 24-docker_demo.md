---
SPDX-FileCopyrightText: © 2024 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Docker demo"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Demonstration of Docker for virtualised development"
keywords:
  - "virtualisation"
  - "docker"
  - "container"
  - "vm"
  - "demo"
  - "demonstration"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Milan Bhatt (CC BY-SA 2.0)" -->
# Docker demonstration
### Tooling behind application containers

![bg right:30%](images/24-whale.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Milan Bhatt (CC BY-SA 2.0)" -->
## What is Docker?
Software for packaging/running 
applications and their dependencies
in predictable execution environments. 

Users can download and execute an
**"application container"** without caring
about code interpreter configuration,
software library versions, startup scripts
and similar boring/error-prone stuff. 

![bg right:30%](images/24-whale.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Milan Bhatt (CC BY-SA 2.0)" -->
## How does it work?
Instructions for how a VM should be
configured are defined as code in
shareable "Dockerfiles". 

"Images" are pre-configured OS images
that can be uploaded/downloaded from
a remote repository, like "Docker Hub".

Relies on OS-level virtualisation
(by default) to provide low overhead
and speedy execution of guests.

![bg right:30%](images/24-whale.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Thierry Ehrmann (CC BY 2.0)" -->
```
$ docker run -ti ubuntu:18.04 /bin/bash

Unable to find image 'ubuntu:18.04' locally
18.04: Pulling from library/ubuntu
a055bf07b5b0: Pull complete 

root@79424287b988:/#
```

![bg right:30%](images/24-server_rack.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
```dockerfile
# Pre-built OS/application image used as base
# for guest downloaded from a remote registry
FROM debian:bookworm-slim

# Commands to run during the build process
# to install dependencies, configure
# options and similar
RUN apt-get update \
    && apt-get install -y curl qrencode

# Copy source code and other application
# artifacts into guest image
COPY my_script.sh /usr/local/bin/

# Instructions for how the guest should
# be executed when run by a user
CMD /usr/local/bin/my_script.sh --fetch
```

![bg right:30%](images/24-containers.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Freed eXplorer (CC BY 2.0)" -->
```dockerfile
# Pre-built OS/application image used as base
# for guest downloaded from a remote registry
FROM python:3.11.0

# Commands to run during the build process
# to install dependencies, configure
# options and similar
RUN pip install Flask==2.2.2

# Copy source code and other application
# artifacts into guest image
COPY app.py .

# Instructions for how the guest should
# be executed when run by a user
USER 10000
CMD ["flask", "run", "--host", "0.0.0.0"]
```

![bg right:30%](images/24-tunnel.jpg)

---
```
$ docker build --tag kool_app:0.2 .

Sending build context to Docker daemon  4.608kB

Step 1/5 : FROM python:3.11.0
Step 2/5 : RUN pip install Flask==2.2.2
Step 3/5 : COPY app.py .
Step 4/5 : USER 10000
Step 5/5 : CMD ["flask", "run", "--host", "0.0.0.0"]
Successfully tagged kool_app:0.2
```

```
$ sudo docker run --publish 5000:5000 kool_app:0.2

* Debug mode: off
* Running on all addresses (0.0.0.0)
```

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
Our example application is
quite simple - let's grab a
more complex/realistic example...

I choose you, Nextcloud!

![bg right:30%](images/24-containers.jpg)

---
![bg center 100%](images/24-nextcloud_home.png)

---
![bg center 100%](images/24-nextcloud_setup_1.png)

---
![bg center 100%](images/24-nextcloud_setup_2.png)

---
![bg center 100%](images/24-nextcloud_setup_3.png)

---
![bg center 100%](images/24-nextcloud_setup_4.png)

---
![bg center 100%](images/24-nextcloud_setup_5.png)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
```
$ docker run \
  --publish 80:80 \
  --volume my_nextcloud_data:/var/www/html \
  --env NEXTCLOUD_ADMIN_USER=bob \
  --env NEXTCLOUD_ADMIN_PASSWORD=hunt_er2 \
  docker.io/library/nextcloud:26.0.10
```

![bg right:30%](images/24-containers.jpg)


---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
The number of command line flags
to our `docker run` is growing.  

Might need other components to
properly run our application,
like a proper database or
reverse proxy for HTTPS.  

We could try to document the
setup or write a bash script
to start our containers.  

To handle these problems,
**"Docker Compose"** was created.

![bg right:30%](images/24-rogers_place.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
### nextcloud/docker-compose.yml
```yaml
services:
  database:
    image: "mysql:8.2"
    volumes:
      - "my_db_data:/var/lib/mysql"
    environment:
      MYSQL_ROOT_PASSWORD: "hunt_er2"
      MYSQL_DATABASE: "nextcloud"
      MYSQL_USER: "nextcloud"
      MYSQL_PASSWORD: "4pp.pass"

  application:
    image: "nextcloud:26.0.10"
    volumes:
      - "my_nextcloud_data:/var/www/html"
    environment:
      NEXTCLOUD_ADMIN_USER: "bob"
      NEXTCLOUD_ADMIN_PASSWORD: "hunt_er2"
      MYSQL_HOST: "database"
      MYSQL_DATABASE: "nextcloud"
      MYSQL_USER: "nextcloud"
      MYSQL_PASSWORD: "4pp.pass"
    ports:
      - "8080:80"

volumes:
  my_db_data: {}
  my_nextcloud_data: {}
```

![bg right:30%](images/24-rogers_place.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
### nextcloud/docker-compose.yml
```yaml
services:
  database:
    image: "mysql:8.2"
    volumes:
      - "my_db_data:/var/lib/mysql"
    environment:
      MYSQL_ROOT_PASSWORD: "hunt_er2"
      MYSQL_DATABASE: "nextcloud"
      MYSQL_USER: "nextcloud"
      MYSQL_PASSWORD: "4pp.pass"

[...]
```

![bg right:30%](images/24-rogers_place.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
### nextcloud/docker-compose.yml
```yaml
[...]

  application:
    image: "nextcloud:26.0.10"
    volumes:
      - "my_nextcloud_data:/var/www/html"
    environment:
      NEXTCLOUD_ADMIN_USER: "bob"
      NEXTCLOUD_ADMIN_PASSWORD: "hunt_er2"
      MYSQL_HOST: "database"
      MYSQL_DATABASE: "nextcloud"
      MYSQL_USER: "nextcloud"
      MYSQL_PASSWORD: "4pp.pass"
    ports:
      - "8080:80"
```

![bg right:30%](images/24-rogers_place.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
```
$ docker compose up --detach

 [+] Running 2/2
 ✔ Container nextcloud-application-1  Started
 ✔ Container nextcloud-database-1     Started
```

```
$ docker compose stop

 [+] Stopping 2/2
 ✔ Container nextcloud-application-1  Stopped
 ✔ Container nextcloud-database-1     Stopped 
```

![bg right:30%](images/24-rogers_place.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
Options in the "docker-compose.yml" file
can be utilized to configure secrets,
health/ready checks, networking,
restart behavior, etc.  

For more complex orchestration needs,
[Kubernetes](https://kubernetes.io/) is a popular alternative.

![bg right:30%](images/24-rogers_place.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Freed eXplorer (CC BY 2.0)" -->
## Further awesomeness
Makes it easy to build immutable systems.

Tons of pre-built images on [Docker hub](https://hub.docker.com/).  
  
Supports both OS-level and
(with some effort) HW-level virtualisation.  

![bg right:30%](images/24-tunnel.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Freed eXplorer (CC BY 2.0)" -->
Hope you've enjoyed the introduction.  

We'll get back to how Docker
works in detail later!

In the meantime,
[Read The Fine Manual](https://docs.docker.com/engine/)!

![bg right:30%](images/24-tunnel.jpg)
