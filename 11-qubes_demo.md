---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Qubes OS showcase"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Demonstration of Qubes OS and it's features"
keywords:
  - "virtualisation"
  - "vm"
  - "qubes"
  - "qubes-os"
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
<!-- _footer: "%ATTRIBUTION_PREFIX% Pedro Ribeiro Simões (CC BY 2.0)" -->
# Qubes OS showcase
### An alternative vision of the desktop

![bg right:30%](images/11-vr_woman.jpg)

<!--
- Qubes OS is a FOSS desktop operating system with focus on security

- Utilizes Xen virtualisation to provide security compartmentalisation (expl. will follow)

- Co-founded by security researcher Joanna Rutkowska

- Allegedly used by Edward Snowden and lots of other paranoid/security concious users, such as
Freedom of the press foundation, the Mullvad VPN company and the organisation running
"Let's Encrypt"

Segue: To demonstrate the OS, I've set it up on a laptop and taken some screenshots in action
-->

---
![bg center:100%](images/11-qubes_desktop_empty.jpg)

<!--
- What you're seeing is the default Qubes desktop when booted and logged in

- Not a pretty sight, made slightly worse by trying to increase font size for the demos

- Shipped with the XFCE (https://xfce.org/) WM, but also available with i3 (https://i3wm.org/)

Segue: Things look a bit more interesting with applications running...
-->

---
![bg center:100%](images/11-qubes_desktop_full.jpg)

<!--
- The screenshot is a bit messy and probably doesn't make a lot of sense right now

- Most important is to make note of the border color of the windows (red, grey, yellow and blue),
these let us know which "qube" (their terminology for a VM) the application is running in

- Each qube acts as a bit of a security boundry: The video player running in the "personal" qube
can't access files or processes running in the "work" qube

- The same is true for the "vault" cube which is provided to store very sensitive information in,
such as private keys and password databases. This qube is further restricted as it isn't even
provided with network access to minimize the risk for leaks

- Qubes shines in the way qubes are integrated with the desktop and each other

Segue: Lets clean up a bit and talk about how you use Qubes...
-->

---
![bg center:100%](images/11-qube_apps.jpg)

<!--
- Scrot shows the Qubes menu (a bit like the Windows start menu) 

- The list shows Qubes installed on the system and have sub-menus for starting applications in them

Segue: Let's start a file browser in the "work" qube...
-->

---
![bg center:100%](images/11-qube_open_disp_1.jpg)

<!--
- Qubes utilise snapshots and temporary VMs in some very neat ways

- If you have an untrusted/potentially malicious file, such as a document received via email or a
program downloaded from an suspicious site on the Internet, it can be a risky thing to open/run it

- The scrot shows a menu in the file manager that allows us to view the document in a
"disposableVM"
-->

---
![bg center:100%](images/11-qube_open_disp_2.jpg)

<!--
- Once selected, we get a status notification telling us a qube is started

- A fresh new VM is created (from a template) just for viewing this document, and it's quite fast
-->

---
![bg center:100%](images/11-qube_open_disp_3.jpg)

<!--
- Notice the border color (and title) of the document editor window, it's different from the file
browser in the "work" qube

- Even if the document contained malicious code, it would be restricted to data and processes
in the disposable qube (which is likely very little of interest)
-->

---
![bg center:100%](images/11-qube_open_disp_4.jpg)

<!--
- Once done reading the document and the window is closed, we get another notification that the
disposable qube is shut down

- It is not only shut down, but also deleted

- This enables us to feel quite comfortable that any malicious backdoors are also deleted
-->

---
![bg center:100%](images/11-qube_disp_apps.jpg)

<!--
- DisposableVMs are just like other Qubes, except that they are created (from a snapshot) on the
fly and destroyed once all running apps in has been closed

- Using a disposable qube for web browsing is quite a good practice for the reasons described in
the previous example

Segue: Qubes OS comes with a bunch of default qubes as we've seen, but you can easily create more
-->

---
![bg center:100%](images/11-qubes_menu.jpg)

<!--
- The "Qubes tools" section of the menu contains utilities for managing the system

- Lets select "Create Qubes VM"
-->

---
![bg center:100%](images/11-qube_create.jpg)

<!--
- Choose a name and a border color for the Qube: a qube per customer and/or project is a good thing

- We can also which template to use for the VM, Qubes OS comes with Debian and Fedora, Kali Linux
(https://www.kali.org/) can be installed as well (a good choice for penetration testers)
-->

---
![bg center:100%](images/11-qube_create_type.jpg)

<!--
- We can also select which type of qube to create

- "TemplateVM" is a qube which you can install software in, configure and use as the base for other
qubes/VMs

- "AppVM" provides a persistent home directory for the qube, but is otherwise cloned from a VM
each time it is started. If you want to install additional software or similar, these will likely
need to be added to the template VM it is based on instead

- "StandaloneVM" is also based on a template, but is once created fully persistent and can be
modified without performing changes to the template. A good choice if you need to setup some
complex software that you don't wanna include in your template VM, but it will consume more disk
space and be a bit slower to start than an "AppVM"

- "DisposableVM" is just what we talked about previously

Segue: Qubes OS provides some tools that help us the desktop without giving up on security
-->

---
![bg center:100%](images/11-qube_copy.jpg)

<!--
- A quite common need is the ability to copy files between VMs

- Qubes OS shows a dialog in the grey dom0 (administrative VM, basically not a regular qube, could
be considered "the host" to keep things simple) that tells us that VM X wants to copy a file to VM
Z, which prevents qubes from moving a round data without the user noticing
-->

---
![bg center:100%](images/11-qubes_clipboard.jpg)

<!--
- Another example is the Qubes clipboard, which controls which VMs can access copy/paste data

- This may seem silly, but the clipboard could contain sensitive information such as passwords
-->

---
![bg center:100%](images/11-qubes_device_redirect.jpg)

<!--
- The same goes for peripherals such as microphones, webcams and USB storage drives

- Sure, there are likely use-cases where you want VMs to access to them, but not all of them and
not all the time

- You probably want your work qube to access the webcam and microphone for meetings
-->

---
![bg center:100%](images/11-qubes_wlan_list.jpg)

<!--
- It may be a bit hard to see due to scaling issues, but the upper right menu bar contains a
notification area

- If we click on the red signal strength indicator, we see drop-down menu appear with a red border
containg network interfaces and visible WiFi networks

- The laptop's network interfaces are forwarded to a dedicated qube that provides networking for
other VMs (qube "sys-net" by default)

- It's actually the same for USB and other peripheral devices as we just saw (qube "sys-usb")

- Qubes OS does it this way to protect the system from attacks delivered via network and external
devices

- If for example firmware in the wireless card is compromised by an attacker on the same network,
the attacker's access is limited to the sys-net qube. The attacker would likely be able to
intercept network traffic, but not much more and the traffic from other qubes is hopefully
encrypted
-->

---
![bg center:100%](images/11-qubes_no_net.jpg)

<!--
- You can actually see this isolation by listing network interfaces in dom0, which has none besides
the loopback interface

Segue: We can take a look at how this is done by opening "Qubes manager" in the tools menu
-->

---
![bg center:100%](images/11-qubes_vm_list.jpg)

<!--
- This quite messy application shows us information about qubes configured on the system

Segue: It also allows us to edit their settings...
-->

---
![bg center:100%](images/11-qube_conf.jpg)

<!--
- The scrot shows the configuration windows for a qube

- Allows us to modify VM settings in a similar fashion to other VMMs
-->

---
![bg center:100%](images/11-qube_pci_conf.jpg)

<!--
- By clicking on the "Devices" menu, we can see PCI devices forwarded/dedicated to the qube

- The current example shows how the laptop's two USB controllers are dedicated to the "sys-usb"
qube, which we saw in a previous example

- Similar configuration exist for the networking VM which has a wired and wireless NIC forwarded

- You could forward other devices as well to qubes of your choice, such as a GPU or studio sound
card
-->

---
![bg center:100%](images/11-qube_fw_conf.jpg)

<!--
- The qube settings also allows us to configure network restrictions for the Qube

- This can of course be done in other ways inside the specific qubes, but it's quite neat to have
the firewall functionality so easily accessible

- Firewalling is actually by default done by a separate qube - you can have multiple of these,
some which are connected to VPN for example, forcing all qubes configured to use it through the
tunnel or proxy
-->

---
![bg center:100%](images/11-qvm_commands.jpg)

<!--
- If you fancy the terminal or want to automate things, everything showed in the demo and much more
can be done with CLI tools
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Eric Savage (CC BY-SA 2.0)" -->
## Not everything is awesome
- [Requires somewhat fancy HW](https://www.qubes-os.org/doc/system-requirements/)
- Quite a lot of overhead
- No 3D acceleration
- Lots to manage and keep updated
- Lacking support for new HW

![bg right:30%](images/11-malachite.jpg)

<!--
- While Qubes OS is really cool and I recommend everyone to try it, it's not problem free

- To run qubes smoothly, you need a somewhat beefy computer with CPU virtualisation features that
are not available on all consumer systems - check out their system requirements

- While working quite well, there is a lot of overhead with all qubes running - if the "system"
and "service" qubes are included, there were 12 different VMs running during my demo

- Especially RAM is a thing you'll need quite a lot of

- For security reasons and the way windows from different qubes are shown, there is not 3D or
hardware codec acceleration available. You can't really game or do things like CAD on Qubes unless
you forward a dedicated GPU to the qube (which is seldom completely trivial)

- Lot's of things to manage, including several templates that must be patched and maintained,
requires a bit of knowledge of the underlying technology

- Qubes dom0 kernel is based on a patched older version of Fedora, which means that it rarely has
good support for new hardware. If you are gonna use qubes, you have better chances with a device
that has a few years on it's neck

Segue: Even if you consider these problems deal-breakers or find it slightly too paranoid, there is
still a lot of things to learn and adopt from Qubes' design....
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Mathias Appel (CC0 1.0)" -->
## Get inspired
- Take a look at [Bromium/HP Wolf Security](https://www.bromium.com/)
- Use VM and snapshots for risky things
- Setup a router VM to force traffic through VPN
- Separate VM per customer/project for easy cleanup and leak prevention

![bg right:30%](images/11-red_panda.jpg)

<!--
- Bromium is a solution that tries to introduce micro-virtualisation for applications on Windows.
They got bought by HP a few years ago and they may have ruined it, but could be worth checking out

- Even if you don't use Qubes you can still have a snapshot'ed VM that can be considered disposable

- Why not do your web browsing in a VM that can be nuked and paved every day?

- If you don't want all your Internet traffic to pass through a VPN, why not setup a dedicated VM
for it? If you setup two VMs, one as a router/gateway and the other as a client to it, you can
restrict connections and minimize the risk for leaks

- Basically what the slide says
-->
