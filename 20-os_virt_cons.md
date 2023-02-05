---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: OS-level virtualisation cons"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Downsides of using OS-level virtualisation compared to HW-level"
keywords:
  - "virtualisation"
  - "vm"
  - "container"
  - "security"
  - "performance"
  - "economics"
  - "cons"
  - "negative"
  - "downsides"
  - "cost"
  - "infosec"
  - "secops"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pedro Ribeiro Simões (CC BY 2.0)" -->
# OS-level virtualisation
### The downsides compared to hardware-level virtualisation 

![bg right:30%](images/20-street_art.jpg)

<!--
- Important to be aware of when OS-level virtualisation may be a bad choice

- We've touched on it a bit and some of you may be able to guess: please do!
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Thierry Ehrmann (CC BY 2.0)" -->
## Reliability
Live migration is wonky.  

Kernel version may different from what is expected by the guest.  
  
Linux can behave... interestingly... when many different tasks are running.  
  
Bugs triggered by guests could crash the host.

![bg right:30%](images/20-rusty_hut.jpg)

<!--
- Live migration is a feature that, in some environments, is heavily used to minimize disruptions.
While this in-theory works and even sometimes in practice, it's hard to depend on it

- Offline migration can still be used, but may not be good enough

- It's nice that we can run different flavors and versions of distros, but a ten year old Ubuntu
version may behave slightly different from a modern Fedora kernel

- The kernel is shared among the host and all guests. It quickly becomes a lot of different
processes and not all resources (like inotify watches) are properly name-spaced. Cgroups doesn't
regulate everything. This is usually less of a problem with HW-level VMs, as the host kernel is
doing far less different things

- A bug in an obscure syscall could crash the kernel. As the kernel is shared, it would affect
every guest and host
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
## Security
Gaps between the different isolation features.  

Host expose a huge attack surface to the guests.  
  
Compatibility has been priority, not security.

![bg right:30%](images/20-gnome.jpg)

<!--
- As OS-level virt was not coherently developed for Linux, there are gaps between the different
isolation technologies such NSes and LSM (https://en.wikipedia.org/wiki/Linux_Security_Modules)

- All the syscalls pose a huge attack surface. Quite complex compared to what a HW-level hypervisor
needs to do

- Syscalls and capabilities that are known to be dangerous (break isolation) are black-/deny-listed

- A far better approach when it comes to security would be to white-/allow-list known safe ones

- This probably break a lot of apps and make OS-level virt harder to adapt
-->
