---
SPDX-FileCopyrightText: © 2026 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: OS-level virtualisation recap"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Recap of OS-level virtualisation part in course"
keywords:
  - "virtualisation"
  - "vm"
  - "container"
  - "recap"
  - "introduction"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dan Rademacher (CC BY 2.0)" -->
# Course progress recap
### Refreshing what we've learned so far

![bg right:30%](images/34-wooden_space_station.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Dan Rademacher (CC BY 2.0)" -->
Talked about the differences between
HW-level and OS-level virtualisation.

Better performance and lower overhead.

Pretend to be another OS  
_and/or_  
Create an isolated environment.

![bg right:30%](images/34-wooden_space_station.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Sergei F (CC BY 2.0)" -->
There is no such thing as a "OS-level VM" 
from the Linux kernels perspective.

A bunch of different kernel features are
glued together by tools like LXC.

Many of these have other use-cases
besides basic virtualisation.

![bg right:30%](images/34-retro_switchboard_sepia.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Nirvana Studios (CC BY 4.0)" -->
The main downsides compared to
HW-level virtualisation is
weaker security isolation
and worse reliability.

![bg right:30%](images/34-scrapy_diver.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Simon Waldherr (CC BY-SA 4.0)" -->
We also talked about the challenges
related to collaborative development
and distribution/deployment of
complex software stacks.

Need for tools to help us use
predictable execution environments
and minimize error-prone manual setup.

(More about solutions later today!)

![bg right:30%](images/34-cern_lhc_side.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Kurayba (CC BY-SA 2.0)" -->
Questions or thoughts
before we move on?

![bg right:30%](images/34-bismuth.jpg)
