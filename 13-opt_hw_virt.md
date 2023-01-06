---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: HW-level optimization"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "How hardware and software features can be used to accelerate VMs"
keywords:
  - "virtualisation"
  - "vm"
  - "acceleration"
  - "accel"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Chris Dlugosz (CC BY 2.0)" -->
# Optimizing virtualisation
### Making HW-level VMs go wroooom!

![bg right:30%](images/13-abstract_laser.jpg)

<!--
- We've talked about the many benefits provided by virtualisation

- Performance is not one of them

- There are ways however to make the overhead of HW-level VMs smaller
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Thierry Ehrmann (CC BY 2.0)" -->
## CPU assisted virtualisation
Allow guests to access parts of CPU, RAM and PCI bus without going through virtualiser.  
  
May require use of feature masking for migration and security.

![bg right:30%](images/13-wheel.jpg)

<!--
- One of the largest gains is to move things to HW (seems a bit counter intuitive)

- Emulating a CPU in SW is complex and usually quite slow

- Supported by most CPUs these days, features allowing direct access to PCI devices (such as GPUs)
may only be accessible on workstation and server systems

- KVM utilise and expose these hardware acceleration features
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Micah Elizabeth Scott (CC BY-SA 2.0)" -->
## Para-virtualisation
Let's not pretend that guests are running on real hardware.
  
Virtual devices don't necessarily need to act like physical HW and can be much more efficient.  
  
Virtio offers standardised virtual devices such as NICs, block devices, sockets and sound cards.

![bg right:30%](images/13-solder_pcb.jpg)

<!--
- Back in the days when virtualisation was new, hypervisors emulated commonly supported devices
such as NICs and SATA HDDs

- These days almost all servers are run virtualised and it seems a bit silly to pretend they are HW

- Para-virtualisation is about stopping the pretending while still benefiting from virtualisation

- Virtio devices are supported out-of-the-box by most modern operating systems running as guests

- Usage of these can drastically improve performance/lower load on the hypervisor
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Freestocks.org (CC0 1.0)" -->
## Memory and data optimization
Deduplication may be used for both guest memory/RAM and disk to save a lot of space.  
  
Memory ballooning features enables overprovisioning of RAM in guests.

![bg right:30%](images/13-cow.jpg)

<!--
- Deduplication == Only store one piece of data ones, for memory/RAM pages and for disks blocks

- If a hypervisor is running 100s of Windows VMs, chances are that a lot of storage space can be
saved if duplicated files can be deduplicated 

- Same goes for RAM, many VMs will likely run the same Linux distro and store the same kernel in
memory

- Deduplication can be costly from a performance perspective, but sometimes that is overweighted by
the potentially huge savings

- "Offline/Post-process" deduplication is often way cheaper from a performance perspective than
"online/in-line" (https://en.wikipedia.org/wiki/Data_deduplication#Classification)

- Memory ballooning allows the host to signal to guests that they can use more memory/should clean
up their caches to save memory during runtime. This enables hypervisor operators to overprovision
memory slightly more and make each hypervisor more cost effective 
-->
