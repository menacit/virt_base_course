<!--
SPDX-FileCopyrightText: © 2023 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0
X-Context: Virtualisation course - Lab
-->

# Virtualisation course - Lab exercise

## Scenario description
Naming products \*-fy is soooo 2015. Regardless, that is exactly what Examplify Inc. did with their
new drink recipe service "Mixologyfy". Both users and investors seems to love it, but the DevOps
team is struggling to collaborate on the code and get it running consistently in production.
The current situation is really impeding velocity and needs to be improved quickly to avoid an
upcoming catastrophic halt.  

In the interview you boldly claimed that this was your area of expertise, didn't you?
Let's put it to the test and save the company!


## Learning objectives
Practical knowledge of using Vagrant and Docker for bundling applications and their dependencies.


## Lab overview
The lab consist of an example Python web application called "mixologyfy.py".
It's a simple application that downloads and presents the
["IBA official cocktails" list](https://en.wikipedia.org/wiki/List_of_IBA_official_cocktails).
Besides reviewing the drink recipes, users of the web application can add cocktails to favorites,
granted that the application is running with "database mode" enabled.  

![Reference screenshot of lab web application](reference_screenshot.png)

The Python script is available in the directory "app-src" ("resources/lab/app-src" to be specific)
alongside a template file called "index.html.jinja", which contains the web application's HTML code
with embedded scripts written in the
["Jinja" template language](https://jinja.palletsprojects.com/en/3.1.x/templates/) to provide
dynamic responses.
  
In order to complete the lab, the student should package the application dependencies and run it
using [HashiCorp Vagrant](https://www.vagrantup.com/) and/or
[Docker Compose](https://docs.docker.com/compose/).

All tools required to complete the assignment should be pre-installed on the student's lab system,
granted that it has been configured in accordance with instructions documented in the file
"resources/lab_setup.md".
  
The "mixologyfy.py" script may **not** be modified during the lab completion process.


## Tasks

### Mandatory ("G")
The following tasks should be executed on the student's physical machine:
- Create/Initialize a Vagrantfile that uses the official AlmaLinux version 9 box
- Utilize a synced folder in Vagrant to share "app-src" directory with guest at the path "/app"
- Utilize a Vagrant provisioner to automatically install the lab application dependencies:
  - ["FIGlet" executable/package](http://www.figlet.org/)
  - Python 3 libraries/modules and their dependencies:
    - Flask version 2 or later
    - psycopg version 3 or later
    - requests version 2 or later

- Utilize a Vagrant forwarded port to expose port 1338/TCP in guest on host port 1337/TCP
- Verify that setup works as intended by executing the following validation steps:
  - Execute "vagrant ssh -c 'python3 /app/mixologyfy.py' " on the host to start the lab application
  - Open a web browser on the host and access the lab web application at "http://localhost:1337/"
  - Modify something in the HTML template file ("app-src/index.html.jinja") via the host system
  - Refresh the lab web application in the host web browser and observe the template modification


### Meritorious ("VG")
The following tasks should be executed in the student's Ubuntu environment (physical or virtual):
- Create Dockerfile based on Alpine Linux version 3.21.0 for lab application and its dependencies:
  - ["FIGlet" executable/package](http://www.figlet.org/)
  - Python 3 libraries/modules and their dependencies:
    - Flask version 3.0.0
    - psycopg version 3.1.16
    - requests version 2.29.0

- Build image from the Dockerfile and execute the container using "docker run" command:
  - Utilize the "publish" feature to expose guest port 1338/TCP to port 1339/TCP on the Ubuntu VM

- Create a Docker Compose file (version 3.8) to setup lab application and associated database:
  - Utilize "build" feature to automatically build image using Dockerfile for lab application
  - Utilize the "ports" feature to expose guest port 1338/TCP to port 1339/TCP on the Ubuntu VM
  - Add secondary container/service running PostgreSQL version 15.5 to serve as a database
  - Utilize a "volume" to ensure that database data is stored persistently
  - Configure lab application to utilize the PostgreSQL database using environment variables
  - Utilize health checks and "depends\_on" to define startup order of containers/services

- Verify that setup works as intended by executing the following validation steps:
  - Execute "docker compose up --build" command on the Ubuntu VM to start the lab application
  - Open a web browser on the host and access the lab application at "http://<UBUNTU\_IP>:1339/"
  - Add a drink recipe to favorites by clicking an "Add to favorites!" link
  - Ensure that "Number of favorites" on web page has been incremented by one
  

### Bonus (just for fun!)
- Utilize the "secrets" feature to avoid storing clear-text credentials in the Docker Compose file
- Add additional service/container to Compose file that performs recurring backups of database
- Publish/Share a modified version of the application as a container on a remote image repository


## Lab report/documentation
Each student should submit a lab report containing **at least** the following information ("G"):
- Documentation of how each task was performed, including reasoning behind solution
- Screenshots as proof of lab web application being accessible from web browser on the host system
  - "**G**": Before applying modifications to HTML template file 
  - "**G**": After applying modifications to HTML template file
  - "**VG**": Usage of the "Add to favorites!" functionality  
  
The lab report should be provided as a plain text file (".txt"), Markdown document or PDF file.
In addition to the report, all lab files that have been changed/created (configuration sets,
Dockerfiles, scripts, screenshots, etc.) should be provided as a ZIP or GZIP archive.  
  
Upload lab report and archive of changed files to
%REPORT_TARGET%.


## Guidance and resources

### Avoid screenshots of text
During a debugging session or lab guidance with the course teacher, avoid taking screenshots of
text error messages/output whenever possible. Instead, utilize the copy-paste feature to extract
and send the relevant output/error messages.


### Verifying setup of lab system
Before starting with the lab tasks, the student should ensure their computer ("the lab system") has
been setup and configured properly. The file "resources/lab\_setup.md" included in the course
resource archive describes the configuration prerequisites and steps to validate them.


### Application sources and repositories
Not all applications and libraries are available for instant installation using a Linux
distribution's standard repositories/package management tools. Even if available, specific
required versions may not be.

Third-party/Non-standard sources like [EPEL](https://wiki.almalinux.org/repos/Extras.html),
[FlatHub](https://flathub.org/) and programming language-specific package repositories like
["PyPi" for Python](https://pypi.org/) are commonly used to install software dependencies.


### Enabling application debug logging
The lab application supports debug message logging by setting the environment variable
"APP\_DEBUG\_LOGGING" to "enabled". This may aid the process of understanding how the application
works and why potential problems occur.


### Reviewing application setting variables
Configuration options of the lab application, such as the HTML template file path, can be tweaked
by modifying/setting environment variables. For a complete list of options, review the initial
documentation/comment section in "mixologyfy.py".


### Vagrant and working directory
When running commands such as "vagrant up" or "vagrant ssh", it's important that the working
directory ("$PWD") is the same as the "Vagrantfile" is stored in. If the commands are not executed
in this directory, Vagrant won't know which specific box/environment the command refers to.


### Vagrantfile without file extension
A common issue when working with Vagrant is accidentally adding a file extension such as ".txt" to
the Vagrantfile, which will result in problems while running the application. To ensure that the
file name is correct, execute one of the following commands depending on operating system:

***Windows**:
```
$ type Vagrantfile
```

**Linux/macOS**:
```
$ cat Vagrantfile
```


### Re-provision Vagrant guest
When a Vagrant guest is first created (after execution of "vagrant up" command), any configured
provisioners (such as "shell") are executed. This process only happens during the initial boot.
If the Vagrantfile has been changed since its initial startup, it may be desirable to run the
following command to reload its configuration and forcefully execute provisioners:

```
$ vagrant reload --provision
```


### File paths in Docker containers
When referring to file paths in Docker files or runtime configuration for containers, keep in mind
that these are not the same as on the host system/Ubuntu VM. In order to access files from the
system running Docker, utilize the "COPY" directive during build-time or "bind volumes" during
run-time.


### File permissions for Docker volumes 
If the application in a Docker container is running as a non-root user and is trying to access a
file from a "bind volume", the file on the system running Docker must be readable by the UID of the
container user.


### Avoid usage of "docker-compose" command
Old documentation about how to utilize Docker Compose often refer to the command "docker-compose".
This is a legacy method of using the utility associated with several problems and should be avoided
in favor of the command "docker compose" (without dash separating the words). 


### Docker Compose and working directory
When running commands such as "docker compose up --build" or "docker compose rm", it's important
that the working directory ("$PWD") is the same as the "docker-compose.yml" is stored in.
If the commands are not executed in this directory, Docker won't know which specific Compose
environment the command refers to.


### Utilizing Compose to build images
Instead of manually building Docker images before executing "docker compose up", the "build" option
may be defined in the file "docker-compose.yml". If used, it's however important to ensure that the
"--build" flag is included when running "docker compose up" to ensure that the Dockerfile is
always checked for changes before execution.


### Hostname resolution in Compose
When specifying multiple containers/services in a Docker Compose file, the different
containers/services can utilize each others names to as network host names instead of specifying
IP addresses in configuration options. This means that a service called "web" can connect to the
database container "db" using the host name "db". For more information, see "Links" section below.


### Compose startup order and health checks
When running multiple containers/services that depend on each other, the order in which these are
started may become important. In order to ensure that the PostgreSQL database is started before
the lab web application, the Docker Compose feature "depends\_on", container health checks and a
utility like "pg\_isready" may be used. For more information, see "Links" section below.


### Validating compose file
Docker Compose declares its configuration in a file called "docker-compose.yml".
The [YAML format](https://en.wikipedia.org/wiki/YAML) used in the configuration file is notoriously
picky about indentation levels (tabs and spaces). In order to detect faulty syntax and formatting
issues, the "yamllint" program/command can be installed and utilized. A text editor that helps with
indentation is also highly recommended.


### "Errno -3: Try again!"
If the Mixologyfy Python script fails to start due to the database error "Errno -3: Try again!",
it means that the application couldn't resolve the hostname specified in the database URI.
Ensure that the correct hostname is used (matching the application container's name in the file
"docker-compose.yml") and that the correct environment variable name is used to specify the
database connection URI setting.


### Asking for assistance
In order to minimize repeated answers to recurring questions, several common issues are brought up
in the lab description (this README file). The teacher should also update the guidance section of
the lab description if such need arises during the course. Before requesting help/guidance from the
course leader, the student should utter the secret passphrase "Black ICE".


### Links
- [Wikipedia: "Environment variables"](https://en.wikipedia.org/wiki/Environment_variable)
- [G4G: Environment variables](https://www.geeksforgeeks.org/environment-variables-in-linux-unix/)
- [AlmaLinux Wiki: "Extra repositories"](https://wiki.almalinux.org/repos/Extras.html)
- [Vagrant CLI documentation](https://developer.hashicorp.com/vagrant/docs/cli)
- [Vagrant boxes repository](https://app.vagrantup.com/boxes/search)
- [Vagrant "shell" provisioner](https://developer.hashicorp.com/vagrant/docs/provisioning/shell)
- [Vagrant provider usage](https://developer.hashicorp.com/vagrant/docs/providers/basic_usage)
- [Vagrant "synced\_folders" feature](https://developer.hashicorp.com/vagrant/docs/synced-folders)
- [Vagrant port forwards](https://developer.hashicorp.com/vagrant/docs/networking/forwarded_ports)
- ["Dockerfile" reference documentation](https://docs.docker.com/engine/reference/builder/)
- ["docker run" reference documentation](https://docs.docker.com/engine/reference/commandline/run/)
- ["Compose" getting started guide](https://docs.docker.com/get-started/08_using_compose/)
- ["Compose" networking overview](https://docs.docker.com/compose/networking/)
- ["Compose" file V3 reference](https://docs.docker.com/compose/compose-file/compose-file-v3/)
- ["Compose": "depends\_on"](https://docs.docker.com/compose/compose-file/05-services/#depends_on)
- ["Compose": Health checks](https://docs.docker.com/compose/compose-file/05-services/#healthcheck) 
- ["Compose": Secrets](https://docs.docker.com/reference/compose-file/secrets/)
- [PostgreSQL image on Docker Hub](https://hub.docker.com/_/postgres/)
- [PGSQL connection URIs](https://www.prisma.io/dataguide/postgresql/short-guides/connection-uris)
- ["pg\_isready" documentation](https://www.postgresql.org/docs/current/app-pg-isready.html)
- [Psycopg installation guide](https://www.psycopg.org/psycopg3/docs/basic/install.html)
