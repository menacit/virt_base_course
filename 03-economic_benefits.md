---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Economic benefits"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "How virtualisation helps companies save money"
keywords:
  - "virtualisation"
  - "vm"
  - "container"
  - "cost"
  - "roi"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Bixentro (CC BY 2.0)" -->
# Economic benefits
### Time to save money and dress sharply

![bg right:30%](images/03-business_man_graffiti.jpg)

<!--
- It's all bout' the money, it's all bout the dumdudmudumdudm.

- Unfortuneatly this is what people other than nerds general care about.  

- Useful knowledge to understand how we got here.

- Important for you to make friends/get promoted/earn a decent salary at most places.

Segue: Let's start with the simple stuff - HW.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Sergei F (CC BY 2.0)" -->
## Less hardware means...
- Less data center space
- Less supporting infrastructure
- Less electricity and cooling
- Less things that can break

![bg right:30%](images/03-fly_on_knife.jpg)

<!--
- Data center space is expensive, as it needs to be secure, climate controlled and somewhat clean.

- Servers need a lot of supporting infrastructure such as network switches, UPSes and (especially)
back in the days KVMs (Keyboard-Video-Mouse, yikes). It all cost money and take space.

- These days it should not come as a surprise to anyone, but electricity is expensive. Cooling also
requires a lot of energy (in general).

- Lots of HW means that many things must be maintained and that can break - not just servers but
also supporting infrastructure. Humans need to fix/order/replace these, humans are expensive and
annoying: you need to find them, give em money and keep them happy.

Segue: Another thing to consider is that we barely use the computers that we've bought.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Roy Luck (CC BY 2.0)" -->
## _Studies_ show _average_ data center CPU utilization at 6-30%

![bg right:30%](images/03-oil_refinery.jpg)

<!--
- There are studies out there made by various actors: all of them show very low utilization.

- These have been produced with more or less effort: many contains circular references.

- Others, such as those published by Google and Alibaba are not likely not very representative of
average enterprise environments.

- Match instructors anecdotal observations.

- We can like fit these computing needs on a few hypervisors instead.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Jonathan Brandt (CC0 1.0)" -->
## Resource sharing means...
- Shared margins for resource utilization
- Easier capacity planning
- Cost savings through use of more efficient/powerful hardware

![bg right:30%](images/03-tumbler.jpg)

<!--
- We also don't need to think so much about margins. We can always vertically scale guests, in some
cases even without shutting down the instance: Linux supports hot swapping of CPUs and similar.

- Same goes for capacity planning, don't need to spend so much effort for every system.

- In general, more powerful HW is more cost efficient from a power and/or space perspective. It
would probably hard to motivate investment in such fancy HW without knowing if it would be used.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Wolfgang Stief (CC0 1.0)" -->
# Technical interlude

![bg right:30%](images/03-chips_on_pcb.jpg)

<!--
Let's take a deep breath: in order to explain further economic benefits we need to understand the
underlying technology a bit better. Let's talk about guest migration.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Austin Design (CC BY-SA 2.0)" -->
## Guest migration
Move VM from one hypervisor to another.

### Offline
Guest is shutdown before migration and started afterwards.

### Online
Guest remains running and is almost seamlessly migrated between hypervisors.

![bg right:30%](images/03-crystal_wave.jpg)

<!--
- In a clustered environment we can move guests between hypervisors

- Some solutions support migrating state (disk, memory, CPU registers, etc) and through slight of
hand make the guest run seamlessly on the other host. Some don't: offline VS online.

- While not a strict requirement, some type of shared storage for VM disks/file systems is required

- Not trivial, but we'll cover the implementation details later in the course.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Austin Design (CC BY-SA 2.0)" -->
# Back to business

![bg right:30%](images/03-smokey_man.jpg)

<!--
Time to tie the tie again.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Kuhnmi (CC BY 2.0)" -->
Migration of VMs, especially live, enables service of hypervisors during office hours.  
  
If hardware breaks, just start up the VM on another host.  
  
**Humans are likely the biggest cost.**

![bg right:30%](images/03-kolibri.jpg)

<!--
- Being able to do maintenance without screaming users is huge.

- Handling HW breakage seams trivial, not so much back in the days when Windows was tightly coupled
with the hardware it was installed on. Still not trivial - both due to actual and license problems

- Legacy systems can survive long past their HWs due date. Companies love this, sysadmins not so
much.

- Deserves repeating: Human labor is expensive and something most organisations try to avoid.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Jeena Paradies (CC BY 2.0)" -->
Deploying software stacks on hardware requires time consuming planning, procurement and setup.  
  
Automation and self-service features cuts time required for meetings and hand-overs.  
  
**Virtualisation makes organisations faster.**

![bg right:30%](images/03-frosty_lion.jpg)

<!--
- Costs needed to anticipated in detail. The requirement to pay a lot up front for new systems was
a huge barrier for startups/small players.

- Buying HW, finding space in a rack and making somewhat put it up takes a lot of effort.

- Lead times for hardware is really long these days and the supply chain is unpredictable.

- If we can remove humans we can start to automate things. Time consuming (expensive) to move tasks
between developers and HW team, lot's of room for errors and miscommunication.

- We wouldn't have devops the way it is today without virtualisation.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Jusotil_1943 (CC0 1.0)" -->
Virtualisation provides a (more or less) predictable execution environment.  
  
Testing, installation and support of complex software stacks is expensive.  
  
**Software vendors love virtual appliances.**

![bg right:30%](images/03-rusted_cards.jpg)

<!--
- Selling software that other parties are suppose to install, manage and/or maintain is a real
mess and quite annoying.

- You need to take a lot of variables into question: OS version, hardware/drivers, faulty setup.

- Before the problem used to be solved by shipping pizza boxes to customers, but that's also meh.

- Virtual appliances can be delivered preconfigured in a somewhat predictable environment, only
exposing limited configuration options that the customers can screw up.
-->
