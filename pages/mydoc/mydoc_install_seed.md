---
title: Seed Solution
tags: [getting_started]
keywords: linux, bash, windows, powershell, cmd, command
summary: "Preparing a new Solution for CDAF"
sidebar: mydoc_sidebar
permalink: mydoc_install_seed.html
folder: mydoc
---

With install for [Windows][mydoc_install_cdaf_on_windows] or [Linux][mydoc_install_cdaf_on_linux] complete, a new solution can be executed.

A key principle of the Continuous Delivery Automation Framework is loose coupling. This gives the automation developer the  ability to run the automation process on their workstation, well before executing in the pipeline tooling. This principle should be retained where possible so that troubleshooting and feature development can be be bought closer to the developer.

> a loosely coupled solution can allow migrating from one pipeline tool to another with minimal effort.

## Seed your solution

To seed a new solution, the minimal requirement is a directory with a solution file CDAF.solution

    mkdir .cdaf
    cp ~/automation/solution/CDAF.solution .cdaf

### Continuous Integration (CI)

With CDAF installed on your path, you can now test the solution by running linux

    ci.sh

or for windows

    ci

Many things will happen, however the key observation is that a file called release.sh for linux or release.ps1 for windows will be produced, this is the build artefact that can be consumed by the Continuous Delivery (CD) stages. 

### Continuous Delivery (CD)

Run the artefact with an example environment, for linux

    ./release.sh TEST

or windows

    ./release.ps1 TEST

Again many things will happen, but because we have not defined any deployment tasks, it will simply report "no action taken".

### CDAF Entry

The default CDAF entry point can conditionally execute the CI & CD steps, i.e. both for feature branches but CI only for the default branch. For linux

    entry.sh

or windows

    entry

You will the same steps executed above, but with a wrapper, it is this wrapper that will be used to loosely couple your solution to you chosen CI/CD toolset.

## Shift-Left & Fail-Fast

Now that you have the bare minimum, appply it to your CI/CD toolset immediately. We want to have a green pipeline from the start to trap any problems we may introduce in subsequent steps

> TODO: guidance on samples

> Next: CDAF [basics, build task][mydoc_basics_build_tasks]

{% include links.html %}
