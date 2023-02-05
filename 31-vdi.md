---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: VDI"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Pros and cons of VDI"
keywords:
  - "virtualisation"
  - "pros"
  - "cons"
  - "container"
  - "vm"
  - "vdi"
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
<!-- _footer: "%ATTRIBUTION_PREFIX% Thierry Ehrmann (CC BY 2.0)" -->
# Introducing VDI
### "Virtual Desktop Infrastructure"

![bg right:30%](images/31-street_art.jpg)

<!--
- We've talked about virtualising servers and running VMs on the desktop

- Why not virtualise the desktop?

- Many do and any many more have tried, turns out that what seems like a good idea may not be so

- VDIs popularity comes and goes.

Segue: But why, whats the idea?
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Scott McCallum (CC BY-SA 2.0)" -->
**Goal: Centralise compute resources.**

![bg right:30%](images/31-turtle.jpg)

<!--
- In the beginning, there were large computers with user facing terminals connected to them

- These terminal were little less than a screen, keyboard and perhaps a futuristic looking mouse

- Didn't have much of choice at the time, when computers became cheaper everyone started getting
their own. This represented a decentralisation

Segue: What are the benefits with centralising people's desktops? Many are the same as for servers
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Bret Bernhoft (CC0 1.0)" -->
## Resource pooling means...
- Less overall hardware
- More processing power when needed
- Shared usage of expensive software and accelerators such as GPUs

![bg right:30%](images/31-towers.jpg)

<!--
- As with server workloads, we can often overprovision the hypervisors running virtual desktops

- Margins need to be a lot smaller. If everyone has the occasional need to perform a performance
critical task, everyone needs a somewhat beefy machine. Chances are that these needs are not
concurrent for all users, meaning that pooling makes a lot of sense.

- The same goes the other way: a virtual desktop could be a lot more powerful if the guest is
running on server HW than would be possible to fit in a light-weight laptop

- Powerful accelerators, such as CAD GPUs, could be plugged into energy-efficient servers in
climate-controlled data centers instead of being crammed into bulky desktop workstations

- Access to powerful computers on demand make a lot of sense and, at least in theory, would save
a lot of money for each individual user

- Some software has very annoying licenses and/or very specific runtime environment requirements

- Especially if there is only the occasional need, sharing this SW through virtual desktops could
make a lot of sense

- Basis for streaming gaming services such as Google Stadia and Geforce Now

- Many cloud providers offer powerful virtual desktops with accelerators for usage on-demand
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Bret Bernhoft (CC0 1.0)" -->
Minimize cost of setup, management and support.  
  
Allows admins to focus their efforts in one place to store and backup data securely\*.

![bg right:30%](images/31-metal.jpg)

<!--
- IT admins can use scripts to automatically create and update virtual desktops when needed

- Supporting users with physical desktops around the world can be a PITA

- If the virtual desktop has been corrupted or suspicious software has been installed on it,
snapshots and/or image templates can be used to quickly return to a working state

- User stores important/sensitive data on their local HDDs, USB drives and similar. Besides the
risks of these getting stole/lost, backing up the data can be hard

- You can't really steal virtual desktop. When a physical laptop is stolen/lost (especiall if
powered on), lots of work is required to make sure that access is revoked and that the sensitive
information was actually inaccessible/encrypted at the time
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Bocek (CC BY 2.0)" -->
## How do users access their virtual desktops?

![bg right:30%](images/31-telephone_pole.jpg)

<!--
- So far we've talked about these things very abstractly

- Usually the virtual desktops are run with HW-level virtualisation and in some cases OS-level

- How to users gain access to these? They need a network connection, but what else?
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% VIA Gallery (CC BY 2.0)" -->
## Thin clients
Low-cost devices with a NIC, display output and basic I/O. No internal storage.  
  
Minimum local compute resources.  
   
Typically shared between multiple users.

![bg right:30%](images/31-thin_client.jpg)

<!--
- Boring low-cost low-energy computers with one job: connect the user to a central computer

- Designed to be low maintenance

- Connect a screen, keyboard, mouse and network connection

- Typically mounted behind a screen or under the table. Commonly spread throughout an office/campus

- Used to all look more or less like in the picture, these days many look like a ChromeCast

- Quite need, especially if combined with a smart card: just plug it into any device in any room
and access your desktop how you last left it
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Adam Greig (CC BY-SA 2.0)" -->
## Web and native apps
Allows users to access their virtual desktop from any device anywhere at any time.  

![bg right:30%](images/31-retro_computer.jpg)

<!--
- If you've used RDP, it's a lot like that

- Can be quite nice for users that work from multiple devices in multiple locations: at least their
desktop/running apps become consistent

- Quiet cheap if users can utilize their own devices to run the client on

- IT doesn't need to maintain any desktop hardware, yay!

- Popular with economically constrained and globally diverse organisations

Segue: This presentation wouldn't be part of the course if we didn't end on a low note...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Maja Dumat (CC BY 2.0)" -->
## The downsides...
- Many users still need offline compute
- Requires stable low latency connection
- Client must still be trusted
- Many eggs in one basket

![bg right:30%](images/31-bunker.jpg)

<!--
- These days, its quite uncommon that users stay in one physical location all the time. They go
to visit customers/providers, work from home and need to participate in the occasional off-site

- While some of they may be able to survive on a tablet, most will need a laptop. Now you have to
manage twice the amount of computers and the wins of VDI get a lot smaller if not nullified

- Requires a decent network connection between the client and virtual desktop server. Especially
crucial is latency: the experience quickly becomes painful with just a little bit of input lag

- The biggest user critique against VDI is the experience: if the network is not great, things feel
sluggish. This somewhat mitigates the "work from anywhere" argument

- While being quite common to combine BYOD and VDI client apps, it may not be desirable from a
security perspective. The org has no or very limited control of the user's endpoint device. While
sensitive data may "only be streamed" to the client and not stored on the user's personal device,
security critical information such as passwords or other credentials are still inputted using the
user's keyboard. In practice, devices that run VDI clients must be trusted

- When the VDI solution fails, it often prevents a lot of people to work at the same time. While
users are typically very dependent on shared services such as email or internal file sharing, at
least some tasks may be available if these are unavailable. If VDI is inaccessible and a
requirement, productivity will likely be severely lowered (especially if thin clients are used)
-->
