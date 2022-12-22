---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Options for HW-level virtualisation"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Examples of solutions for HW-level virtualisation on the market"
keywords:
  - "virtualisation"
  - "vm"
  - "vmware"
  - "esxi"
  - "kvm"
  - "QEMU"
  - "hyperv"
  - "firecracker"
  - "cloudhypervisor"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © ETC Project (CC0 1.0)" -->
# Virtualisation software
### Examples of HW-level solutions

![bg right:30%](images/10-computer_man.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Martin Fisch (CC BY 2.0)" -->
## VMware
- ESXI is directly installed on HW
- Great functionality for clustering
- Expensive and proprietary, but batteries are safely included

![bg right:30%](images/10-bees.jpg)

<!--
- vSan and vSwitch

- "No one ever got fired for buying VMware"
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Daniel Oliva Barbero (CC BY 2.0)" -->
## Hyper-V
- Window's native virtualisation technology
- Does what you expect these days
- Powers WSL version 2
- Foundation of impressive "VBS" functionality
- Somewhat messy licensing

![bg right:30%](images/10-vapor_windows.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Fandrey (CC BY 2.0)" -->
## Bhyve
- HW-level virtualisation for FreeBSD
- Ported to Mac OS
- Designed to explicitly not support legacy operating systems

![bg right:30%](images/10-beastie.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Maja Dumat (CC BY 2.0)" -->
## "KVM"
What people really mean is
**libvirt + QEMU + KVM**.  
  
Most used virtualisation stack on Linux and the base for offerings from Red Hat and Canonical.

![bg right:30%](images/10-tunnel.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Pedro Ribeiro Simões (CC BY 2.0)" -->
## libvirt
- Abstraction layer for running/managing VMs
- Supports several different hypervisors
- Does the dirty work of setting up networking, storage, snapshots etc.
- Mess of Python and XML files

![bg right:30%](images/10-cables.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Martin Fisch (CC BY 2.0)" -->
## QEMU
- Swiss army knife of emulation
- Emulates BIOS/UEFI and devices
- Security was not highest priority

![bg right:30%](images/10-mountains.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Aka Tman (CC BY 2.0)" -->
## KVM
- Feature of Linux kernel
- Used to access hardware acceleration features
- Not only used by QEMU!

![bg right:30%](images/10-mosaic.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Masahiko Ohkubo (CC BY 2.0)" -->
## Proxmox VE
- All-in-one solution deployed on HW
- Managed through web UI or API
- Uses QEMU + KVM and LXC
- Built-in ZFS support

![bg right:30%](images/10-ascii_x.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Edd Thomas (CC BY 2.0)" -->
## Cloud Hypervisor
- Lousy name!
- Modern replacement for QEMU
- Designed for multi-tenant server hosting
- Lots of backing

![bg right:30%](images/10-nixie_tube.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Martin Fisch (CC BY 2.0)" -->
## Firecracker
- Developed by AWS
- Runs performant "microVMs"
- Not designed for general purpose hosting
- Shares code with Cloud Hypervisor

![bg right:30%](images/10-fire.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Lars Juhl Jensen (CC BY 2.0)" -->
## Xen
- Pioneering solution for para-virtualisation
- Performant "bare metal" hypervisor
- Relatively small TCB

![bg right:30%](images/10-panda.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Scsami (CC0 1.0)" -->
![bg center:100%](images/10-hypervisor_types.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Lars Juhl Jensen (CC BY 2.0)" -->
## Xen
- Pioneering solution for para-virtualisation
- Performant "bare metal" hypervisor
- Relatively small TCB

![bg right:30%](images/10-panda.jpg)

<!--
TODO
-->
