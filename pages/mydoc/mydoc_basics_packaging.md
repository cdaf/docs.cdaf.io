---
title: Packaging
tags: [getting_started, tasks]
keywords: artefact, artifact, package, zip, gzip, tar, base64
last_updated: March 3, 2022
summary: Artefact retention within release package.
sidebar: mydoc_sidebar
permalink: mydoc_basics_packaging.html
folder: mydoc
simple_map: true
map_name: usermap
box_number: 3
folder: mydoc
---

# Build-Once/Deploy-Many

An objective of Continuous Delivery is to have a predictable, repeatable, deployment process. A fundamental principle of CDAF to achieve this producing an immutable release package. This decouples the deployment process from the source management process. The release package is a self-contained deployment asset, and should be executable anywhere, i.e. on the automation developers desktop, within the pipeline or even manually file transferred to a remote server.

## Artefact Retention

In the [Configuration Management][mydoc_basics_configuration_management] step, a default release package was created which contained properties files. The following step defines the solution specific artefacts which need to be available at deploy time. These are typically compiled binaries, but can be any set of files and/or directories.

Retain the output from the previous [build task][mydoc_basics_build_tasks].

### Linux

``` bash
echo 'output' > .cdaf/storeForLocal
```

### Windows

``` powershell
Set-Content .\.cdaf\storeForLocal 'output'
```

## Continuous Delivery Emulation (CD)

Retest your solution

    cdEmulate.sh

or for windows

    cdEmulate

Inspect the directory `TasksLocal`, and will now contain the `output` directory produced by the [build task][mydoc_basics_build_tasks]. Test the artefact

### Linux

``` bash
./TasksLocal/output/runtime.sh
```

### Windows

``` powershell
.\TasksLocal\output\runtime.ps1
```

This should output the following:

```
Deploy %integer%, property set to : %property%
```

## Other File Locations

There are three artefact definitions file names, depending on context, local, remote or both:

- storeFor
- storeForLocal
- storeForRemote

Other directories within your solution directory which will also be automatically included in the root of your deployment directory. Based on the suffix these will be placed in a local context, remote context or both. See the following sections for how these contexts differ.

- crypt
- cryptLocal
- cryptRemote
- custom
- customLocal
- customRemote

An explanation of the local and container extensions will be explained in following sections.

> Next: [Local Tasks][mydoc_basics_local_tasks]

{% include links.html %}
