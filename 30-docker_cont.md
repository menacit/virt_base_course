---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Docker revisited"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Recap/Continueation of Docker in virtualisation course"
keywords:
  - "virtualisation"
  - "container"
  - "docker"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% NASA (CC BY 2.0)" -->
# Docker revisited

![bg right:30%](images/30-space_walk.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% NASA (CC BY 2.0)" -->
Docker's primary focus is to package/run
applications and their dependencies in a
predictable execution environment.  

**Let's take a deeper look at
how it achieves this!**

![bg right:30%](images/30-space_walk.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Rod Waddington (CC BY-SA 2.0)" -->
## Let's run a container!
```
$ docker run \
  --publish 8080:80 \
  --volume my_nextcloud_data:/var/www/html \
  docker.io/library/nextcloud:26.0.10
```

![bg right:30%](images/30-green_cabling.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
## Fetching container image
```
Unable to find image 'nextcloud:26.0.10' locally
26.0.10: Pulling from library/nextcloud
af107e978371: Already exists
6480d4ad61d2: Already exists
[...]
e9daddf7d237: Pull complete
d929539deed8: Pull complete
Digest: sha256:7f053b3fd21391e08[...]ec9c1fe7a7
```

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jorge Franganillo (CC BY 2.0)" -->
## Observing application output
```
Initializing nextcloud 26.0.10.1 ...
New nextcloud instance
Initializing finished
[...]
[mpm_prefork:notice] [pid 1] AH00163:
Apache/2.4.57 (Debian) PHP/8.2.14 configured
-- resuming normal operations
[core:notice] [pid 1] AH00094:
Command line: 'apache2 -D FOREGROUND'
```

![bg right:30%](images/30-bumper_cars.jpg)

---
![bg center 75%](images/30-nextcloud_setup.png)

---
![bg center 75%](images/30-nextcloud_landing.png)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Martin Fisch (CC BY 2.0)" -->
Hmm, a lot just happened there.  

Let's try to brake it down step-by-step!

![bg right:30%](images/30-squirell.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Rod Waddington (CC BY-SA 2.0)" -->
## Let's run a container!
```
$ docker run \
  --publish 8080:80 \
  --volume my_nextcloud_data:/var/www/html \
  docker.io/library/nextcloud:26.0.10
```

![bg right:30%](images/30-green_cabling.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Rod Waddington (CC BY-SA 2.0)" -->
The `docker` CLI utility is a client
speaking HTTP with the **Docker daemon**.  
  
Can be used to run and interact with
containers on local/remote hosts.  
  
Sub-command "run" provides hundreds
of different option flags to control
how the container is executed,
such as CPU and RAM limits.

`docker.io/library/nextcloud:26.0.10`
indicates which **container image**
should be used...

![bg right:30%](images/30-green_cabling.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Rod Waddington (CC BY-SA 2.0)" -->
```
$ docker volume inspect my_nextcloud_data
[
  {
    "Name": "my_nextcloud_data",
    "Driver": "local",
    "Labels": null,
    "Mountpoint":
"/var/lib/docker/volumes/my_nextcloud_data/_data",

    "Options": null,
    "Scope": "local"
  }
]
```

![bg right:30%](images/30-green_cabling.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Rod Waddington (CC BY-SA 2.0)" -->
The `docker` CLI utility is a client
speaking HTTP with the **Docker daemon**.  
  
Can be used to run and interact with
containers on local/remote hosts.  
  
Sub-command "run" provides hundreds
of different option flags to control
how the container is executed,
such as CPU and RAM limits.

`docker.io/library/nextcloud:26.0.10`
indicates which **container image**
should be used...

![bg right:30%](images/30-green_cabling.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
## Fetching container image
```
Unable to find image 'nextcloud:26.0.10' locally
26.0.10: Pulling from library/nextcloud
af107e978371: Already exists
6480d4ad61d2: Already exists
[...]
e9daddf7d237: Pull complete
d929539deed8: Pull complete
Digest: sha256:7f053b3fd21391e08[...]ec9c1fe7a7
```

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
The container image is a bundle containing all
files, scripts and code libraries required to
run an application predictably. 
  
Could be compared to a ZIP file of a
"debootstrapp'ed" directory used in
previous examples with `chroot`.  

Container images are typically stored/shared
using a repository such as "Docker Hub".    

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
How do we create container images?  

Typically, a "Dockerfile" and the
command `docker build` is used...

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
```dockerfile
# Name of existing image to use as base
FROM debian:bookworm-slim

# Command(s) executed inside container
# during image build process
RUN apt-get update \
    && apt-get install -y curl qrencode

# Copies file from host into container
COPY my_script.sh /usr/local/bin/

# Metadata indicating to container runtime
# which program to execute on start-up
CMD /usr/local/bin/my_script.sh --fetch
```

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
```
$ docker build --tag my_script:v2.3 .

=> [internal] load build definition from
Dockerfile [...]
=> [1/3] FROM debian:bookworm-slim
  => resolve docker.io/library/
  debian:bookworm-slim@sha256:bac354c[...]
=> [2/3] RUN apt-get update [...]
=> [3/3] COPY my_script.sh /usr/local/bin/
=> exporting to image
[+] Building 13.3s (8/8) FINISHED

$ docker image save my_script:v2.3 \
  > container_image-my_script-v2.3.tar
```

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
```dockerfile
# Minify client side assets (JavaScript)
FROM node:latest AS build-js

RUN npm install gulp gulp-cli -g
WORKDIR /build
COPY . .
RUN npm install --only=dev && gulp

# Build Golang binary
FROM golang:1.15.2 AS build-golang

WORKDIR /go/src/github.com/gophish/gophish
COPY . .
RUN go get -v && go build -v

# Runtime container
FROM debian:stable-slim

WORKDIR /opt/gophish
COPY --from=build-golang \
  /go/src/github.com/gophish/gophish/ ./

COPY --from=build-js \
  /build/static/js/dist/ ./static/js/dist/

[...]
```

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jorge Franganillo (CC BY 2.0)" -->
## Observing application output
```
Initializing nextcloud 26.0.10.1 ...
New nextcloud instance
Initializing finished
[...]
[mpm_prefork:notice] [pid 1] AH00163:
Apache/2.4.57 (Debian) PHP/8.2.14 configured
-- resuming normal operations
[core:notice] [pid 1] AH00094:
Command line: 'apache2 -D FOREGROUND'
```

![bg right:30%](images/30-bumper_cars.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jorge Franganillo (CC BY 2.0)" -->
Most of the heavy lifting is
delegated to [containerd](https://containerd.io/).  
  
Shared component used by several
container management tools besides Docker,
like Kubernetes, "Pouch" and balenaEngine.  

Uses `runc` by default to spawn containers
using OS-level virtualisation, but supports
other runtimes like `runhcs` (Windows) and
[Kata](https://katacontainers.io/) (HW-level virtualisation).

![bg right:30%](images/30-bumper_cars.jpg)

---
![bg center 75%](images/30-nextcloud_setup.png)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Rod Waddington (CC BY-SA 2.0)" -->
## Tweaking application configuration
```
$ docker run \
  --publish 8080:80 \
  --volume my_nextcloud_data:/var/www/html \
  --env NEXTCLOUD_ADMIN_USER=bob \
  --env NEXTCLOUD_ADMIN_PASSWORD=hunt_er2 \
  docker.io/library/nextcloud:26.0.10
```

![bg right:30%](images/30-green_cabling.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
The number of command line flags
to our `docker run` is growing.  

Might need other components to
properly run our application,
like a database or web server.  

We could try to document the
setup or write a bash script
to start our containers.  

To handle these problems,
"Docker Compose" was created.

![bg right:30%](images/30-rogers_place.jpg)

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

![bg right:30%](images/30-rogers_place.jpg)

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

![bg right:30%](images/30-rogers_place.jpg)

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

![bg right:30%](images/30-rogers_place.jpg)

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

$ docker compose rm --volumes --force

 [+] Removing 2/2
 ✔ Container nextcloud-application-1  Removed
 ✔ Container nextcloud-database-1     Removed
```

![bg right:30%](images/30-rogers_place.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
Options in the "docker-compose.yml" file
can be utilized to configure secrets,
health/ready checks, networking,
restart behavior, etc.  

[Reading The Fine Manual](https://docs.docker.com/compose/)
is highly recommended.  

For more complex orchestration needs,
[Kubernetes](https://kubernetes.io/) is a popular alternative.

![bg right:30%](images/30-rogers_place.jpg)
