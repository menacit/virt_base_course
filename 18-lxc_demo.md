---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: LXC/LXD demo"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Demonstration of LXC/LXD for OS-level virtualisation"
keywords:
  - "virtualisation"
  - "os"
  - "lxc"
  - "lxd"
  - "demo"
  - "demonstration"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Freed eXplorer (CC BY 2.0)" -->
# LXC/LXD demonstration
### A peak into OS-level virtualisation

![bg right:30%](images/18-rusty_factory.jpg)

<!--
- Let's look at how LXC can be used and what neat things it provides

- LXC == Container technology, LXD == service to manage it and other things (think libvirt)

- Far from a complete demo of the feature set and I don't expect you to remember the commands, more
of a tasting to see what it's capable of
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Jan Hrdina (CC BY-SA 2.0)" -->
```
$ sudo snap install lxd

lxd 5.9-9879096 from Canonical✓ installed
```

```
$ sudo lxd init --minimal
```

![bg right:30%](images/18-optics.jpg)

<!--
- Installation is trivial: If you're on Ubuntu, chances are that it's already installed

- As Canonical is lead, Ubuntu has the best integration. The upstream project recommends install
via snap (https://snapcraft.io/), but some other distros have native packages

- Once installed, the "lxd init" command allows you to enable lxd and customize settings, such as
cluster configuration. Passing the "--minimal" flag provides automated configuration without any
questions
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Dennis van Zuijlekom (CC BY-SA 2.0)" -->
```
$ sudo lxc image list images: | shuf

centos/8-Stream(3more)
openwrt/21.02(3more)
fedora/36(3more)
almalinux/9(3more)
opensuse/15.4/desktop-kde(1more)
mint/tina(3more)
alpine/3.17(3more)
[...]
```

![bg right:30%](images/18-usb_leds.jpg)

<!--
- Before we can create a OS-level VM (or "system container" as they are called in LXD lingo)

- The projects builds images for a large number of different Linux distros, you aren't just limited
to the one running on your host/hypervisor

- The example command shows a randomized sample of distros

- These are preconfigured, no need to go through an install wizard

Segue: Let's select one and get it started...
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Price Capsule (CC BY-SA 2.0)" -->
```
$ sudo lxc launch images:almalinux/9 srv-1

Creating srv-1
Retrieving image: Unpack: 100% (3.81GB/s)
Starting srv-1
```

![bg right:30%](images/18-desert_hut.jpg)

<!--
- In this example we'll create an instance based on the Alma Linux image (successor to Centos)

- Ofc there are many options that can be tweaked, but creating an OS-level container can be this
easy and (if the image has already been downloaded to the host before) deployed in a few seconds
-->

---
```
$ cat /etc/os-release | grep -F PRETTY_NAME
PRETTY_NAME="Ubuntu 22.04.1 LTS"

$ sudo lxc exec -t srv-1 -- /bin/bash

[root@srv-1 ~]# cat /etc/os-release | grep -F PRETTY_NAME
PRETTY_NAME="AlmaLinux 9.1 (Lime Lynx)"
```

<!--
- Once created, we can execute an interactive shell in the guest to start running commands

- The example output shows that the host is running Ubuntu 22.04, while our newly created guest is
a Alma Linux instance

Segue: This is neat quite neat and sure it was easy to get started, but previously density and low
overhead was raised as the main advantages...
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © NASA (CC BY 2.0)" -->
```
$ sudo lxc info srv-1 --resources

Name: srv-1
Status: RUNNING

Resources:
  Processes: 15
  Disk usage:
    root: 2.62MiB
  Memory usage:
    Memory (current): 54.58MiB
[...]
```

![bg right:30%](images/18-earth.jpg)

<!--
- The command shows a truncated version of the info command, which among other things show resource
usage of the instance

- Granted that we have not installed any particular software or service besides what is provided by
the container image, but it currently only consumes 2.6MiB of disk space and 55MiB of RAM

- The disk usage in this output does not include the Alma Linux image, but the kool thing is that
it will be shared by other instances using the same template

- In other words, the only per-instance storage requirements are changes or files we add after
initial deployment

- We'll talk more about this sorcery later in the course
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Martin Fisch (CC BY 2.0)" -->
```
$ sudo lxc exec -t srv-2 -- /bin/ash

~ # apk add fortune
(1/3) Installing libmd (1.0.4-r0)
(3/3) Installing fortune (0.1-r1)

~ # fortune 

Matter cannot be created or destroyed,
nor can it be returned without a receipt.
```

![bg right:30%](images/18-seal.jpg)

<!--
- We can do most thing's we expect out of a Linux server, such as install and run software

- "srv-2" is based on the "Alpine Linux" distributions, which is very minimal and popular in the
space
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © OLCF at ORNL (CC BY 2.0)" -->
```
$ sudo lxc snapshot srv-2 pre_upgrade
```

```
$ sudo lxc restore srv-2 pre_upgrade
```

![bg right:30%](images/18-server_macro.jpg)

<!--
- As with HW-level VMs, we can create snapshots on regular basis or before we do stupid things

- The can be disk-only or contain runtime state (memory, CPU registers, etc.)

Segue: As briefly mentioned, LXD has built-in clustering functionality which is quite easy to get
going (especially compared to other virtualisation solutions)
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Thierry Ehrmann (CC BY 2.0)" -->
```
$ sudo lxc cluster list

node-1
node-2
node-3
```

```
$ sudo lxc info srv-1 | grep Location

Location: node-1
```

```
$ sudo lxc cluster evacuate node-1
```

```
$ sudo lxc info srv-1 | grep Location

Location: node-2
```

![bg right:30%](images/18-neon_skull.jpg)

<!--
- The example cluster contains three hypervisor nodes

- Let's say that we want to perform service (upgrade, repair, etc.) on a node

- The "cluster evacuate" sub-command migrates all instances running on the specified host and
disables scheduling on it

- The example shows how our Alma Linux instance is moved from "node-1" to "node-2"
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © NASA/Bill Stafford (CC BY 2.0)" -->
## Other neat features
- Runs on a potato
- Automatic [overlay networking](https://wiki.ubuntu.com/FanNetworking)
- LXD also supports HW-level virtualisation
- Live migration... [sometimes](https://linuxcontainers.org/lxd/docs/master/howto/move_instances/)

![bg right:30%](images/18-space_training.jpg)

<!--
- Runs on a Raspberry Pi, no need for fancy hardware. If you have a few you can setup a cluster!

- As noted, LXD clustering is easy to get started with. The "lxc init" wizard can be setup an
overlay network for you, which enables communication between guests on different nodes regardless
if one of the hypervisor nodes is in your basement and the other on a VPS in a public cloud

- To make things a bit more confusing, LXD supports HW-level virtualisation with QEMU + KVM since
a few versions ago. While still a bit early, it's nice to not deal with libvirt and make use of
the easy clustering

- LXD brags about live migration of both OS-level and HW-level guests. This doesn't always work,
especially not for OS-level guests. As a rule of thumb, expect the ability to live migrate HW-level
guests but not OS-level guests (they are however usually quite fast to offline migrate)
-->
