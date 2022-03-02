---
title: Build Tasks
keywords: ci, build, maven, msbuild, dotnet, npm, pip, bundler, gradel, ant, make
tags: [getting_started, tasks]
summary: "The CI Task, i.e. creating artefacts from code."
sidebar: mydoc_sidebar
permalink: mydoc_basics_build_tasks.html
---

## Continuous Integration

Continuous Integration (CI) is the objective of bringing code branches together and building them to produce a consolidated artefact. This shift-left approach ensures the efforts of multiple contributors are combined and tested regularly. The testing within CI typically starts with unit testing, and that should be included in the build task. For some ecosystems this is an implicit or parameterised part of the build command, others, it's separate command.

### How dows it work

CDAF will process all build.tsk files in the solution root, then all the build.tsk files found in one level of sub-directories.

The build.tsk files are processed line by line, each line is logged and then executed, with errors and exceptions trapped and logged. In the case of linux the error processing is based on the exit code and standard error, while windows has a broader range of errors, such as halt and exception conditions. 

### A Simple Build Task

In this example, a Java build using Maven is performed. A complete reference for operations and built-in variables is available in the [supported features reference page][mydoc_supported_features].

All properties in your CDAF.solution are automatically loaded as variables when the task engine starts:

``` properties
archGroupID=co.ntier
archArtID=spring-mvc-archetype
archVersion=1.0.2
```

The output of this is placed in a temporary directory based on the solution name. The CDAF operation ``REMOVE`` is used to clean this temporary directory using the built-in variable, ``$SOLUTION``. Once clean, the Maven build is performed:

``` bash
REMOVE ${SOLUTION}

mvn --batch-mode archetype:generate -D"archetypeGroupId=${archGroupID}" -D"archetypeArtifactId=${archArtID}" -D"archetypeVersion=${archVersion}" -D"groupId=io.cdaf.java" -D"artifactId=${SOLUTION}" -D"version=${artifactPrefix}"
```

### A More Complex Build Task

In this example, a ASP.NET solution is build is being performed to create a Web Deploy package. The ``EXITIF`` operation allows the skipping of the build prcess if the built-in variable ``$ACTION`` has been set to ``clean``. In the CDAF.solution:

``` properties
productVersion=2.3
```

The ``MSTOOL`` operation loads the path to MSBuild.exe into environment variable ``$env:MS_BUILD``. The ``REPLAC`` operation detokenises static content file to inject the product version, which includes the built in ``$BUILDNUMBER``. Then the compile of the code and generation of Web Deploy (``/T:Package``) artefacts is performed:

``` powershell
REMOVE bin
REMOVE obj

Write-Host "If Action is clean only, then exit`n"
EXITIF $ACTION -eq "clean"

Write-Host "Combine to create symantic (http://semver.org/) version`n"
ASSIGN $productVersion+='.'
ASSIGN $productVersion+=$BUILDNUMBER

MSTOOL

Write-Host "PROJECT         : $($PROJECT)"
Write-Host "`$productVersion : $productVersion`n"

Write-Host "[$PROJECT] Apply product version as static content`n"
REPLAC Views\Shared\_Layout.cshtml %productVersion% $productVersion

Write-Host "[$PROJECT] Build Project ($PROJECT) with specific parameters for web deploy.`n"
& "$env:MS_BUILD" $PROJECT.csproj /T:Package /P:Configuration=Release /p:buildNumber=$productVersion
```

{% include links.html %}
