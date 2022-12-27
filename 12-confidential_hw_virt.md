---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Confidential computing"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "How hardware features can be used to improve virtualisation security"
keywords:
  - "virtualisation"
  - "vm"
  - "confidential"
  - "infosec"
  - "security"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Nikki Tysoe (CC BY 2.0)" -->
# Confidential computing
### How to make virtualisation a bit safer

![bg right:30%](images/12-space_invander.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Eric Chan (CC BY 2.0)" -->
Traditionally, we must trust the hypervisor and operators of underlying infrastructure.  

![bg right:30%](images/12-jellyfish.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Eric Kilby (CC BY-SA 2.0)" -->
We can encrypt disks of instances, but with somewhat limited value.

![bg right:30%](images/12-sloth.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Jan Bommes (CC BY 2.0)" -->
Operators can build trust using transparency.  
  
Trust may not be enough due to regulatory requirements.  
  
Even if operators act in good faith, things can still get owned.

![bg right:30%](images/12-broken_floor.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Quinn Dombrowski (CC BY-SA 2.0)" -->
Currently lots of interest (see "money") in solving these issues for cloud and edge computing.

![bg right:30%](images/12-switches.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Sergei F (CC BY 2.0)" -->
## Memory encryption
- Prevent host (and other guests) from peaking at VM memory
- Guests are still vulnerable against many different attacks
- AMD SEV is an example


![bg right:30%](images/12-rusty_lock.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Lydur Skulason (CC BY 2.0)" -->
## "Full guest isolation"
- Hardware and software features to prevent host from messing with guests
- Guests verify runtime environment before starting/decrypting data
- Intel tries to solve this with [TDX](https://intel.github.io/ccc-linux-guest-hardening-docs/)
- AMD [SEV-ES](https://developer.amd.com/sev/) is another solution


![bg right:30%](images/12-snow_dome.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Fritzchens Fritz (CC0 1.0)" -->
## What's the catch?
- Still early days, lacking support in virtualisation software stack
- Current state of verified boot is quite bad, especially in Linux distributions
- Requires trust in proprietary black boxes
- Several vulnerabilities have been identified

![bg right:30%](images/12-broken_cpu.jpg)

<!--
TODO
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Graham Drew (CC BY 2.0)" -->
Mayhaps a good complement to minimize risk, if understood properly.

![bg right:30%](images/12-sinking_boat.jpg)

<!--
TODO
-->

