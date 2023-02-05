---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-FileCopyrightText: © 2022 semeiths
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Prerequisites"
author: "Joel Rangsmo <joel@menacit.se> and semeiths"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Required software and configuration for virtualisation course"
keywords:
  - "virtualisation"
  - "prerequisites"
  - "prereqs"
  - "requirements"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Gytis B (CC BY-SA 2.0)" -->
# Course prerequisites
### What you need to know and setup

![bg right:30%](images/02-vechicle_graveyard.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Thierry Ehrmann (CC BY 2.0)" -->
## You need to know...
Basic networking and shell usage of Linux.

![bg right:30%](images/02-man_thinking.jpg)

<!--
- Participants need to know basic ethernet and IP networking to understand some concepts and labs.

- Being somewhat comfortable in the Linux shell is a requirement. Some of the things we'll cover
can't be done through a GUI.

- When covering OS virtualisation we'll also dig a bit deep down into Linux internals. You don't
need to be an expert but knowing what kernel space and user space is will surely help.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kristina Hoeppner (CC BY-SA 2.0)" -->
## You need to setup...
- [HashiCorp Vagrant](https://developer.hashicorp.com/vagrant/downloads) on your host machine
- Virtual machine with [Ubuntu Server 22.04](https://ubuntu.com/download/server)
- [Docker Engine](https://docs.docker.com/engine/install/ubuntu/) installed **in the Ubuntu VM**
  
**Ask for help if anything is unclear!**

![bg right:30%](images/02-llama.jpg)

<!--
- We'll need some software and a lab environments for the course

- Ubuntu will be used in most demos and labs.

- For now, just make sure that the software is installed and seem to be working.

- Check out the presentation links: I will however not provide a step-by-step guide, you won't get
it in real life.
-->
