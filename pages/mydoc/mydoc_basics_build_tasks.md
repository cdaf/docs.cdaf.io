---
title: Build Tasks
tags: [getting_started, tasks]
keywords: ci, build, maven, msbuild, dotnet, npm, pip, bundler, gradel, ant, make
last_updated: March 3, 2022
summary: The CI Task, i.e. creating artefacts from code.
sidebar: mydoc_sidebar
permalink: mydoc_basics_build_tasks.html
simple_map: true
map_name: usermap
box_number: 2
folder: mydoc
---

## Continuous Integration

Continuous Integration (CI) is the objective of bringing code branches together and building them to produce a consolidated artefact. This shift-left approach ensures the efforts of multiple contributors are combined and tested regularly. The testing within CI typically starts with unit testing, and that should be included in the build task. For some ecosystems this is an implicit or parameterised part of the build command, others, it's separate command.

### How does it work

CDAF will process all build.tsk files in the solution root, then all the build.tsk files found in one level of sub-directories.

The build.tsk files are processed line by line, each line is logged and then executed, with errors and exceptions trapped and logged. In the case of linux the error processing is based on the exit code and standard error, while windows has a broader range of errors, such as halt and exception conditions. 

For this material, the build output is a simple script, for some language specific examples see

- [ASP.NET Classic (MSBuild)](https://blog.cdaf.io/posts/2023-04-25-web-deploy/)
- [Java Maven](https://blog.cdaf.io/posts/2023-04-25-maven/)

## Extend the Seeded Solution

Based on the [configuration management][mydoc_basics_configuration_management], add a `build.tsk` file to the solution root.

### Linux

``` bash
echo 'echo \"hash!/usr/bin/env bash\" > runtime.sh' > build.tsk
echo 'echo \"echo Deploy %integer%, property set to : %property%\" >> runtime.sh' >> build.tsk
echo 'hash=$(printf \"\\u0023\")' >> build.tsk
echo 'REPLAC runtime.sh hash $hash' >> build.tsk
echo 'REFRSH runtime.sh output' >> build.tsk
echo 'chmod +x output/runtime.sh' >> build.tsk
```

### Windows

``` powershell
Set-Content build.tsk 'Set-Content runtime.ps1 "Write-Host `"Deploy %integer%, property set to : %property%`""'
Add-Content build.tsk 'REFRSH runtime.ps1 output'
```

### Continuous Integration (CI)

The `build.tsk` is a CI task so only need to execute

    ci.sh

or for windows

    ci

The build process will now be triggered, this can be observed in the log `build.tsk found in solution root`, this will produce a directory called `output`, however, this will not be included in the release file, which will be covered in the next step

> Next: [Packaging][mydoc_basics_packaging]

{% include links.html %}
