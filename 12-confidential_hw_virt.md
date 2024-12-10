---
SPDX-FileCopyrightText: © 2024 Menacit AB <foss@menacit.se>
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
<!-- _footer: "%ATTRIBUTION_PREFIX% Nikki Tysoe (CC BY 2.0)" -->
# Confidential computing
### Making computers a bit more trustworthy

![bg right:30%](images/12-space_invander.jpg)

<!--
- Virtualisation is in general very beneficial for security, as we've discovered during the course

Segue: It does however have it's downsides and doesn't solve every problem...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Eric Chan (CC BY 2.0)" -->
Traditionally, we must trust the hypervisor and operators of underlying infrastructure.  

![bg right:30%](images/12-jellyfish.jpg)

<!--
- Guests depend the host's security, as it is in full control of their execution*

- The hypervisor can snoop on the guests' disks and memory. This could be used to steal sensitive
information such as credentials from memory and confidential databases from disk

- From the perspective of the guest, it is in general not possible to inspect the security of the
underlying hypervisor and it's supporting infrastructure. Instead, users are forced to more or less
trust the infrastructure operators

- This problem also exist for physical servers that are colocated in a third-party's data center
(which is the common thing these days as data centers are expensive facilities to own/operate), but
in many cases this requires physical access to the servers (which are usually in a "locked" rack or
cage). A malicious actor who have access to a hypervisor or the virtualisation control plane (think
vCenter or similar) usually has a far easier time gaining access to VMs

- Add brasklapp about the terrible state of BMCs/IPMI/HW management interfaces

Segue: So what can we do to limit trust in the operators of physical infrastructure?
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Eric Kilby (CC BY-SA 2.0)" -->
We can encrypt disks of instances, but with somewhat limited value.

![bg right:30%](images/12-sloth.jpg)

<!--
- Disk encryption can be used to protect data at rest

- If someone would walk away with the hypervisor or network storage appliance that the guest's
disk image is stored on, at least it would be encrypted

- Relevant as we don't necessarily know how the operator handles backups of data and
HW decommissioning/broken disks (perhaps they are sent to a third-party vendor?)

- Regardless the key needed to unlock the disk must be in memory of the guest that access the data

- Probably stored somehow as we want to be able to reboot servers without entering a password
or similar every time. Encrypted storage on servers, especially OS disks, is a bit of a mess

- If the decryption key for the data is available in the guest, chances are that the hypervisor
can access it as well - either through snooping of memory or by manipulating storage for the guest
operating system
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Jan Bommes (CC BY 2.0)" -->
Operators can build trust using transparency.  
  
Trust may not be enough due to regulatory requirements.  
  
Even if operators act in good faith and auditors are happy, things can still get owned.

![bg right:30%](images/12-broken_floor.jpg)

<!--
- Infrastructure operators, regardless if they are your company's IT department or a third-party
hosting provider, can do things to earn trust even tough we can't inspect security from the guest

- Allow independent auditors to inspect and test security controls/processes

- Not just technical things such as patch levels and network restrictions, but also physical
security, background checks of personnel and similar

- As a wise and pessimistic man once said: "trust is just a word for lacking security"

- Laws and industry compliance frameworks may prevent organisations from letting a third party
host/control their infrastructure even if they want to

- Even if operators are not actively malicious and auditors didn't find any obvious problems,
systems can still get hacked. New vulnerabilities and attack techniques are discovered every day
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Quinn Dombrowski (CC BY-SA 2.0)" -->
Currently, lots of interest (see "money") in solving these issues for cloud and edge computing.  
  
"Confidential computing" is the collective term used for attempted solutions.

![bg right:30%](images/12-switches.jpg)

<!--
- Many different organisations would like to solve the problem that sounds a bit like a pipe-dream:
not having to trust the computer your software (in this case VM) is running on

- Organisations doesn't necessarily have the skills, resources or interest in operating their own
infrastructure

- Many would like to a cloud provider, but don't feel comfortable giving away access to their data

- Cloud providers would very much like to take these peoples' money

- Large and security concious organisations would like to save money by using internally pooled
virtual infrastructure, but have some many different security requirements that it is hard to do so

