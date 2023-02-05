---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Lab recap"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Recap of virtualisation course labs"
keywords:
  - "virtualisation"
  - "vm"
  - "container"
  - "labs"
  - "recap"
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
# Virtualisation labs recap
### Review of practical lab exercises

![bg right:30%](images/30-space_walk.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Martin Fisch (CC BY 2.0)" -->
## What's in your toolbox?
- Base knowledge and Google-fu
- Slides and other course material
- Questions and clarification requests

![bg right:30%](images/30-squirell.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jorge Franganillo (CC BY 2.0)" -->
## Lets break them down

![bg right:30%](images/30-bumper_cars.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
## Lab: Shared dev environment
Example Inc. wants their programmers to use the same software for web development.
Vagrant has been chosen to tackle this challenge.  
  
★ Create a Vagrantfile that sets up Neovim, Python and a web server in a Debian 11 VM  
  
★★ Store/share the Vagrantfile together with a HTML document using Git

![bg right:30%](images/30-lego.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
_"Example Inc. wants their programmers to use the same software for web development."_  
  
Collaborative development is not trivial.  
  
See presentation:  
"Introduction to virtual development".

![bg right:30%](images/30-lego.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
_"Vagrant has been chosen to tackle this challenge."_  
  
What is Vagrant? How does it relate to collaborative development?  
  
> Vagrant enables users to create and configure lightweight, reproducible, and
> portable development environments.

— Start page of [https://www.vagrantup.com/](https://www.vagrantup.com/).  
  
See presentation: "Vagrant demo".

![bg right:30%](images/30-lego.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
_"★ Create a Vagrantfile that sets up Neovim, Python and a web server in a Debian 11 VM"_  
  
What is a "Vagrantfile"? How does it relate to the collaborative development challenge?  
  
See presentation: "Vagrant demo".

![bg right:30%](images/30-lego.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
_"★★ Store/share the Vagrantfile together with a HTML document using Git"_  
  
What would be the purpose of tracking the Vagrantfile and a HTML document with Git?  
  
How does it relate to collaborative web development? What role could the HTML document serve?  
  
See presentation: "Vagrant demo".

![bg right:30%](images/30-lego.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
## Lab: Containerise Gitea
Examplify wants to make money by hosting [Gitea](https://gitea.io) servers for development teams.  
  
★ Package and run Gitea in a Docker container  
  
★★ Deploy Gitea backed by a MySQL database with Docker Compose  
  
★★★ Compile and run Gitea from source using a multi-stage Docker build

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
_"Examplify wants to make money by hosting Gitea servers for development teams."_  
  
What is Gitea? How could it help development teams and bring income to Examplify?  
  
> Gitea is a community managed lightweight code hosting solution written in Go.

— Start page of [https://gitea.io](https://gitea.io).  
  
What does this mean for Examplify?

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
_"★ Package and run Gitea in a Docker container"_  
  
What is Docker? How does it relate to the challenge?  
  
Throw "Package application Docker" query into search engine.  
  
Is there any reference documentation?  
  
See presentation: "Docker demo".

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
_"★★ Deploy Gitea backed by a MySQL database with Docker Compose"_  
  
What is MySQL? What is Docker Compose?  
  
Google "Gitea + MySQL".  
  
> You need a database to use Gitea. Gitea supports PostgreSQL, MySQL, SQLite, and MSSQL...

— [Database section of Gitea manual](https://docs.gitea.io/en-us/database-prep/)  
  
What role does Docker Compose play?  
  
See presentation: "Docker demo".

![bg right:30%](images/30-pixel_map.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Steven Kay (CC BY-SA 2.0)" -->
_"★★★ Compile and run Gitea from source using a multi-stage Docker build"_  
  
What does "source" mean in this context? Why would anyone compile software from source?  
  
Look up ["multi-stage build" in the docs](https://docs.docker.com/build/building/multi-stage/).  
  
What is the benefit of multi-stage builds in this context?

![bg right:30%](images/30-pixel_map.jpg)
