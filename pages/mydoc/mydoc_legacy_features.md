---
title: Legacy Features
keywords: legacy, pki, aes, unpackaged
last_updated: Mar 5, 2022
summary: "Summary of features which are not planned for deprecation, but are not recommended for implemenation."
sidebar: mydoc_sidebar
permalink: mydoc_legacy_features.html
folder: mydoc
---

[Remote Tasks][mydoc_basics_remote_tasks]

An alternative is to use a PKI encrypted password, this requires pre-installation on the agent and only suitable for self-hosted agents. This is a complicated approach and not a recommended method.

```
context  target     deployHost            remoteUser           remotePass
remote   VAGRANT    windows-1.mshome.net  windows-1\adminuser  $env:CDAF_PS_USERPASS
```

{% include links.html %}
