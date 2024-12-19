---
SPDX-FileCopyrightText: © 2024 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Vagrant demo"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Demonstration of Vagrant for virtualised development"
keywords:
  - "virtualisation"
  - "vagrant"
  - "demo"
  - "demonstration"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% NASA/JPL-Caltech (CC BY 2.0)" -->
# Vagrant demonstration
### Shareable development environments

![bg right:30%](images/23-retro_space.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% NASA/JPL-Caltech (CC BY 2.0)" -->
## What is HashiCorp Vagrant?
Software for automating the process of
setting up test/development environments
using virtual machines.

Released back in 2010
by Mitchell Hashimoto.

![bg right:30%](images/23-retro_space.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% NASA/JPL-Caltech (CC BY 2.0)" -->
## How does it work?
Instructions for how a VM should be
configured are defined as code in
shareable "Vagrantfiles". 

"Boxes" are pre-configured OS images
that can be uploaded/downloaded from
a remote repository, like "Vagrant Cloud".

Relies on a "provider", like VirtualBox
or VMware Fusion, for the heavy lifting.

![bg right:30%](images/23-retro_space.jpg)

---
```ruby
$ cat Vagrantfile 

Vagrant.configure("2") do |config|
  # Pre-built OS image used as base for guest
  # downloaded from a remote registry
  config.vm.box = "ubuntu/bionic64"

  # Directory shared between host and guest
  config.vm.synced_folder "./code", "/vagrant_data"

  # Commands to run after spawning guest
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y python3 python3-pip
    pip3 install -r /vagrant_data/requirements.txt
  SHELL
end
```

---
```
$ vagrant validate
Vagrantfile validated successfully.

$ vagrant up

Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'ubuntu/bionic64'...
==> default: Forwarding ports...
==> default: Waiting for machine to boot.
==> default: Running provisioner: shell...
[...]
Done
```

---
```
$ vagrant ssh

vagrant@ubuntu-bionic:~$ cd /vagrant_data/
vagrant@ubuntu-bionic:/vagrant_data$ flask run

* Environment: production
* Debug mode: off
* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

```
$ vagrant destroy --force
==> default: Forcing shutdown of VM...
==> default: Destroying VM...
```

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Fritzchens Fritz (CC0 1.0)" -->
## Other neat things
Multiple VMs can be configured and
launched using a single Vagrantfile.  

"Vagrant Share" plugin enables you
to easily provide remote access
to a guest for collaboration.

For building production OS images,
try [HashiCorp Packer](https://developer.hashicorp.com/packer).

![bg right:30%](images/23-negative.jpg)
