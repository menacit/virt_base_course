---
SPDX-FileCopyrightText: © 2022 Menacit AB <foss@menacit.se>
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
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Pelle Sten (CC BY 2.0)" -->
# Virtualised development
### Why devops teams have grown to love it

![bg right:30%](images/22-abandoned_office.jpg)

<!--
- We've touched on this, especially related virtual appliances

- Let's dig a bit deeper to understand what the problem really is
-->

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Martin Fisch (CC BY 2.0)" -->
**In theory, collaborative development of software shouldn't be that hard.**

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
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Scott Skippy (CC BY-SA 2.0)" -->
What dependencies (and versions) are installed on developers workstations?  
  
How about in the different server environments?  
  
Who should deploy and manage the stack? (application, load balancer, databases, etc.)

![bg right:30%](images/22-dice.jpg)

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Qubodup (CC BY 2.0)" -->
```
$ cat requirements.txt

Flask==2.0.3
```

```
$ python3 -m venv .
$ ls

bin include lib64 lib app.py
pyvenv.cfg requirements.txt

$ bin/pip install -r requirements.txt

Successfully installed Flask-2.0.3

$ bin/flask run

* Environment: production
* Running on http://127.0.0.1:5000
```

![bg right:30%](images/22-glitch_globe.jpg)

---
<!-- _footer: "© Course authors (CC BY-SA 4.0) - Image: © Martin Fisch (CC BY 2.0)" -->
## Some problems
- Sharing venv's is not trivial
- Only handles Python dependencies\*
- Doesn't describe how stack should be run

![bg right:30%](images/22-albatross.jpg)
