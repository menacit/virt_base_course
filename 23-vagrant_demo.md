---
SPDX-FileCopyrightText: © 2026 Menacit AB <foss@menacit.se>
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

Minimizes the need for repetitive and
error-prone manual configuration - yay!

Tries to ensures that all developers and
testers have a similar environment.

Released in 2010 by Mitchell Hashimoto.

![bg right:30%](images/23-retro_space.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Stig Nygaard (CC BY 2.0)" -->
## How does it work?
Instructions for how a VM should be
configured is defined as code in a
sharable "Vagrantfile", which is
typically stored alongside your
app's code in Git or similar.

These build upon "boxes", which are
pre-configured OS images that can
be downloaded from a remote
repository, like "Vagrant Cloud".

Relies on a "provider", like VirtualBox
or VMware Fusion, for the heavy lifting.

![bg right:30%](images/23-glowing_fish.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Halfrain (CC BY-SA 2.0)" -->
Let's try it out, shall we?

![bg right:30%](images/23-red_windows.jpg)

---
### kool\_app/app.py
```python
from flask import Flask, request

app = Flask("kool_app")

@app.route("/api/request_info")
def request_information():
    return {
        "ip_address": request.remote_addr,
        "browser": request.headers["User-Agent"]}
```

---
```ruby
$ cd kool_app
$ cat Vagrantfile 

Vagrant.configure("2") do |config|
  # Pre-built OS image used as base for guest,
  # downloaded from a remote registry
  config.vm.box = "ubuntu/bionic64"

  # Directory shared between host and guest
  # that contains the application's code
  config.vm.synced_folder "./code", "/shared_data"

  # Commands to run after spawning guest for setup
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y python3 python3-pip
    pip3 install -r /shared_data/requirements.txt
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
<!-- _footer: "%ATTRIBUTION_PREFIX% Halfrain (CC BY-SA 2.0)" -->
## What just happened?

![bg right:30%](images/23-tripple_exposure_road.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Fritzchens Fritz (CC0 1.0)" -->
## Other neat things
Setup port forwarding rules that
enables host to access network
services running in the guest.

Files edited/added by the host in
the shared directory are instantly
updated in the guest (and vice versa).

Multiple VMs can be configured and
launched using a single Vagrantfile,
great for testing complex cluster
setups and similar!

![bg right:30%](images/23-negative.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Matthias Ripp (CC BY 2.0)" -->
## Wrapping up
Vagrant is a useful tool for testing
and development, but it is a bit buggy -
beware of sharp edges and RTFM!

For building production OS images,
checkout [HashiCorp Packer](https://developer.hashicorp.com/packer).

Any questions, perhaps?

![bg right:30%](images/23-regensburg.jpg)
