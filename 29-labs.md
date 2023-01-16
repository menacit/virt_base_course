---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Labs"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Labs covering areas discussed during virtualisation course"
keywords:
  - "virtualisation"
  - "vm"
  - "container"
  - "labs"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Fritzchens Fritz (CC0 1.0)" -->
# Virtualisation labs
### Putting knowledge to practice

![bg right:30%](images/29-chip.jpg)

<!--
- So far, we've been going through a lot of theory

- Course exercises have been focused on the high level pros/cons of virtualisation

- We're about to put that knowledge to the test
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Mario Hoppmann (CC BY 2.0)" -->
**Lab descriptions tells you what to do, not how you should do it.**  
  
**Your submissions should document how you solved the problem.**

![bg right:30%](images/29-polar_bear.jpg)

<!--
- Labs will be based on different scenarios you may encounter in real life

- Just like in real life, no one will tell you exactly how to do it. Then the job should be
replaced by a shell script

- No one knows every on-top of their head, feel free to Google, discuss with class mates, look
through old slides and ask for support

- Let me know how you approached the challenge and why you chose the solution steps you did

- There are three labs. They each have a mandatory step that everyone should do

- They have option harder steps with I highly recommend tackling for higher grades. Recommend that
you focus on completing the first step of the three exercises first.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Dennis van Zuijlekom (CC BY-SA 2.0)" -->
## Lab: Shared dev environment
Example Inc. wants their programmers to use the same software for web development.
Vagrant has been chosen to tackle this challenge.  
  
★ Create a Vagrantfile that sets up Neovim, Python and a web server in a Debian 11 VM  
  
★★ Store/share the Vagrantfile together with a HTML document using Git
  
**[virt_course+012901@%EMAIL_DOMAIN%](mailto:virt_course+012901@%EMAIL_DOMAIN%)**

![bg right:30%](images/29-lego.jpg)

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © William Murphy (CC BY-SA 2.0)" -->
## Lab: Network benchmark
Department of Examples need to cut cots in IT.
You've been tasked with investigating if para-virtualisation could help.  
  
★ Run network benchmarks between two guests to determine benefits of using Virtio NICs  
  
★★ Produce a presentation with results targeted towards a non-technical management team
   
**[virt_course+012902@%EMAIL_DOMAIN%](mailto:virt_course+012902@%EMAIL_DOMAIN%)**

![bg right:30%](images/29-street_art.jpg)

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Steven Kay (CC BY-SA 2.0)" -->
## Lab: Containerise Gitea
Examplify wants to make money by hosting [Gitea](https://gitea.io) servers for development teams.  
  
★ Package and run Gitea in a Docker container  
  
★★ Deploy Gitea backed by a MySQL database with Docker Compose  
  
★★★ Compile and run Gitea from source using a multi-stage Docker build
   
**[virt_course+012903@%EMAIL_DOMAIN%](mailto:virt_course+012903@%EMAIL_DOMAIN%)**

![bg right:30%](images/29-pixel_map.jpg)
