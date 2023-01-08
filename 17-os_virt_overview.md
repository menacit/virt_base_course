---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: OS-level virtualisation overview"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Overview of OS-level virtualisation technologies and their uses"
keywords:
  - "virtualisation"
  - "os"
  - "vm"
  - "introduction"
  - "overview"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Wendelin Jacober (CC0 1.0)" -->
# OS-level virtualisation
### What makes it different and desirable?

![bg right:30%](images/17-cyberpunk_mirrors.jpg)

<!--
- Up until this point, we've mostly talked about things from a HW-level virtualisation perspective

Segue: May be time to refresh the differences between HW-level and OS-level
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Dennis van Zuijlekom (CC BY-SA 2.0)" -->
## HW-level virtualisation
Pretend to be hardware well enough to make operating systems run.

## OS-level virtualisation
Pretend to be an operating system environment well enough to run applications.

![bg right:30%](images/17-lock_pin.jpg)

<!--
- In general, developers and companies don't care much if the OS believes it's running on HW,
they just want to run their application stacks

- The goal of OS-level virtualisation is to convince users and applications, not OSes

- OS-level instances are often called "containers", I try to not use the term as it is a bit
confusing and could mean mean other things (more about that later)

Segue: To further complicate things, we can create sub-groups of OS-level virt...
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Pelle Sten (CC BY 2.0)" -->
Pretend to be another OS  
_or_  
Create an isolated environment

![bg right:30%](images/17-galley_carts.jpg)

<!--
- Basically what the slide says
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Pelle Sten (CC BY 2.0)" -->
FreeBSD's Linuxulator and Windows' WSL v1 allows execution of (many) Linux applications. 
  
[Wine](https://www.winehq.org/) allows (many) Windows programs to run on Linux, \*BSD and Mac OS.

![bg right:30%](images/17-silo.jpg)

<!--
- Syscalls are translated from Linux to FreeBSD or Windows syscalls

- Some other parts of the system are also emulated to create the illusion of running on Linux

- Linux on x86_64 has over 300 different syscalls that have many different options. It's quite hard
to fully emulate this and implement the same quirky behavior as on Linux

- FreeBSD is stuck on an old version of Linux and WSL v2 changed to running HW-level virtualised
Linux kernels instead

- Wine has gotten a lot better during the last couple of years since Valve (developers of Steam and
games like Counter-Strike) got involved to make software run on Steam deck
(https://www.steamdeck.com)

- Far from problem free, but can be very useful
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Pelle Sten (CC BY 2.0)" -->
Pretend to be another OS  
_or_  
**Create an isolated environment**

![bg right:30%](images/17-galley_carts.jpg)

<!--
- Our main focus will be virtualising the same OS as the host, this is by far most common
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Rolf Dietrich Brecher (CC BY 2.0)" -->
**Why use OS-level virtualisation?**

![bg right:30%](images/17-insect.jpg)

<!--
- What motivates us to use OS-level instead of HW-level? We already got a solution

Segue: Well, there are several benefits...
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Freed eXplorer (CC BY 2.0)" -->
Shared kernel saves memory and CPU cycles:
- No HW emulation overhead
- Concurrent usage of accelerators like GPUs
- More efficient scheduling of processes

**Cheaper, faster and more Greta-friendly.**

![bg right:30%](images/17-tunnel.jpg)

<!--
- As we don't need to pretend to be hardware, we can get rid of emulation layers that cause a lot
of overhead. Applications can get more or less direct access (while restrict) access to actual HW

- When running HW-level virt, each guest runs it's own OS kernel. This requires RAM and
processor capacity. 

- The same kernel is used by the host and all guests, shaving of the overhead

- This also enables concurrent sharing of HW devices that could otherwise only be used by one
HW-level guest at a time

- Efficiently sharing resources among HW-level VMs is hard, as the hypervisor has fairly limited
knowledge what goes on inside each guest. Are they using RAM because they need to or because of
caching? Are the processes using CPU batch jobs that could be give less priority?

- For the hypervisor, OS-level virtualisation is a bit like a one-way mirror: it can see everything
going on in the guests but not the other way around

- This allows the hypervisor to treat all programs running in guests as regular processes and
efficiently schedule them

- All in all, these shared kernel benefits allows much higher density of guests

Segue: The one-way mirrorness has other benefits as well...
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © NASA/Chris Gunn (CC BY 2.0)" -->
The one-way mirror allows a hypervisor to continuously monitor guests for malicious activity.  
  
[Falco](https://falco.org) is a kool example.

![bg right:30%](images/17-james_webb.jpg)

<!--
- While it's true that HW-level hypervisors can typically snoop on guests (as we've discussed),
in-practice it is a bit cumbersome and involves quite a bit of overhead

- As the host has great insight into what is happening in OS-level guests, activity can be
observed

- Falco is an Intrusion Detection System (IDS) for OS-level virtualisation on Linux (specifically
containers, we'll talk more about that later). You can configure it to alert you when specific
applications are run and abnormal behavior occurs: Should your web server really spawn a port
scanner process?

Segue: Enough about the benefits, what are our options?
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Pelle Sten (CC BY 2.0)" -->
## Virtuozzo
- First commercially available solution for Linux
- FOSSed in 2005 as ["OpenVZ"](https://openvz.org/)
- Popular in the low-end hosting space

## LXC
- Designed to [fit into mainline Linux](https://en.wikipedia.org/wiki/Linux_kernel#Mainline_Linux)
- Development currently lead by Canonical
- Used by ChromeOS to run regular Linux apps

![bg right:30%](images/17-spheres.jpg)

<!--
- We've already talked a bit about FreeBSD jails (see "Types of virtualisation" presentation)

- Limit ourselves to Linux, no really wide-spread solutions for Windows

- Virtuozzo is often shorted to just VZ

- Very early solution that showed great potential

- Required use of proprietary software with license fees and a heavily patched Linux kernel,
which mayhaps prevented it from being more widely used

- The core was open-sourced as "OpenVZ", still quite tightly tied to the SWsoft company

- Still quite popular today, especially in web hosting and for cheap VPSes as it allows great
density of guests on a single node

- A bit quirky behavior sometimes, applications didn't always behave as expected. Full HW-level
virtualisation probably seemed easier for many users (as they were used to one OS on a physical
server)

- As stated, one of the things preventing wide-spread adoption was that the development and
community was heavily controlled by SWSoft. You had to use a kernel with their patches, which was
somewhat limiting

- LXC was initially developed by IBM and other parties with the goal of only using (or at least
directly upstreaming) functionality in the Linux kernel (more about that later)

- Canonical are the makers of Ubuntu and it's where its most tightly integrated
-->