- Growing interest in edge computing (https://en.wikipedia.org/wiki/Edge_computing), which often
means that servers will move from relatively safe data centers (from a physical perspective) to
small service lockers next to the highway or in the forest. It may be tricky to prevent malicious
actors from physically gaining access to the HW in these cases

- Would likely also be way to expensive for everyone with "edge needs" to own their own
geographically spread out infrastructure. Sharing will be necessary if not only the biggest players
wanna utilize it.
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Sergei F (CC BY 2.0)" -->
## Memory encryption
- Prevent host (and other guests) from peaking at/modifying VM memory
- Guests are still vulnerable against many different types of attacks
- AMD SEV\* is an example of a solution

![bg right:30%](images/12-rusty_lock.jpg)

<!--
- OT intro: The benefits of disk encryption is widely understood, but many don't know that keys
stored in RAM can often be extracted using so called "cold boot attacks"
(https://en.wikipedia.org/wiki/Cold_boot_attack) or similar methods

- Data is typically stored unencrypted in RAM (or otherwise the keys to decrypt it are stored in
RAM next to it), which means that an attacker with physical access to RAM may be able to extract it

- This is obviously bad if someone gains physical access to the hypervisor, but the hypervisor can
as previously mentioned most often snoop on the memory of guests and even manipulate it

- Processor/chipset vendors started introducing features that encrypt all data stored in RAM with
a random key generated per boot by the CPU (in which the key is, supposedly securely, stored)

- Initially, the goal was to prevent against physical attacks as described above, but new features
were added that generated a random encryption key per guest (or rather the area of memory dedicated
to each guest), which in theory would prevent the hypervisor (and other guests which may have been
able to escape/breakout) from peeking at it

- Hypervisor can still modify executable files on the guest disk or use a number of other
techniques to gain access, which makes the memory encryption a bit irrelevant

- AMD's naming scheme is a mess, see https://developer.amd.com/sev/

Segue: The dream lives on and since then new features have been introduced which tries to address
some of these vulnerabilities/attacks...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Lydur Skulason (CC BY 2.0)" -->
## "Full guest isolation"
- Hardware and software features to prevent host from messing with guests
- Owner of guests verify runtime environment before starting/decrypting data
- Intel tries to solve this with [TDX](https://intel.github.io/ccc-linux-guest-hardening-docs/)
- AMD [SEV-SNP](https://developer.amd.com/sev/) is another solution

![bg right:30%](images/12-snow_dome.jpg)

<!--
- HW vendors switched focus from just memory encryption to a more holistic approach

- These features would not only prevent hypervisors from messing with guest memory, but also CPU
registers/state

- Mayhaps most importantly, they provide a method for guests to verify during startup that they
actually running in this encrypted/isolated environment

- Once the guest knows that the coast is clear, it can decrypt/process sensitive data

- Quite complicated how this works on a technical level and a bit out-of-scope for this course

Segue: This sounds wonderful and almost to good to be true...
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Fritzchens Fritz (CC0 1.0)" -->
## What's the catch?
- Still early days, lacking support in virtualisation software stack
- Current state of verified boot is quite bad, especially in Linux distributions
- Requires trust in a proprietary black box
- Several vulnerabilities have been identified, breaking the promise

![bg right:30%](images/12-broken_cpu.jpg)

<!--
- These HW features have just started getting upstream support in the Linux kernel and
virtualisation stack - will take a while before they are fully rolled out and stable

- Verified/attested boot chains, which seems to be requirement for guests to run without
trusting the host operating system, is far from problem free. The Linux implementations for secure
boot (which is one of the pieces) seems to be motivated by getting it run on all HW, not making
things actually more secure

- In practice, we are moving trust from the hypervisor (which is often based/running on FOSS and
auditable code) to CPUs running closed-source firmware with a bad track record

- These isolation technologies are not perfect and vulns have been discovered in them. Intel SGX,
which is a similar technology that has been on the market for quite some time, have had several
flaws that completely break the security promise

Segue: So, should we just give up on these technologies?
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Graham Drew (CC BY 2.0)" -->
Mayhaps a good complement to minimize risk, if understood properly.

If you find this interesting,
checkout [Joel's talk from SEC-T](https://youtu.be/vdj9Pr-6dq8).

![bg right:30%](images/12-sinking_boat.jpg)

<!--
- The security of a system should be multi-layered: technologies such as Intel TDX may be able to
stop an attacker that has managed to get a foothold on a hypervisor

- Everything that improves the overall security of a system should be considered, even if it's not
a silver bullet

- Perhaps it prevents companies from building business models based on snooping

- The main danger is the promise it makes and how people interpret that
-->
