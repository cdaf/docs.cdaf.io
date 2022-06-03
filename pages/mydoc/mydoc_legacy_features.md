---
title: Legacy Features
tags: [feature_configuration, tasks]
keywords: local testing, loop-back, loop back
last_updated: May 4, 2022
summary: Supported features of CDAF, whos use is discouraged
sidebar: mydoc_sidebar
permalink: mydoc_legacy_features.html
folder: mydoc
---

## Desktop Testing

Continuous delivery emulation on a single host can be performed with, or without, windows containers (docker/docker-compose).

### Native (without containers)

This approach uses the local host for both target (CD) and build (CI) execution. Provision the host with both roles

    .\automation\provisioning\mkdir.ps1 C:\deploy
    .\automation\provisioning\CredSSP.ps1 server

    .\automation\provisioning\trustedHosts.ps1 *
    .\automation\provisioning\CredSSP.ps1 client

{% include links.html %}
