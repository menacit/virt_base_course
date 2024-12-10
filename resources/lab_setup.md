<!--
SPDX-FileCopyrightText: © 2024 Menacit AB <foss@menacit.se>
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
This step is only required if the student is not running Ubuntu 24.04 on their physical machine.  
  
Navigate to the [official Ubuntu Server download web page](https://ubuntu.com/download/server)
and select "Download 24.04.1 LTS". This should trigger the download of an ISO formatted
installation image ("ubuntu-24.04.1-live-server-amd64.iso").


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
This step is only required if the student is not running Ubuntu 24.04 on their physical machine.  
  
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
remote host (verifying a working Internet connection) and include "DISTRIB\_RELEASE=24.04" in its
output.


### Installing Docker on Ubuntu
The containerisation software "Docker" is utilized during the course labs and must be installed in
the Ubuntu environment configured during the previous step. There are several options available to
install Docker and its required dependencies, but the only one tested for course labs is the
[official "repository" installation method](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository).

Once installed, issue the following commands to configure permissions and verify that the system
has been setup correctly:

```
$ sudo usermod -a -G docker ${USER}
$ newgrp docker
$ docker run hello-world
```

If executed successfully, the commands should produce output similar to the example below:

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c1ec31eb5944: Already exists 
Digest: sha256:305243c734571da2d100c8c8b3c3167a098cab6049c9a5b066b6021a60fcb966
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.
[...]
```

If the student is experiencing permission issues with Docker, reboot the Ubuntu environment and
try again.


### Installing Vagrant
On the student's host computer (physical computer with a virtual machine manager installed),
[download and install](https://developer.hashicorp.com/vagrant/docs/installation) the VM automation
software ["HashiCorp Vagrant"](https://www.vagrantup.com/).  

In order to verify the installation, open a terminal ("PowerShell" on Microsoft Windows) and
execute the following commands:

```
$ mkdir vtest; cd vtest
$ vagrant init bento/ubuntu-24.04
$ vagrant up
$ vagrant ssh
```

If successfully executed, the student should be presented with a shell prompt in a new VM.  
If the setup process hangs for an excessive amount of time or exits with an error during execution
of the "vagrant up" command, open the virtual display/console for the newly created VM in your VMM
("Show" when selecting the guest in VirtualBox GUI, for example) to investigate its boot logs.
  
Once the verification process has been completed successfully, exit the guest shell prompt and
execute "vagrant destroy" to delete the test VM.


## Troubleshooting guidance

### Problems starting/destroying Vagrant VM
When executing Vagrant commands, the student may encounter error messages containing the following
string:

```
A Vagrant environment or target machine is required to this command.
```

This typically occurs when the command is not executed in the correct
directory. Before issuing any Vagrant commands, ensure that the current working directory is the
same as the "Vagrantfile" was created in:

```
$ cd /path/to/vtest && ls Vagrantfile
```

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


### "Permission denied" when using Gitbash
On a Windows system, Vagrant commands should not be executed in a "Gitbash" shell as it has known
compatibility issues, especially related to SSH authentication to the guest VM. If possible,
utilize a PowerShell prompt or the ["Windows Terminal" app](https://aka.ms/terminal) instead.
