---
SPDX-FileCopyrightText: © 2023 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Security benefits"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "How virtualisation helps organisations build and operate more secure systems"
keywords:
  - "virtualisation"
  - "vm"
  - "container"
  - "security"
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
<!-- _footer: "%ATTRIBUTION_PREFIX% Tim Green (CC BY 2.0)" -->
# Security benefits
### (Yes, there are several)

![bg right:30%](images/06-moss_face.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kuhnmi (CC BY 2.0)" -->
## Safely running multi-user/multi-tenant systems is hard.

![bg right:30%](images/06-birds.jpg)

<!--
- One of the initial motivations for using virtualisation.

- Most companies don't fully trust all their employees: even fewer their competition. Multi-tenancy
is an important use-case to save money but hard to do in commodity general purpose OSes.

- Simpler to just use VMs per customer/user/applications.

Segue: Besides keeping things simple, limiting what the job for a host is has other benefits.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Austin Design (CC BY-SA 2.0)" -->
## One VM per task enables...
- A smaller attack surface
- Fewer privileged users per system
- Tighter network restrictions
- Easier anomaly and intrusion detection

![bg right:30%](images/06-tower.jpg)

<!--
- From a infosec perspective, we want a small attack surface. Less services means less code means
less risk for security vulnerabilities.

- Perhaps not everyone in the IT staff needs to be root on every system? Still often the case, but
for security sensitive organisations this is now an option.

- Systems that perform a limited set of tasks are easier to restrict and monitor, lot's of noise
otherwise.

Segue: Some people have taken this reasoning to heart and very far.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Freestocks.org (CC0 1.0)" -->
[Qubes OS](https://www.qubes-os.org/) and [unikernels](https://en.wikipedia.org/wiki/Unikernel)
such as [MirageOS](https://mirageos.org/) represent the logical extreme of these arguments.

![bg right:30%](images/06-christmas_sweater.jpg)

<!--
- Qubes OS runs everything in VMs: there is no reason why your personal web browsing should be able
to compromise your work for customer X. We'll talk more about Qubes later in the course.

- Unikernels (or library OSes) builds a runtime environment which bundles an application and only
enough OS to get things running. Great to minimize attack surface and keep things performant, low
overhead for kernel context switching.

- Wouldn't be reasonable if it wasn't for the predictable runtime environment that virtualisation
provides.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Wolfgang Stief (CC0 1.0)" -->
## Computers are stateful
Snapshots enable a more aggressive security patching process.
  
Properly cleaning up a hacked server is no trivial task - neither is forensics.  
  
Modifications and malware cannot only hide in the OS, but also in firmware and OoB mechanisms.

![bg right:30%](images/06-computer.jpg)

<!--
- Being able to utilise snapshots to aggressively change systems (such as apply updates) has many
security benefits as well.

- Snapshots provide a known good state: extremely helpful if a system is hacked. Can also be used
to dif in order to find what the hacker did.

- Physical computers store a lot of state that can be changed and persisted even after an OS is
reinstalled (or even if the disk is physically destroyed.

- Also relevant for multi-tenancy: how had and who will have access to the server after you?

- The server HW industry has started to make changes, but VMs are far supreme in this case.
-->
