---
SPDX-FileCopyrightText: © 2023 Menacit AB <foss@menacit.se>
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
<!-- _footer: "%ATTRIBUTION_PREFIX% ETC Project (CC0 1.0)" -->
# Virtualisation software
### Examples of HW-level solutions

![bg right:30%](images/10-computer_man.jpg)

<!--
- So far everything we've covered applies more or less to both HW-level and OS-level virtualisation

- We've been quite soft and general, this section will be more technical

- Remind students to ask questions if things are unclear
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Martin Fisch (CC BY 2.0)" -->
## VMware
- ESXI is directly installed on HW
- Great functionality for clustering
- Expensive and proprietary, but batteries are safely included

![bg right:30%](images/10-bees.jpg)

<!--
- ESXI is installed on HW just like you would a Linux distribution

- Hypervisor cluster is controlled by vCenter

- Live migration, vSwitch and vSAN makes setting up highly availble hypervisor clusters easy

- Decent choice for SMBs with limited IT staff and high availability requirements

- "No one ever got fired for buying VMware"
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Daniel Oliva Barbero (CC BY 2.0)" -->
## Hyper-V
- Window's native virtualisation technology
- Does what you expect these days
- Powers WSL version 2
- Foundation of impressive "VBS" functionality
- Somewhat messy licensing

![bg right:30%](images/10-vapor_windows.jpg)

<!--
- Built in to Windows

- VM manager (similar to Virtualbox) can be activated as a Windows feature

- Requires Windows 10 Pro/Enterprise or Windows 11 Pro. Included in Windows Server, but you often
need to pay per VMs and/or CPU cores. It's boring.

- Was quite late to enter the game and even later to become a competitive option, but works alright
for both Windows and Linux guests these days

- WSL == Windows Subsystem For Linux, ability to run Linux distros in highly integrated VMs

- Clarify that this applies to WSL version 2, not WSL version 1 which is OS-level virtualisation

- VBS == Virtualisation Based Security, examples are Cred Guard, Drive Guard and old Edge sandbox

- VBS uses security properties provided by virtualisation and related HW features without running
traditional OSes in VMs
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Fandrey (CC BY 2.0)" -->
## Bhyve
- HW-level virtualisation for FreeBSD
- Ported to macOS and Illumos
- Designed to explicitly not support legacy operating systems

![bg right:30%](images/10-beastie.jpg)

<!--
- Mostly anecdotal, bring this up as we've previously talked about jails

- FreeBSD is not so widely used these days, but probably lots of users on the Mac port as it is/was
used for Docker on Mac OS

- By not supporting legacy OSes, less code/complexity is required.

- Less code == less risk for bugs and easier to audit/maintain/change
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Maja Dumat (CC BY 2.0)" -->
## "KVM"
What people really mean is
**libvirt + QEMU + KVM**.  
  
Most used virtualisation stack on Linux and the base for offerings from Red Hat and Canonical.

![bg right:30%](images/10-tunnel.jpg)

<!--
- People use the term KVM incorrectly

- Several different software components make up what people refer to

- For a long while this was the most common solution for virtualisation on Linux servers

- Red Hat makes RHEL (which Centos/Alma Linux/Rocky Linux is based on) and sponsors Fedora

- Canonical makes Ubuntu

Segue: Let's break these components down and see what purpose they serve
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pedro Ribeiro Simões (CC BY 2.0)" -->
## libvirt
- Abstraction layer for running/managing VMs
- Supports several different hypervisors
- Does the dirty work of setting up networking, storage, snapshots etc.
- Mess of Python and XML files

![bg right:30%](images/10-cables.jpg)

<!--
- If you have used virt-manager or virsh, you've used libvirt

- Most often a client (such as virsh) talks to libvirtd running as a system service

- Handles a lot of the Grunt work, configures routing/NAT rules etc.

- The project shows it's age
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Martin Fisch (CC BY 2.0)" -->
## QEMU
- Swiss army knife of emulation
- Emulates BIOS/UEFI and devices
- Security was not the highest priority

![bg right:30%](images/10-mountains.jpg)

<!--
- QEMU is very flexible, it can emulate obscure CPU architectures and ancient floppy devices

- Most OSes expect a BIOS, hardware devices, etc: QEMU emulates several kinds of these depending
on the OS's needs.

- QEMU's primary goal (at least initially) was to be a somewhat fast and very flexible solution
for emulation. These days, it's primarily used to run server VMs in data centers which is quite
far from this initial goal.

- It's a bit like the "Good/Cheap/Fast"-rule, you need lots of code to implement all these
features and options - lots of code means high risk for bugs, worst case security vulnerabilities

