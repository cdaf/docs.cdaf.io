---
title: n-1 Image Policy
published: true
permalink: 2023-09-25-n-1-image-policy.html
summary: Docker & Vagrant Support Policy.
tags: [news]
---

CDAF Docker images and Vagrant Box support for Windows Server and Ubuntu from now will be limited to an n-1 approach. Older images will remain available but will not receive any further updates.

## Vagrant

For Vagrant https://app.vagrantup.com/cdaf, the following Boxes are deprecated.

- cdaf/CentOSLVM v2022.10.09
- cdaf/WindowsServer v2023.03.13
- cdaf/UbuntuLVM v2022.10.05

The following will be deprecated at the next Windows Server major release

- cdaf/WindowsServerCore
- cdaf/WindowsServerStandard

### VirtualBox 7

There are currently no plans to release VirtualBox 7 compatible images.

## Docker

For Docker https://hub.docker.com/u/cdaf, no public images have been deprecated as only private images were eligible for deprecation under this policy.

---

See [Paying Off Technical Debt Blog](https://blog.cdaf.io/articles/2023-07-06-tech-debt/)

{% include links.html %}
