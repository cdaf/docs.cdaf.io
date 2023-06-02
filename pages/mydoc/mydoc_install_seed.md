---
title: Seed Solution
tags: [getting_started]
keywords: linux, bash, windows, powershell, cmd, command
summary: Preparing a new Solution for CDAF
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

### Linux

``` bash
echo "solutionName=mycoolproduct" > .cdaf/CDAF.solution
echo "artifactPrefix=0.1" >> .cdaf/CDAF.solution
```

### Windows

``` powershell
Set-Content .\.cdaf\CDAF.solution "solutionName=mycoolproduct"
Add-Content .\.cdaf\CDAF.solution "artifactPrefix=0.1"
```

The minimum properties are the name of your solution, and the versioning prefix. The resulting artefact will have the build number appended to the release package, e.g. the first build will be 0.1.1, then 0.1.2 and so on. See [packaging][mydoc_basics_packaging].

``` properties
solutionName=mycoolproduct
artifactPrefix=0.1
```

### Continuous Integration (CI)

With CDAF installed on your path, you can now test the solution by running linux

    ci.sh

or for windows

    ci

Many things will happen, however the key observation is that a file called release.sh for linux or release.ps1 for windows will be produced, this is the build artefact that can be consumed by the Continuous Delivery (CD) stages. 

## Shift-Left & Fail-Fast

Now that you have the bare minimum, apply it to your CI/CD toolset immediately. We want to have a green pipeline from the start to trap any problems we may introduce in subsequent steps

> Next: Install CDAF [to your pipeline][mydoc_install_pipeline]

{% include links.html %}
