---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Prerequisites"
author: "Joel Rangsmo <joel@menacit.se>"
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
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Gytis B (CC BY-SA 2.0)" -->
# Course prerequisites
### What you need to know and setup

![bg right:30%](images/02-vechicle_graveyard.jpg)

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Thierry Ehrmann (CC BY 2.0)" -->
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
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Kristina Hoeppner (CC BY-SA 2.0)" -->
## You need to setup...
- [HashiCorp Vagrant](https://developer.hashicorp.com/vagrant/downloads) On your Host machine
- Virtual machine with [Ubuntu Server 22.04](https://ubuntu.com/download/server)
- [Docker Engine](https://docs.docker.com/engine/install/ubuntu/) installed **in Ubuntu Server VM**

## What you may experiment with...
Try enabling/configuring nested virtualisation and check if it works **in Ubuntu Server VM**:

```
$ sudo apt install cpu-checker && kvm-ok
```

![bg right:30%](images/02-llama.jpg)

<!--
- We'll need some software and a lab environments for the course

- Ubuntu will be used in most demos and labs.

- For now, just make sure that the software is installed and seem to be working.

- Nested virtualisation allows us to run hardware accelerated virtualisation inside a HW-level VM,
which could be very useful for experimentation.

- It does however put requirements on HW and SW configuration. Urge participants to try enabling
it: if it works well for the majority we'll try to incorporate use of it in labs.

- Check out the presentation links: I will however not provide a step-by-step guide, you won't get
it in real life.
-->