- A great example is the "Venom" VM escape vuln (https://en.wikipedia.org/wiki/VENOM), which
affected code used to emulate a floppy device which was enabled in most (every?) guest. Most users
in the current century probably never needed this feature, but it still was available.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Aka Tman (CC BY 2.0)" -->
## KVM
- Feature of the Linux kernel
- Used to run performance critical operations in kernel space and access HW acceleration features
- Not only utilized by QEMU!

![bg right:30%](images/10-mosaic.jpg)

<!--
- What makes QEMU become fast and usable, fully emulating a CPU and RAM is very slow

- Not only used by QEMU, as we are about to see

Segue: Before we get into other users of KVM, there is a project that only use two of the
components (not libvirt)
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Masahiko Ohkubo (CC BY 2.0)" -->
## Proxmox VE
- All-in-one solution deployed on HW
- Managed through web UI or API
- Uses QEMU + KVM and LXC
- Built-in ZFS support

![bg right:30%](images/10-ascii_x.jpg)

<!--
- Makes use of QEMU and KVM, but not libvirt as it is a bit of a mess

- Basically same installation procedure as for ESXI

- Supports automation through API: Terraform and Ansible can use this

- Besides HW-level VMs it can run lightweight OS-level using LXC, more about that later

- Includes out-of-the-box support for ZFS, which provides great software RAID, snapshots and
data corruption detection among other things

- Supports many of the same clustering features as VMware ESXI, but not nearly as polished

- Great for a similar usecases as ESXI, also for home labs - it's FOSS!
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Edd Thomas (CC BY 2.0)" -->
## Cloud Hypervisor
- Lousy name!
- Modern replacement for QEMU
- Designed for multi-tenant server hosting
- [Lots of financial backing](https://www.cloudhypervisor.org/#Get%20Involved)

![bg right:30%](images/10-nixie_tube.jpg)

<!--
- Initially developed by Intel, but know governed by the Linux Foundation

- Main focus is not to run everything like QEMU, but run modern server OSes

- Supports Linux and since somewhat recently the latest Windows Server

- Priorities are security and performance, not flexibility

- Development is sponsored by several (and in some cases competing companies), such as Intel, ARM,
AMD, Microsoft, ByteDance (developers of Tiktok) and Alibaba (probably largest non-US cloud)

- Uses KVM on Linux to make things fast!

- Will likely be a reasonable replacement for libvirt + QEMU for most users soon

Segue: Another user of KVM is Firecracker
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Martin Fisch (CC BY 2.0)" -->
## Firecracker
- [Developed by AWS](https://firecracker-microvm.github.io/#faq)
- Runs performant "microVMs"
- Not designed for general purpose hosting
- Shares code with Cloud Hypervisor

![bg right:30%](images/10-fire.jpg)

<!--
- Firecracker isn't built to run general purpose server operating systems/workloads

- Initially developed for Amazon's FaaS Lambda

- Wanted the speed and low overhead of OS-level virtualisation but security of HW-level

- Both Firecracker and Cloud Hypervisor are written in Rust, which is a language that help
developers make safer and more performant applications. A lot of the low-level code in these
projects share code, resulting in that they make each other better
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Lars Juhl Jensen (CC BY 2.0)" -->
## Xen
- Pioneering solution for para-virtualisation
- Performant "bare metal" hypervisor
- Relatively small [TCB](https://en.wikipedia.org/wiki/Trusted_computing_base)

![bg right:30%](images/10-panda.jpg)

<!--
- Originally a research project, released as FOSS in 2003
- High performance with focus on para-virtualisation (more about that later in the course)
- Served as the base for AWS instances (now days they seem to use KVM more and more)

Segue: Xen has an interesting design and is quite different from QEMU + KVM....
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Scsami (CC0 1.0)" -->
![bg center:100%](images/10-hypervisor_types.jpg)

<!--
- https://en.wikipedia.org/wiki/Hypervisor#Classification

- https://wiki.xenproject.org/wiki/Xen_Project_Beginners_Guide

- TODO: Add better speaker notes for this somewhat complicated topic
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Lars Juhl Jensen (CC BY 2.0)" -->
## Xen
- Pioneering solution for para-virtualisation
- Performant "bare metal" hypervisor
- Relatively small [TCB](https://en.wikipedia.org/wiki/Trusted_computing_base)

![bg right:30%](images/10-panda.jpg)

<!--
- TCB == Trusted Computing Base, HW and SW that if compromised could affect the overall security
of a system. Kernel level software, such as drivers, and components with firmware often have more
or less unrestricted access to memory, so a compromise of them could allow an attacker to gain
full control of all software running on the machine

- Having a small TCB is desirable as less code is easier to test and audit for security issues

- As Xen acts as a thin layer and lots of functionality normally associated with a virtual machine
manager is delegated to dom0 (the privileged VM used to manage the system and other VMs), Xen has
a relatively small TCB

- If you wanna try it out, the easiest way is probably to install XCP-NG (https://xcp-ng.org/)

Segue: Due to these properties, Xen was chosen as the virtualisation technology for Qubes OS...
-->
