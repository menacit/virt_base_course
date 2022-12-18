---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Cons/Negatives"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Downsides of using virtualisation"
keywords:
  - "virtualisation"
  - "vm"
  - "container"
  - "security"
  - "performance"
  - "economics"
  - "cons"
  - "negative"
  - "downsides"
  - "cost"
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
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Wendelin Jacober (CC0 1.0)" -->
# Downsides of virtualisation
### ~~The good~~, the bad and the ugly

![bg right:30%](images/07-crashed_bus.jpg)

<!--
Not all is a dance on roses.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Tofoli Douglas (CC0 1.0)" -->
## Economics
More messy licenses to care about.  
  
System sprawl - many guests to take care of.

![bg right:30%](images/07-mountain.jpg)

<!--
- Software vendors that sell licenses are happy for virtualisation.

- Quite easy to spin up new systems without thinking about the effort required to take care of
them: they still need to patched and when they break humans take care of them. 
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Jesse James (CC BY 2.0)" -->
## Reliability
More code means more complexity and things that can break.  

Large blast radius if virtualisation fails.
  
Lazy ways to implement reliability aren't always the best ones.

![bg right:30%](images/07-man_statue.jpg)

<!--
- All the abstractions can introduce... interesting problems and breakage.

- High-availability is usually best implemented near the application. A client that can handle
reconnections and migration between remote endpoints is likely a way simpler solution.

- Reality may not always meet expectations: migration can fail and introduce problems. 
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Kristina Hoeppner (CC BY-SA 2.0)" -->
## Security
Isolation is not perfect, many eggs in one basket.  
  
Must trust underlying infrastructure, control plane and humans.  
  
Way to easy to spin-up and forget about systems.

![bg right:30%](images/07-sheep.jpg)

<!--
Basically what the slide says.
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Jonathan Brandt (CC0 1.0)" -->
## Performance
Always some overhead, depending on workload it may be significant.  
  
Less predictable due to "noisy neighbours" and hidden counters.  
  
Trickier to utilize accelerators and CPU features.  

![bg right:30%](images/07-neon_voxel.jpg)

<!--
- All emulation has a performance cost. OS-level virt usually introduce way less, but still there.

- Depending on workloads this can be a big deal: especially I/O intensive workloads tend to suffer.

- You can't always know how well your instance will perform, has the HW is shared among others.
One day can be fine while the next is shit. Hypervisors are almost always overprovisioned.

- Lot of sensors and counters used for advanced performance analysis can't be observed from inside
the guest, making debugging and performance analysis trickier.
-->
