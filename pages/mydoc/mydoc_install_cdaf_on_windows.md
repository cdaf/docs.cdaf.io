---
title: Install CDAF on Windows
permalink: mydoc_install_cdaf_on_windows.html
keywords: CDAF on windows, pc, powershell, cmd
summary: Install CDAF to user home
sidebar: mydoc_sidebar
folder: mydoc
---

To install for the local user, recommend placing in your home directory

``` powershell
 cd $HOME
. { iwr -useb https://cdaf.io/static/app/downloads/cdaf.ps1 } | iex
.\automation\provisioning\addPath.ps1 "$(pwd)\automation"
```

Exit your session and re-open to reload the path.

> Next: [seed your solution][mydoc_install_seed]

{% include links.html %}
