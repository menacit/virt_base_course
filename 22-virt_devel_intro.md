---
SPDX-FileCopyrightText: © 2026 Menacit AB <foss@menacit.se>
SPDX-License-Identifier: CC-BY-SA-4.0

title: "Virtualisation course: Introduction to virtual development"
author: "Joel Rangsmo <joel@menacit.se>"
footer: "© Course authors (CC BY-SA 4.0)"
description: "Examples of how virtualisation can help devops teams be more effective"
keywords:
  - "virtualisation"
  - "introduction"
  - "vm"
  - "os"
  - "container"
  - "devops"
color: "#ffffff"
class:
  - "invert"
style: |
  section.center {
    text-align: center;
  }

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pelle Sten (CC BY 2.0)" -->
# Virtualised development
### Tackling development and deployment

![bg right:30%](images/22-abandoned_office.jpg)

<!--
- We've touched on this, especially related virtual appliances

- Let's dig a bit deeper to understand what the problem really is
-->

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Martin Fisch (CC BY 2.0)" -->
In theory, collaborative development and
testing of software shouldn't be that hard.  

We got interpreted languages and
great tools like GitHub to help us.

Shouldn't be so hard, right?

![bg right:30%](images/22-bees.jpg)

---
### app.py
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
```
$ flask run

* Environment: production
* Debug mode: off
* Running on http://127.0.0.1:5000
```

```
$ curl http://localhost:5000/api/request_info | jq

{
  "browser": "curl/7.81.0",
  "ip_address": "127.0.0.1"
}
```

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Joel Rangsmo (CC BY-SA 4.0)" -->
Let's put it in a shared Git repository,
provide a download link for customers
and get filthy rich!

![bg right:30%](images/22-metal_kid_kicking_statue.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Scott Skippy (CC BY-SA 2.0)" -->
What dependencies (and versions) are
installed on developers' workstations?  
  
How about in the different server environments,
such as staging and production?
  
What about other components in the stack?
(OS, load balancer, databases, etc.)

![bg right:30%](images/22-dice.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Qubodup (CC BY 2.0)" -->
```
$ cat requirements.txt

Flask==2.0.3
```

```
$ python3 -m venv my_env
$ ls my_env

bin include lib64 lib app.py
pyvenv.cfg requirements.txt

$ my_env/bin/pip install -r requirements.txt

Successfully installed Flask-2.0.3

$ my_env/bin/flask run

* Environment: production
* Running on http://127.0.0.1:5000
```

![bg right:30%](images/22-glitch_globe.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Martin Fisch (CC BY 2.0)" -->
## Some problems
- Code may not behave exactly on all platforms
- Only handles Python dependencies\*
- Doesn't describe how stack should be run

![bg right:30%](images/22-albatross.jpg)

---
<!-- _footer: "%ATTRIBUTION_PREFIX% Pelle Sten (CC BY 2.0)" -->
Is all doom and gloom?  

Let's explore some tools that tries
to help us with these challenges!

![bg right:30%](images/22-abandoned_office.jpg)
