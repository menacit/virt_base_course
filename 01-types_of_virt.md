---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Types of virtualisation"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Why we started using virtualisation and what types there"
keywords:
  - "virtualisation"
  - "vm"
  - "container"
  - "background"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Reid Campbell (CC0 1.0)" -->
# Background and basics
### Why and how we virtualise 

![bg right:30%](images/01-orca.jpg)

<!--
- We'll begin with a retrospective to understand how we ended up where we are today

- Try to clarify the different kinds of virtualisation available
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Robert Sullivan (CC0 1.0)" -->
## Computers were humans.

![bg right:30%](images/01-human_computers.jpg)

<!--
- A bit of pop history: The picture shows a group of NACA computers, precursor to NASA

- Often rooms full of women, minorities and anyone else not considered fully esteemed

- Things started to change with a lot with Turing's Christof computer

- Not get stuck here, it's fun but there are whole books available for those who are interested
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © C. Watts (CC BY 2.0)" -->
## Computers became...
- Problem specific devices
- General purpose
- Time-shared/multi-user

![bg right:30%](images/01-old_computers.jpg)

<!--
- Digital computers became a thing a big thing as they could solve things a lot faster than humans

- Slowly but surely became field-programmable and general purpose, saved a lot of money!

- Everyone (see all scientists and fortune 50s) wanted access to a computer, so time sharing and
remote access became a thing: a very early version of the cloud, many experts at the time thought
computing would be provided by regional providers in a similar manner to water and electricity.
The word terminal is still with us - but the view of computing as a utility look slightly dif.

- Multi-user systems became the norm and suddenly not everyone with access to the computer were
equally trusted or given equal amounts of processing power. Things started to get more and more
complex. Richard Stallman, the father of GNU and the FOSS movement, was famous for actively working
against restrictions of computer usage.

Segue: Proto-virtualisation already exist in different forms on mainframes, but in the beginning of
the 2000s the need becomes apparent in the commodity server market as well.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Beraldo Leal (CC BY 2.0)" -->
## Initial motivations
To save money and "keep things simple".

![bg right:30%](images/01-sunfire_dark.jpg)

<!--
- So what were the main motivations: basically what the slide says

- Up until that point, every hertz could have a use and the benefits (see dreamy eyed potential) of
digitalization had been many. Maybe the IT bubble burst started putting focus on cost again.

- Computers had started to become way too powerful for single tasks, but the security model of OSes
had remained largely the same - multi-tenancy was not simple and admin privileges, which were more
or less required for everything, were omnipotent and hard to restrict.

- Ofc these problems aren't impossible to solve, but the effort required to change hardware,
software and way-of-working (see knowledge) was deemed like too big of a task.

Segue: Two primary methods for solving these problems started to appear
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Jonathan Brandt (CC0 1.0)" -->
## HW-level virtualisation
Pretend to be hardware well enough to make operating systems run.

## OS-level virtualisation
Pretend to be an operating system environment well enough to run applications.

## Domain-specific virtual machines
More about that later...

![bg right:30%](images/01-tree_glitch.jpg)

<!--
- HW-level virtualisation is probably what comes to mind for most people when they hear the term.

- If you used VirtualBox, you know this.

- Quite complex and slow to pretend to be hardware, but the method soon showed many benefits.

- Make legacy operating systems and applications run without customisation: business as usual.

- Most users do however not care about how the OS is doing, they care about their apps running.

- OS-level virtualisation tries to provide an environment that is as close as possible to what
applications and admin expects: It's job is not to fool the operating system.

- OS-level virtualisation requires changes of OS, but probably easier than pretend to behave like
a physical object with all it's quirks.

- Mostly used to virtualise OSes of the same kind (Linux on Linux) but not only

- The ideas of uncoupling applications from hardware and/or operating systems became a thing as
well, but more about that later in the course: For now focus on HW-level and OS-level virt.

Segue: To make things a bit less diffuse, let's talk about early contenders in the field.

-->

---
## VMware
- Early player introducing the industry to x86 virtualisation
- Capable of virtualising hardware for most operating systems
- Still popular today, though a bit messy

![bg right:30%](images/01-vmware_web_2000.jpg)

<!--
- Company that brought HW-level virtualisation to the masses since the early 2000s.

- Many people considered it a bit of a moon shot at the time.

- While slow it quickly became popular as it helped companies save a lot of money (more about that
later in the course).

- Early in the space of clustering nodes.

- Used to be unchallenged king of HW-level virt for a long time, but these days there are several
who battle for the title: many which are freely available.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Fandrey (CC BY 2.0)" -->
## FreeBSD Jails
- Introduced in version 4.0 (2000)
- Lazy solution to "UID 0 problem"
- Most OS functionality provided in an isolated manner to each jail
- Very popular for web and shell hosting

![bg right:30%](images/01-console_beastie.jpg)

<!--
- First virtualisation on UNIX, inspired Solaris Zones, OpenVZ and other solutions.

- The "UID 0 problem" was the main focus: Splitting root up into smaller parts was deemed to much
a hassle.

- Create isolated jails, which have their own root and own view of the system, such as processes
and the file system root.

Segue: We are already using a lot of terms, let's try to clarify what some of them mean.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Jonathan Miske (CC BY-SA 2.0)" -->
## Glossary and loose synonyms

### Physical machine
Host, hypervisor, virtual machine manager (VMM)

### Virtual machine
Guest, instance, VM


![bg right:30%](images/01-abandoned_silo.jpg)

<!--
Many of these terms are not strictly correct, but they are widely used so I've tried to group them.
-->
