---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Reliability benefits"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "How virtualisation helps organisations build more robust infrastructure"
keywords:
  - "virtualisation"
  - "vm"
  - "container"
  - "sre"
  - "reliability"
  - "redundancy"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Meddygarnet (CC BY 2.0)" -->
# Reliability benefits
### Not only nerds care about uptime

![bg right:30%](images/04-soldering_robot.jpg)

<!--
Virtualisation helps us run systems reliably, but how?
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Loco Steve (CC BY-SA 2.0)" -->
## Virtualisation enables...
- Easy maintenance of hypervisors and supporting infrastructure thanks to migration
- Legacy workloads to run on decent and supported HW
- Less maintenance work due to less HW
- Better testing due to predictable runtime environment

![bg right:30%](images/04-train.jpg)

<!--
A lot of the same things that make virtualisation good from an economic perspective applies to
reliability as well.

Segue: There are some other neat benefits as well.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Takomabibelot (CC BY 2.0)" -->
Makes multi-server and multi-site redundancy economically viable for many organisations.

![bg right:30%](images/04-number_three.jpg)

<!--
- Computers break, we should not rely on a single one. Same goes for data centers.

- Three is a magic number in computing (and voting in general) as it enables a quorum to be kept.
Redundancy with two nodes may be better than with none, but handling state and data is a mess:
requires a lot of fencing and painful reconciliation.

- Would be quite expensive and out of the questions for most organisations to do this with HW only.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% J.V.R Sharma (CC BY-SA 2.0)" -->
## Snapshots
- Freeze and store guest state
- Roll back changes with ease
- Enabled through Copy-On-Write disk storage and/or overlay file systems

![bg right:30%](images/04-cow_sheep.jpg)

<!--
- The ability to capture state of a guest and roll back.

- Some virtualisation solutions only support disk snapshots and not RAM/CPU state. Really only
matters if you want to be able to revert instance to an already running state.

- Modern filesystems also implement snapshots, but VM snapshots leave less room for trouble.

- Important to note that a disc only snapshot should preferably be taken when the guest is shut
down: things could be cached in memory, databases are notorious.

Segue: Let's put this feature to some use for reliability.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Nicholas Day (CC BY 2.0)" -->
Snapshots enables operators to apply bug fixes and perform other changes with more confidence.

![bg right:30%](images/04-color_glitch.jpg)

<!--
- Organisations are often scared to mess with things "that work", even when needed or the change
improves reliability long-term.

- Move fast and don't break thing.
-->

