---
SPDX-FileCopyrightText: © 2023 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: OS-level virtualisation technology"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Overview of features and technology which enables OS-level virtualisation on Linux"
keywords:
  - "virtualisation"
  - "os"
  - "vm"
  - "container"
  - "internals"
  - "cgroup"
  - "namespaces"
  - "chroot"
  - "linux"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Enrique Jiménez (CC BY-SA 2.0)" -->
# OS-level virtualisation
### How does it work on Linux?

![bg right:30%](images/19-silicon_wafer.jpg)

<!--
- We'll take a peak into which features of Linux that enable solutions like LXC and VZ to work

- Don't expect you to remember all details and commands, but these isolation features serves as
the for OS-level virtualisation security.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Eric Nielsen (CC BY 2.0)" -->
There is no such thing as a OS-level VM in the Linux kernel.  
  
Gluing together features like _chroot_, _namespaces_ and _cgroup_ creates the illusion.  
  
This functionality has other neat use-cases besides virtualisation.

![bg right:30%](images/19-abandoned_house.jpg)

<!--
- There is no spoon

- Unlike OSes such as FreeBSD and Solaris, there is no kernel concept of a OS-level VM in Linux

- For better or worse, a hodgepodge of technologies are used together to build something that looks
like an OS on a real server

- The flip side of this is that the features can be used to achieve other kool things outside of
the system virtualisation space

- We won't cover all technologies, but rather focus on the core ones

Segue: We have to start some where, may as well travel back to the epoch...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
## chroot
- Introduced in UNIX during the 70s
- "Change file system root"
- Not designed as a security feature

![bg right:30%](images/19-pdp.jpg)

<!--
- Somewhat mysterious origins

- Theory is that it was originally developed to aid development of new UNIX OS versions

- Syscall to change a process (and sub-processes) view of the file system three

- Prevent processes in chroot from accessing files outside of the specified directory

- Not designed for security, as were about to see

Segue: Probably makes more sense with an example...
-->

---
```
$ sudo debootstrap buster my_debian_root http://deb.debian.org/debian/

I: Retrieving InRelease 
I: Resolving dependencies of required packages...
I: Retrieving libacl1 2.2.53-4
[...]
I: Configuring libc-bin...
I: Base system installed successfully.
```

```
$ ls my_debian_root/

bin  boot  dev  etc  home  lib  lib32  lib64 [...]
```

<!--
- Debootstrap is a tool to download and "install" a Debian-based distribution into a directory

- Used by installers and similar during system setup

- In this example Debian 10 (codename "buster") is installed to the directory "my_debian_root"

- When listing files in the directory, we recognize these from the file system root ("/")

- This will serve as the base for our chroot
-->

---
```
$ cat /etc/os-release | grep -F PRETTY_NAME
PRETTY_NAME="Ubuntu 22.04.1 LTS"

$ sudo chroot my_debian_root /bin/bash

root@node-1:/# cat /etc/os-release | grep -F PRETTY_NAME
PRETTY_NAME="Debian GNU/Linux 10 (buster)"
```

<!--
- To show that this actually, OS information is printed on the host and in the chroot ("guest")

- The CLI program "chroot" uses the "chroot" syscall

- Spawn an interactive shell in the chroot (bash)

- Notice how the prompt change, this is Debian's default prompt

- The file "/etc/os-release" in the Debian chroot is actually "my_debian_root/etc/os-release"

Segue: This kind-of-works, we have some sort of proto-virtualisation going on here, but as I said
chroot was not designed as a security feature...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Andrew Hart (CC BY-SA 2.0)" -->

```
root@node-1:/# dmesg | wc -l
1002

root@node-1:/# ps -xa | grep password
/bin/pacemaker loop --password G0d!

root@node-1:/# tcpdump -i eth0

tcpdump: listening on eth0
[...]
160 packets captured
```

![bg right:30%](images/19-broken_glass.jpg)

<!--
- The same kernel is shared inside and outside of the chroot

- root is still root and can list/kill/manipulate processes, read sensitive kernel logs, dump
network traffic, load kernel modules, restart the host, etc.

