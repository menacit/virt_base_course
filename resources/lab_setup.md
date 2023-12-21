<!--
SPDX-FileCopyrightText: © 2023 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0
X-Context: Virtualisation course - Lab setup guidance
-->

# Virtualisation course: Lab setup

## Introduction
This documentation describes the required steps and guidance for setting up a lab environment for
Menacit's introductory virtualisation course. Ensure to read it carefully before requesting
assistance from the course teacher(s).


## Required steps

### Downloading Ubuntu ISO
The lab environment has been designed and tested on Ubuntu Server 22.04.
Navigate to the [official Ubuntu download web page](https://ubuntu.com/download/server) and
select the "Download Ubuntu Server 22.04.3 LTS" option. This should trigger the download of an
installation image ("ubuntu-22.04.3-live-server-amd64.iso").


### Installing compatible VMM
During the course, the student is expected to create/configure virtual machines both manually and
utilizing automation tools, such as ["HashiCorp Vagrant"](https://www.vagrantup.com/).  
  
The course can be completed using any virtual machine manager/hypervisor
[supported by Vagrant](https://developer.hashicorp.com/vagrant/docs/providers). Historically, most
students have opted to utilize [Oracle's "VirtualBox"](https://www.virtualbox.org/wiki/Downloads),
which integrates well with Vagrant and can operate on Windows, Linux and macOS. If VirtualBox is
chosen, make sure to only download the open-source version and avoid the "Extension Package".

Users of macOS on modern Apple hardware who experience problems with VirtualBox may prefer to use
[VMware Fusion](https://www.vmware.com/products/fusion.html). For more information, see the
["vmware" provider documentation](https://developer.hashicorp.com/vagrant/docs/providers/vmware).


### Creating lab VM
In your VMM, create a new virtual machine and specify the downloaded Ubuntu Server ISO as the
installation medium.

Ensure that the VM is created with the following minimum specification:
- 20 GB of disk space
- 3 GB of RAM/memory
- 2 CPU cores

During the operating system installation process, choose default options. When presented with the
option to install additional software, make sure that "docker" is **not** selected.

In order to verify your installation, open a console/virtual display to the VM, login and execute
the following command:

```
$ ping -c 3 one.one.one.one && cat /etc/lsb-release
```

If the VM is properly setup and configured, the command above should successfully connect to a
remote host (verifying a working Internet connection) and include "DISTRIB\_RELEASE=22.04" in its
output.


### Installing Docker in VM
The containerisation software "Docker" is utilized during the course labs and must be installed on
the Ubuntu Server VM created during the previous step. There are several options available to
install Docker and its required dependencies, but the only one tested for course labs is the
[official "repository" installation method](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository).

Once installed, issue the following commands to configure permissions and verify that the system
has been setup correctly:

```
$ sudo usermod -a -G docker ${USER}
$ newgrp
$ docker run hello-world
```

If the student is experiencing permission issues with Docker, reboot the virtual machine and
try again.


### Installing Vagrant on host
On the student's host computer (physical computer with a virtual machine manager installed),
[download and install](https://developer.hashicorp.com/vagrant/docs/installation) the VM automation
software ["HashiCorp Vagrant"](https://www.vagrantup.com/).  

In order to verify the installation, open a terminal ("PowerShell" on Microsoft Windows) and
execute the following commands:

```
$ mkdir vtest; cd vtest
$ vagrant init ubuntu/jammy64
$ vagrant up
$ vagrant ssh
```

If successfully executed, the student should be presented with a shell prompt in a new VM.


## Troubleshooting guidance

### Enabling virtualisation support
Virtualisation software like VirtualBox relies on hardware features included in most processors.
These features are typically enabled by default, but some computer manufacturers require that they
are explicitly enabled.  
  
If the student is experiencing issues creating virtual machines, review "step one" and "step two"
in [Microsoft's virtualisation support documentation](https://support.microsoft.com/en-us/windows/enable-virtualization-on-windows-11-pcs-c5578302-6e43-4b4b-a449-8ced115f58e1).


### "Incompatible character encodings"
Vagrant doesn't handle file system paths well with non-ASCII character/mixed character encoding.  
Users who encounter error messages such as "join: incompatible character encodings: CP850 and..."
have two options: create a new user account/file system path containing only ASCII characters (A-Z)
or reconfigure the Vagrant path settings, as documented below.  
  
On Windows, start a command prompt **as administrator** (right click "Run as administrator") and
execute the following commands:

```
$ md "C:\vagrant_data"
$ setx VAGRANT_HOME "C:/vagrant_data"
$ setx GEM_HOME "C:/vagrant_data"
$ takeown /a /r /f "C:\vagrant_data"
$ "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" setproperty machinefolder "C:\vagrant_data"
```

Copy the "resources" directory into "C:\\vagrant\_data" and re-execute "vagrant up".
