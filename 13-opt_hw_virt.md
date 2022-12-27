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
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Thierry Ehrmann (CC BY 2.0)" -->
## CPU assisted virtualisation
Allow guests to access parts of CPU, RAM and PCI bus without going through virtualiser.  
  
May require use of feature masking for migration and security.

![bg right:30%](images/13-wheel.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Micah Elizabeth Scott (CC BY-SA 2.0)" -->
## Para-virtualisation
Let's not pretend that guests are running on real hardware.
  
Virtual devices don't necessarily need to act like physical HW and can be much more efficient.  
  
Virtio offers standardised virtual devices such as NICs, block devices, sockets and sound cards.

![bg right:30%](images/13-solder_pcb.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Freestocks.org (CC0 1.0)" -->
## Memory and data optimization
Deduplication may be used for both guest memory/RAM and disk to save a lot of space.  
  
Memory ballooning features enables overprovisioning of RAM in guests.

![bg right:30%](images/13-cow.jpg)

<!--
TODO
-->
