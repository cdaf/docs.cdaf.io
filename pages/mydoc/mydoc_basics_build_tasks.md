---
title: Build Tasks
keywords: ci, build, maven, msbuild, dotnet, npm, pip, bundler, gradel, ant, make
tags: [tasks]
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



``` bash
PROPLD ${SOLUTIONROOT}/CDAF.solution
REMOVE ${SOLUTION}

mvn --batch-mode archetype:generate -D"archetypeGroupId=${archGroupID}" -D"archetypeArtifactId=${archArtID}" -D"archetypeVersion=${archVersion}" -D"groupId=io.cdaf.java" -D"artifactId=${SOLUTION}" -D"version=${artifactPrefix}"
```

### A Complex Build Task

Let's jump into a complex example, to see a some of the key 

``` powershell
REMOVE bin
REMOVE obj

Write-Host "If Action is clean only, then exit`n"
EXITIF $ACTION -eq "clean"

Write-Host "Load product (solution) attributes`n"
ASSIGN $loadProperties="$SOLUTIONROOT\CDAF.solution"

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
