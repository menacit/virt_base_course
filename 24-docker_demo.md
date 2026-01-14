---
SPDX-FileCopyrightText: © 2026 Menacit AB <foss@menacit.se>
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
### Tooling for application containers

![bg right:30%](images/24-whale.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Milan Bhatt (CC BY-SA 2.0)" -->
## What is Docker?
Software for packaging/running 
applications and their dependencies
in predictable execution environments. 

Used for both development environments
and production deployment of software.

Users can download and execute an
**"application container image"** without
caring about messy compiler configuration,
incompatible software library versions
and similar boring/error-prone stuff -
just\* specify the image name and version!

![bg right:30%](images/24-whale.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Milan Bhatt (CC BY-SA 2.0)" -->
...same goes for application upgrades -
just\* ask users to bump the version tag and
they'll get everything they need to run
the next version of your fantastic app
in a predictable execution environment!

(Quite neat for software vendors)

![bg right:30%](images/24-whale.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Axelspace Corporation (CC BY-SA 4.0)" -->
## How does it work?
Instructions for how a container image
should be configured are defined as
code in a shareable "Dockerfile". 

These utilize pre-built OS/app images
that can be uploaded/downloaded from
a remote repository, like "Docker Hub".

Relies on OS-level virtualisation
(by default) to provide low overhead
and speedy execution of containers.

![bg right:30%](images/24-suez_canal_satellite.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Axelspace Corporation (CC BY-SA 4.0)" -->
Users should not to modify content
in the container images they use.

Everytime\* a container is updated
or restarted, it will be reset to
the specified container image
(a bit like a classic snapshot).

Persistent data should thefore be
stored outside of the container -
more about that later!

![bg right:30%](images/24-suez_canal_satellite.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Johannes P1hde (CC BY 2.0)" -->
**Let's take it for a spin!**

![bg right:30%](images/24-analog_ccc.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Thierry Ehrmann (CC BY 2.0)" -->
```
$ docker run -ti ubuntu:18.04

Unable to find image 'ubuntu:18.04' locally
18.04: Pulling from library/ubuntu
a055bf07b5b0: Pull complete 

root@79424287b988:/#
```

![bg right:30%](images/24-server_rack.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Freed eXplorer (CC BY 2.0)" -->
### kool_app/Dockerfile
```dockerfile
# Pre-built OS/application image used as base
# for container, downloaded from a remote registry
FROM python:3.11.0-alpine

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

<!--
https://hub.docker.com/_/python/
-->

---
```
$ cd kool_app
$ docker build --tag kool_app:0.2 .

Sending build context to Docker daemon  4.608kB

Step 1/5 : FROM python:3.11.0-alpine
Step 2/5 : RUN pip install Flask==2.2.2
Step 3/5 : COPY app.py .
Step 4/5 : USER 10000
Step 5/5 : CMD ["flask", "run", "--host", "0.0.0.0"]
Successfully tagged kool_app:0.2
```

```
$ docker run --publish 80:5000 kool_app:0.2

* Debug mode: off
* Running on all addresses (0.0.0.0)
```

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jack Lawrence (CC BY 2.0)" -->
```
$ curl http://127.0.0.1/api/request_info

{
  "browser": "curl/7.81.0",
  "ip_address": "172.17.0.1"
}
```

![bg right:30%](images/24-plastic_duck.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jack Lawrence (CC BY 2.0)" -->
If we upload our built container image
to a repository like "Docker Hub",
users can simply run:

```
$ docker \
    run --publish 80:5000 \
    example_company/kool_app:0.2
```

![bg right:30%](images/24-plastic_duck.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
```dockerfile
# Pre-built OS/application image used as base
# for container, downloaded from a remote registry
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
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Hrdina (CC BY-SA 2.0)" -->
Our demo application is
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
like a SQL database or
reverse proxy for HTTPS.  

We could try to document the
setup or write a bash script
to start our containers - meh!  

To handle these problems,
**"Docker Compose"** was created.

![bg right:30%](images/24-rogers_place.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
### nextcloud_env/docker-compose.yml
```yaml
services:
  db.example.test:
    image: "mysql:8.2"
    volumes:
      - "my_db_data:/var/lib/mysql"
    environment:
      MYSQL_ROOT_PASSWORD: "hunt_er2"
      MYSQL_DATABASE: "nextcloud"
      MYSQL_USER: "nextcloud"
      MYSQL_PASSWORD: "4pp.pass"

  app.example.test:
    image: "nextcloud:26.0.10"
    volumes:
      - "my_nextcloud_data:/var/www/html"
    environment:
      NEXTCLOUD_ADMIN_USER: "bob"
      NEXTCLOUD_ADMIN_PASSWORD: "hunt_er2"
      MYSQL_HOST: "db.example.test"
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
```yaml
services:
  db.example.test:
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
```yaml
[...]

  app.example.test:
    image: "nextcloud:26.0.10"
    volumes:
      - "my_nextcloud_data:/var/www/html"
    environment:
      NEXTCLOUD_ADMIN_USER: "bob"
      NEXTCLOUD_ADMIN_PASSWORD: "hunt_er2"
      MYSQL_HOST: "db.example.test"
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
$ cd nextcloud_env
$ docker compose up --detach

 [+] Running 2/2
 ✔ Container nextcloud-application-1  Started
 ✔ Container nextcloud-database-1     Started
```

![bg right:30%](images/24-rogers_place.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
```
$ cd nextcloud_env
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
<!-- _footer: "%ATTRIBUTION_PREFIX% Wzhkevin (CC BY-SA 4.0)" -->
## Further awesomeness
Tons of pre-built images on [Docker Hub](https://hub.docker.com/).  
  
Supports both OS-level and
(with some effort) HW-level virtualisation.  

Also works-ish on Windows and macOS.

![bg right:30%](images/24-maersk_huacho_container_ship.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% CGP Grey (CC BY 2.0)" -->
Hope you've enjoyed the introduction.  

We'll look at how Docker works in
detail later during the course.

In the meantime,
[Read The Fine Manual](https://docs.docker.com/engine/)!

Questions or clarifications?

![bg right:30%](images/24-bletchley_park_computer_wiring.jpg)