- The only thing that is isolated is the file system

Segue: How do we solve this? Kernel namespaces is a part of the solution...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Torkild Retvedt (CC BY-SA 2.0)" -->
## Namespaces
"Functionality to partition a group of processes view of the system".  
  
Host can see through all, members can't.  

We'll focus on "process", "network" and "user".

![bg right:30%](images/19-cameleon.jpg)

<!--
- Since the early 2000s, the Linux kernels namespace functionality has grown organically

- Allows us to create new and isolated "views" of parts of the kernel, such as users, file systems,
network interfaces/routes processes

- Members in this case is one or more processes (including their sub-processes)

- Works like a one-way mirror, the host can see what is going on inside all namespaces, but their
members can only see things in their dedicated namespace(s)

- There are currently eight different ones and new ones are in development, we'll focus one the
ones that are most important and/or easy to understand

- Cgroup, IPC, Network, Mount, PID, Time, User, UTS

Segue: This is a bit complicated to explain, some examples may help...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% David J (CC BY 2.0)" -->
## Process/PID namespace
Members get their own view of the process tree.

![bg right:30%](images/19-tree.jpg)

<!--
- All programs that are started on a Linux system (processes) gets their own process ID (PID)

- The PIDs start from 1, which is the first program started upon boot and typically an init system
like systemd or OpenRC

- A user can view/kill/interact with their own processes, root can do it for all (by default)

- A malicious program could do bad thing with other processes

- The PID namespace gives it members it's own listing - a PID inside a NS may be 5 from the
perspective of the host, but 1 inside the namespace

- This means that namespace members can only mess with their own processes
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Helsinki Hacklab (CC BY 2.0)" -->
```
$ ps -e | head -n 4
PID   TTY   TIME      CMD
1     ?     00:00:01  systemd
2     ?     00:00:00  kthreadd
3     ?     00:00:00  rcu_gp

$ sudo chroot my_debian_root ps -e | head -n 4
PID   TTY   TIME      CMD
1     ?     00:00:01  systemd
2     ?     00:00:00  kthreadd
3     ?     00:00:00  rcu_gp
```

![bg right:30%](images/19-led_smile.jpg)

<!--
- Listing of processes inside and outside of the chroot, showing their the same
-->

---
```
$ ps -e | head -n 4
PID   TTY   TIME      CMD
1     ?     00:00:01  systemd
2     ?     00:00:00  kthreadd
3     ?     00:00:00  rcu_gp

$ sudo unshare --fork --pid -- chroot my_debian_root /bin/bash

root@node-1:/# ps -e
PID   TTY   TIME      CMD
1     ?     00:00:00  bash
2     ?     00:00:00  ps
```

<!--
- "unshare" and "nsenter" are two good CLI utilities for playing around with NSes

- In this case, we create a new PID namespace that the chroot command is executed in

- The example shows how PID 1 is different in these contexts 
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dave Herholz (CC BY-SA 2.0)" -->
## Network namespace
Separate "network stack" for members processes.  
  
Example use-cases:
- Configure per-application FW rules
- Force cherry-picked services through a VPN
- Handle overlapping network segments 

![bg right:30%](images/19-network_switches.jpg)

<!--
- The network namespace may be the most versatile one

- When a new network NS is created, no network devices are in it and it got it's own routing table,
firewall rules, etc

- We can either move one or more physical interfaces into the NS or virtual interface route through
the host namespace

- This is how OS-level guests are network isolated from each other, but very useful in other cases
as well as the slide says

TODO: Write better descriptions of non-virt use-cases
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Thierry Ehrmann (CC BY 2.0)" -->
## User namespace
Root in chroot is root.  
  
Lots of things such as package managers expect root privileges, but don't really need it.  
  
User namespaces give members their own group and user lists.

![bg right:30%](images/19-wireframe_head.jpg)

<!--
- Read the first sentence five times fast!

- As mentioned, root in the chroot can still mess with the shared kernel

- Many things expect to be run as root/UID 0, but don't usually need it as they only poke around on
the file system ("my_debian_root" in this case) and won't use dangerous/fancy kernel features

