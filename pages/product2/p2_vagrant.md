---
title: Vagrant Atlas
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_vagrant.html
---

## Vagrant Boxes

Vagrant box images available here [https://app.vagrantup.com/cdaf](https://app.vagrantup.com/cdaf) are build initially for Hyper-V using AtlasBase.ps1. This is cloned in VirtualBox and then both images are prepared using AtlasImage.ps1. Finally the images are packaged on the Hyper-V and VirtualBox hosts using AtlasPackage.ps1. The resulting .box files are uploaded to Vagrantup.

### Related Material

The following links have contributed to the construction of the Atlas scripts

 * https://www.vagrantup.com/docs/virtualbox/boxes.html
 * http://www.hurryupandwait.io/blog/in-search-of-a-light-weight-windows-vagrant-box
 * http://huestones.co.uk/node/305
 * https://stackoverflow.com/questions/39469452/installing-removed-windows-features/46985832#46985832

{% include links.html %}
