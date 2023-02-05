---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
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
```ruby
$ cat Vagrantfile 

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.synced_folder ".", "/vagrant_data"

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

For production VMs, try [HashiCorp Packer](https://developer.hashicorp.com/packer).

![bg right:30%](images/23-negative.jpg)
