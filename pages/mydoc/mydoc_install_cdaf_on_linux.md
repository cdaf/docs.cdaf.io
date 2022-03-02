---
title: Install CDAF on Linux
tags: [getting_started, troubleshooting]
keywords: linux, bash
summary: "Install CDAF to user home"
sidebar: mydoc_sidebar
permalink: mydoc_install_cdaf_on_linux.html
folder: mydoc
---

To install for the local user, recommend placing in your home directory

``` bash
cd $HOME
curl -s https://cdaf.io/static/app/downloads/cdaf.sh | bash -
./automation/provisioning/addPath.sh "$(pwd)/automation"
```

Exit your session and re-open to reload the path.

> Next: [seed your solution][mydoc_install_seed]

{% include links.html %}
