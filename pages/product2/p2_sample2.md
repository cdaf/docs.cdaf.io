---
title: Vagrant on Linux
keywords: sample
summary: Vagrant with Oracle VirtualBox
sidebar: product2_sidebar
permalink: p2_sample2.html
---

# Vagrant

CDAF Vagrant boxes support VirtualBox.

    curl -s https://raw.githubusercontent.com/cdaf/linux/master/install.sh | bash -
    ./automation/provisioning/base.sh vagrant

## VirtualBox

Oracle VirtualBox

    ./automation/provisioning/base.sh virtualbox

### Create Desktop Build Server

sudo apt-get -y install vagrant virtualbox


To create a desktop environment, navigate to the solution root and run:

    vagrant up

### Continuous Delivery Testing

Once the environment is running access the build server an execute the CD emulation. Note: On a Windows host bash tools are recommended to provide native SSH access.

    vagrant ssh build
    cd /vagrant
    ./automation/cdEmulate.sh

### Clean-up and Destroy

If change made that need to be checked in, clean the workspace:

    .\automation\cdEmulate.sh clean

Once finished with the environment, destroy using:

    vagrant destroy -f

{% include links.html %}
