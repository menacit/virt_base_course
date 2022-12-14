---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
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
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Milan Bhatt (CC BY-SA 2.0)" -->
# Docker demonstration
### The whale that changed everything

![bg right:30%](images/24-whale.jpg)

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Thierry Ehrmann (CC BY 2.0)" -->
```
$ sudo docker run -ti ubuntu:18.04 /bin/bash

Unable to find image 'ubuntu:18.04' locally
18.04: Pulling from library/ubuntu
a055bf07b5b0: Pull complete 

root@79424287b988:/#
```

![bg right:30%](images/24-server_rack.jpg)

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Jan Hrdina (CC BY-SA 2.0)" -->
```dockerfile
FROM python:3.11.0

RUN pip install Flask==2.2.2
COPY app.py .

USER 10000
CMD ["flask", "run", "--host", "0.0.0.0"]
```

![bg right:30%](images/24-containers.jpg)

---
```
$ sudo docker build -t kool_app:0.2 .
Sending build context to Docker daemon  4.608kB

Step 1/5 : FROM python:3.11.0
Step 2/5 : RUN pip install Flask==2.2.2
Step 3/5 : COPY app.py .
Step 4/5 : USER 10000
Step 5/5 : CMD ["flask", "run", "--host", "0.0.0.0"]
Successfully tagged kool_app:0.2
```

```
$ sudo docker run kool_app:0.2

* Debug mode: off
* Running on all addresses (0.0.0.0)
```

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Yves Sorge (CC BY-SA 2.0)" -->
```yml
services:
  db:
    image: postgres:14
    volumes:
      - ./data/db:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=G0d!

  web:
    image: my_awesome_app:v9
    ports:
      - "8000:8000"
    environment:
      - DB_URL=pgsql://db
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=G0d!
    depends_on:
      - db
```

![bg right:30%](images/24-neon_forest.jpg)

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Freed eXplorer (CC BY 2.0)" -->
## Further awesomeness 
Tons of pre-built images on [Docker hub](https://hub.docker.com/).  
  
Supports both OS-level and (with some effort) HW-level virtualisation.  
   
[Read The Fine Manual!](https://docs.docker.com/engine/)

![bg right:30%](images/24-tunnel.jpg)
