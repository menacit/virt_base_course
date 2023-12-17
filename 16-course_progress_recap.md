---
SPDX-FileCopyrightText: © 2023 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Course progress recap"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Recap of introductory part of virtualisation course"
keywords:
  - "virtualisation"
  - "vm"
  - "container"
  - "recap"
  - "introduction"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
# Course progress recap
### Refreshing what we've learned so far

![bg right:30%](images/16-ram_tree.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kuhnmi (CC BY 2.0)" -->
Covered what virtualisation is and it's benefits.  
  
Talked about HW-level virtualisation and it's pros/cons.

![bg right:30%](images/16-hummingbird.jpg)

<!--
- As we learned, virtualisation has many benefits related to security, economics, reliability and
environmental aspects

- HW-level virtualisation == Emulation of a computer with the goal of making an operating system
run on it like it would on real HW

- Has anyone tested Proxmox, Qubes or related?
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jon Evans (CC BY 2.0)" -->
- ~~High-level concepts and pros/cons~~
- ~~Hardware-level virtualisation~~
- OS-level virtualisation
- Virtualised development and containers
- Labs
- Course recap and summary

![bg right:30%](images/16-jellyfish.jpg)

<!--
- Basically course progress status
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pelle Sten (CC BY 2.0)" -->
Things are about to get more complex.  
  
**Remember to ask questions and utilize available learning resources!**

![bg right:30%](images/16-rusty_silos.jpg)

<!--
- Some of the following topics will be more complex and technical

- Remind students that they need to spend time studying outside of lessons

- Ask for help and clarifications

- Remind students that they can help make things better by clarifying things for future students,
no stupid questions exist!
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% John K. Thorne (CC0 1.0)" -->
### Q&A, reflections and feedback

![bg right:30%](images/16-dome_collage.jpg)

<!--
- Throughout the course, students have been asked to submit their reflections after each segment

- Several things were brought up that seems to have left impressions, many found Qubes kool and
were surprised to find some many benefits of virtualisation

- Several students requested a glossary

- Questions and other feedback came up that I would like to take some time to address before we
continue progressing into OS-level virtualisation
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pelle Sten (CC BY 2.0)" -->
**In most use-cases, the security pros far outweigh the cons.**

![bg right:30%](images/16-locks.jpg)

<!--
- We've talked a lot about the security aspects related to virtualisation, both good and bad

- One of the exercises included argumentation against virt from a security perspective

- Why many of these arguments are true, for most use-cases the pros far outweigh the cons

- Talk a bit about the pros

- Hypervisors are usually configured in large cluster setups with a single control plane (like
vCenter for VMware), which involves some risks. While this is usually cost effective, you can run
hypervisors more or less independently to mitigate the risks. It's not an inherit problem with virt

- Performance and complexity probably has the strongest argument against virtualisation
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% OLCF at ORNL (CC BY 2.0)" -->
"Pizza box" is slang for rack server.  
  
Physical servers requires time, money and energy to get/keep up and running.  
  
Most software vendors don't want to manage physical appliances.

![bg right:30%](images/16-server_rack.jpg)

<!--
- I've used the term "pizza boxes" several times, not all may know what it is

- Not everyone may have even seen a rack server (or a DC for that matter, is there interest?)

- The image shows the back-side of a rack with several of them stacked in it

Segue: Let's take a closer look
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Robert Jemimus (CC BY 2.0)" -->

![bg center:100%](images/16-exposed_server-1.jpg)

<!--
- Close-up of rack server/pizza box with lid off 
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Robert Jemimus (CC BY 2.0)" -->

![bg center:100%](images/16-exposed_server-2.jpg)

<!--
- Close-up of mounted and extended rack server with lid open
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% OLCF at ORNL (CC BY 2.0)" -->
"Pizza box" is slang for rack server.  
  
Physical servers requires time, money and energy to get/keep up and running.  
  
Most software vendors don't want to manage physical appliances.

![bg right:30%](images/16-server_rack.jpg)

<!--
- As we talked about, physical things break - debugging these issues and dealing with RMA is no fun

- Physical servers also makes it harder to move fast, as everything requires more planning, people
and effort

- Software vendors prefer to not trust customers to setup their complex stacks. Appliances solve
this problem as the vendor can deliver a more or less configured server to the customer. These used
to be physical servers, but these days they are mostly virtual appliances due to the effort
required in maintaining physical HW

- Revisit the presentations "Economic benefits" and "Reliability benefits" for more info

Segue: Another thing that was brought up in the "Reliability benefits" presentation was why three
is a magic number - that could use some clarification...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Andrew Hart (CC BY-SA 2.0)" -->
Qubes OS is neat, but requires decent hardware.  

\>10GB RAM, Intel VT-x/AMD-V
and Intel VT-d/AMD-Vi.  

Checkout the ["hardware compatibility list"](https://www.qubes-os.org/hcl/).  

![bg right:30%](images/16-seals.jpg)

<!--
- Students showed interest in Qubes OS, but don't know which HW to run it on
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Helsinki Hacklab (CC BY 2.0)" -->
Para-virtualised devices, such as network cards and disks, don't pretend to be physical things.  
  
By getting rid of the illusion, a lot of overhead is removed which make them faster.

![bg right:30%](images/16-umbrellas.jpg)

<!--
- In the beginning, hypervisors wanted to be able to run the OSes everyone was using

- To make things smooth, they emulated devices that were commonly supported/had drivers shipped
with the OSes

- These days almost all servers are virtualised and have been for quite some time

- Purpose built virtio drivers are included in most modern OSes that talk to a virtual device that
doesn't pretend to be physical (abide by the laws of nature and act in ways that are fast in HW but
slow in SW)

- This removes unnecessary emulation overhead, which results in lower load on hypervisors that can
be translated into heigher VM density and thereby economic benefits.

Segue: On the topic of performance, there may be need to clarify some terms commonly used...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pedro Ribeiro Simões (CC BY 2.0)" -->
Vertical scaling == Add/Remove CPU, RAM, etc.  
  
Horizontal scaling == Add/Remove VM instances.

![bg right:30%](images/16-sculpture.jpg)

<!--
- Upscaling: Making systems powerful/able to handle more load

- Downscaling: Making systems less powerful/able to handle less load, but saves money

- Vertical upscaling is done by adding more CPU cores or what ever resource is necessary to a VM.
Some hypervisors and OSes supports doing this while the guest is running, other require a reboot

- Horizontal upscaling means deploying more VMs running the same application and using a load
balancer or similar to spread user traffic against the servers

- Vertical upscaling only takes you so far, eventually you'll outgrow the physical server. Not all
OSes and apps handle super big instances very well

- Horizontal scaling may be a better choice and adds redundancy, but adds additional complexity
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jeena Paradies (CC BY 2.0)" -->
If you got some spare hardware,
why not try setting up
[Proxmox VE](https://www.proxmox.com/en/proxmox-virtual-environment/)
or [XCP-NG](https://xcp-ng.org/)?  

Play around with advanced features,
such as live migration and
PCI forwarding.

![bg right:30%](images/16-stones.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Tero Karppinen (CC BY 2.0)" -->
**Questions/thoughts before we keep going?**

![bg right:30%](images/16-pixel_forest.jpg)