- Like the PID NS, members of a user NS get their own account list: UID 0 (root) for the NS members
may be UID 2031 on "the host"/outside of the NS

Segue: Could talk about NSes, let's move on to cgroups...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pete Seeger (CC BY 2.0)" -->
## cgroup
Members usage of system resources (CPU, memory, disk I/O, etc.) can be limited.  
  
Used together with [CRIU](https://criu.org/) for live migration.  
  
[Not just used for virtualisation](https://www.redhat.com/sysadmin/cgroups-part-four).

![bg right:30%](images/19-bonzai_tree.jpg)

<!--
- Control groups

- Limit how much resources a group of processes can use

- Possibility to pin the on specific CPU cores for example, which can be good for performance and
security (prevent "noisy neighbors" on the CPU core, keep cache warm/isolate)

- Supports a feature called checkpointing which can be used to snap the state of processes in a
cgroup - this state can be restored or migrated to another host (in some cases hehe) 

- Heavily used by systemd, all services and users run in their own cgroup to allow granular
resource measurements/restrictions. Also good if you wanna kill a service and don't leave zombie
process lying around (https://en.wikipedia.org/wiki/Zombie_process)
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Wendelin Jacober (CC0 1.0)" -->
## seccomp
Limit which/how system calls can be used.  
  
Some syscalls allows breakout of isolation.  
  
Minimize attack surface of shared kernel.  

![bg right:30%](images/19-telephone_booth.jpg)

<!--
- Mentioned system calls (syscalls) several times during the course: the way user applications tell
the kernel to do things, such as open files or network sockets

- x86_64 Linux expose over 300 different syscalls, some of which are simple and others with complex
configuration options (syscall arguments)

- Large attack surface, some are know to break isolation. We don't want a guest to be able to issue
a syscall that reboots the system, do we?

- As always, we want to limit the attack surface: most applications don't use too many of them any
way

- Some applications, like the Firefox rendering process, do this to sandbox itself and limit
potential things an attacker could do if compromised

Segue: We've talked about how OS-level virtualisation was partly introduced as making proper
multi-user/admin restrictions to tricky. Well, we've tried to do that also...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Bengt Nyman (CC BY 2.0)" -->
## Capabilities 
Originally developed to make root less omnipotent.  
  
Caps like "NET\_BIND\_SERVICE" and "SYS\_CHROOT" can be given to non-root users.  
  
Not very fine-grained and some are unsafe.

![bg right:30%](images/19-cg_16.jpg)

<!--
- Does root in all cases need to be able to do everything?

- Doesn't it seem stupid to give a user root privileges if they "only" need to modify network
settings?

- Capabilities can be given/taken away from processes, including root processes

- It can also be configured as an extended attribute for executable files

- A typical historic use-case was to run network services as root if they needed to listen to a
port beneath 1023 (https://www.w3.org/Daemon/User/Installation/PrivilegedPorts.html). This is an
unnecessary risk, as an attacker would often gain complete root access if the service was owned

- The capability "CAP_NET_BIND_SERVICE" also non-root processes to do this

- chroot normally requires root privs, but there exist a capability to change that

- The available caps often allow much more functionality than may be needed. Some like
"CAP_NET_ADMIN" have known flaws as it exposes functionality that can be used to gain unrestricted
root access. It's tricky to bolt on these types of restricts after a system has been built and the
interest in fixing it is limited

- Removing caps for a OS-level guest can minimize the kernel attack surface
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Stacy B.H (CC BY 2.0)" -->
**These and other features make up the beautiful mess we call OS-level virtualisation on Linux!**

![bg right:30%](images/19-panda.jpg)

<!--
- We've only scratched the surface, a lot of other things make up OS-level virt

- Could go more in-depth if interest and time exist

- Understand that it's a lot to take in, especially if you're not super comfortable with Linux

- As noted, you're not expected to remember all of this in detail. If you can only take away one
thing, that is OS-level virtualisation on Linux is comprised of several parts and not developed
as one feature, which will lead to some issues as we're about to see
-->
