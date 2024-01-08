---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Recap"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Review/Recap of virtualisation course"
keywords:
  - "virtualisation"
  - "pros"
  - "cons"
  - "summary"
  - "review"
  - "security"
  - "economics"
  - "environment"
  - "reliability"
  - "container"
  - "vm"
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
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
# Virtualisation course recap
### Summarising what we've covered

![bg right:30%](images/33-hdd_macro.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Freed eXplorer (CC BY 2.0)" -->
# Exercise: Help the CTO
Participants are split into four or more groups.  
  
Each group is assigned to present **either** the economic, reliability, security or environmental
pros/cons of virtualisation, targeted towards a **CTO role** in an assigned example organisation.  
  
The presentation should cover usage of HW-/OS-level virtualisation, virtual/container development
and VDI. After presentation, send slides to
**[courses+virt\_013301@%EMAIL_DOMAIN%](mailto:courses+virt_013301@%EMAIL_DOMAIN%)**

![bg right:30%](images/33-cave.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Yves Sorge (CC BY-SA 2.0)" -->
## Org. 1: Examplify
Cash strapped startup on a mission to make developers (and stockholders) happy.  
  
Develops, hosts and supports a solution for collaborative coding.  
  
Needs to grow fast and has employees all over the world working from home.  
  
**Focus on the economic pros/cons.**

![bg right:30%](images/33-rocket.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
## Org. 2: Xample Industries
Well-established company in heavy-manufacturing.  
  
Every second of downtime and delays means huge monetary losses.  
  
Depend on many legacy IT systems for their factory production line. 
  
**Focus on the reliability pros/cons.**

![bg right:30%](images/33-welding.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
## Org. 3: Department Of Examples
Spook agency making the world a safer place.  
  
Keeping information secret and systems secure is of uttermost importance.  
  
Plagued by bureocrats, spies and sinister insiders.  
  
**Focus on the security pros/cons.**

![bg right:30%](images/33-cyber.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Gerben Oolbekkink (CC BY 2.0)" -->
## Org. 4: Example Airways
Transportation company with urgent need for efficient greenwashing.  
  
Has several data centers spread around the world.  
  
Need to handle the occasional surge of visitors and bookings on their website.  
  
**Focus on the environmental pros/cons.**

![bg right:30%](images/33-butterflies.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Mauricio Snap (CC BY 2.0)" -->
**Remember the target audience/focus area.**  
  
**If it suites your presentation, add/modify the example organisation's challenges.**

![bg right:30%](images/33-eye.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% OLCF at ORNL (CC BY 2.0)" -->
## Let's summarise!

![bg right:30%](images/33-data_center.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jennifer Morrow (CC BY 2.0)" -->
## Economic benefits
Less HW == Less electricity, DC space and painful human labor.  
  
Enables self-service and automation which helps organisations move faster.

![bg right:30%](images/33-sphere.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% USGS EROS (CC BY 2.0)" -->
## Reliability benefits
Maintenance of underlying infrastructure without disruptions.  
  
Easier testing and operations due to predictable runtime environments.  
  
Enables quick recovery to a good known state. 

![bg right:30%](images/33-satellite_photo.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
## Security benefits
Reduces attack surface through fine grained segmentation of systems.  
  
Enables users to somewhat safely handle untrusted data.  
  
Enables quick recovery to a good known state. 

![bg right:30%](images/33-lock.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Nacho Jorganes (CC BY-SA 2.0)" -->
## Environmental benefits
Less HW == less e-waste and energy consumption.  

![bg right:30%](images/33-cow.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dennis van Zuijlekom (CC BY-SA 2.0)" -->
## OS-level > HW-level
- Faster!
- More efficient/higher density
- Easier to inspect and monitor

![bg right:30%](images/33-core_memory.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Marco Verch (CC BY 2.0)" -->
## OS-level < HW-level
- Easier to break isolation
- Less stable/predictable
- Barley supported live-migration

![bg right:30%](images/33-pcb_macro.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Bret Bernhoft (CC0 1.0)" -->
# DE\_END
### Thanks for listening!

![bg right:30%](images/33-abstract_party.jpg)
