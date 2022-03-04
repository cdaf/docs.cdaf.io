---
title: Install Pipeline
tags: [getting_started]
keywords: linux, bash, windows, powershell, cmd, command
summary: "Verify your new Solution in your CI/CD Pipeline"
sidebar: mydoc_sidebar
permalink: mydoc_install_pipeline.html
folder: mydoc
---

There are far too many CI/CD toolsets avaiable to provide detailed instructions on how to connect your solution, however, this page should provide enough examples to help configure your selected pipeline. The key principle is loose coupling, so there are two scripts to call, entry for CI, and release for CD.

# Pipeline as Code

The front-runner toolsets which are used for testing CDAF are

- Microsoft Azure DevOps
- GitLab
- Atlassian (Bamboo & BitBucket Pipelines)
- GitHub (Actions)
- Jenkins

All of this support pipelines as code. For examples of configuring these tools, see the GitHub samples for [Linux](https://github.com/cdaf/linux/tree/master/samples) and [Windows](https://github.com/cdaf/windows/tree/master/samples).

The following examples are provided for toolsets which have manual configuration options or for special considerations.

## Linux

### CI process

```
For TeamCity ...
  Command Executable : ./automation/processor/buildPackage.sh
  Command parameters : %build.number% %build.vcs.number%

For Go (requires explicit bash invoke) ...
  Command   : /bin/bash
  Arguments : -c './automation/processor/buildPackage.sh ${GO_PIPELINE_COUNTER} ${GO_REVISION}'

For Bamboo ...
  Script file : ./automation/processor/buildPackage.sh
  Argument    : ${bamboo.buildNumber} ${bamboo.repository.branch.name}

For Jenkins ...
  Command : ./automation/processor/buildPackage.sh $BUILD_NUMBER $JOB_NAME

Azure DevOps (formerly TFS/VSTS)
  Set the build name to the solution, to assure known workspace name in Release phase.
  Use the visual studio template and delete the nuget and VS tasks.
  Instructions are based on default VS layout, i.e. repo, solution, projects, with the solution in the repo root.
  NOTE: The BUILD DEFINITION NAME must not contain spaces in the name as it is the directory
        Set the build number $(rev:r) to ensure build number is an integer
        Cannot use %BUILD_SOURCEVERSION% with external Git
  Command Filename  : ./automation/processor/buildPackage.sh
  Command arguments : $BUILD_BUILDNUMBER $BUILD_SOURCEVERSION
  Working directory : selected and set to blank (otherwise the path of the ciProcess will be used)

For BlueMix ...
  Similar to TFS/Azure DevOps, BlueMix supports a single "staging" directory for artefact retention
  Build script : ./automation/processor/buildPackage.sh $BUILD_NUMBER $GIT_BRANCH staging@staging
```

### CD Process

```
Note: artifact retention typically does include file attribute for executable, so
  set the first step of deploy process to make all scripts executable
  chmod +x ./*/*.sh

For TeamCity ...
  Choose "Deployment" build
  "Use Finish Build" trigger (branch filter +:<default>)
  Configure artifact dependency using "Build from the same chain"
  Add a Configuration parameter from build.vcs.number to %env.BUILD_NUMBER%
  Add Command Line build step
  Command Executable : ./release.sh $TEAMCITY_BUILDCONF_NAME $build.number

For Go ...
  requires explicit bash invoke
  Command   : /bin/bash
  Arguments : -c './release.sh ${GO_ENVIRONMENT_NAME}'

For Bamboo ...
  Warning! Ensure there are no spaces in the environment name or release (by default release Release-xx)
  Script file : ./release.sh
  Argument    : ${bamboo.deploy.environment} ${bamboo.deploy.release}

For Jenkins ...
  Artefacts do not retain their executable bit:
        chmod +x ./*/*.sh
  Promote plugin:
    For each environment, the environment name is a literal which needs to be defined each time
    Command : ././release.sh <environment name> $PROMOTED_NUMBER
  Delivery Pipeline plugin:
    Retrieve the upstream build number from the manifest. Can use the Job Name as Environment Name
    Command : ./TasksLocal/transform.sh ./TasksLocal/manifest.txt
    Command : eval $(./TasksLocal/transform.sh ./TasksLocal/manifest.txt)
    Command : ./TasksLocal/delivery.sh $JOB_NAME $BUILDNUMBER

For Azure DevOps (formerly TFS/VSTS)
  Verify the queue for each Environment definition, and ensure Environment names do not contain spaces.
  Create an "Empty" Release definition, and use the "Command Line" utility task (note, requires double quote when more than one argument).
    Tool           : Run
    Script         : chmod +x **/*.sh && ./TasksLocal/delivery.sh $RELEASE_ENVIRONMENTNAME $RELEASE_RELEASENAME
    Working folder : $(System.DefaultWorkingDirectory)/myproduct/drop

  then add "Shell Script" utility task to execute the delivery process
    Command Filename  : $(System.DefaultWorkingDirectory)/myproduct/drop/./release.sh
    Command arguments : $RELEASE_ENVIRONMENTNAME $RELEASE_RELEASENAME
    Working folder    : $(System.DefaultWorkingDirectory)/myproduct/drop

For BlueMix ...
  Ensure staging@ directive has been used in build or the relative path will be incorrect
    ./TasksLocal/delivery.sh $IDS_STAGE_NAME $IDS_JOB_NAME
```

## Windows

### CI process

```
For TeamCity ...
  Command Executable  : call C:\Users\jules\Desktop\temp\automation\ci.bat %build.counter%
  When feature branches are enable, the branch name can be passed (will queue if used before first feature branch run)
  Command Executable  : call C:\Users\jules\Desktop\temp\automation\ci.bat %build.counter% %teamcity.build.branch%

For Bamboo ...
  Script file         : C:\Users\jules\Desktop\temp\automation\ci.bat
  Argument            : ${bamboo.buildNumber} ${bamboo.repository.branch.name}

For Jenkins ...
  Command : C:\Users\jules\Desktop\temp\automation\ci.bat %BUILD_NUMBER% %SVN_REVISION%

For BuildMaster ... (use "Get Source from Git Repository" to download to $WorkingDirectory, then "PSExec" as follows)
  Set workspace       : cd $WorkingDirectory
  Run CI Process      : C:\Users\jules\Desktop\temp\automation\ci.bat ${BuildNumber}

For Azure DevOps/Server (formerly Visual Studio Team Services (VSTS)/Team Foundation Server (TFS))
  Recommend using azure-pipelines (see samples folder)
    Use the visual studio template and delete the nuget and VS tasks.
    NOTE: The BUILD DEFINITION NAME must not contain spaces in the name as it is the directory.
          recommend using solution name, then the Release instructions can be used unchanged.
          Set the build number $(rev:r)
    Recommend using the navigation UI to find the entry script.
    Command Filename  : C:\Users\jules\Desktop\temp\automation\ci.bat
    Command arguments : %BUILD_BUILDNUMBER% %BUILD_SOURCEBRANCHNAME%
```

### CD Process

```
For TeamCity ...
  Choose "Deployment" build
  "Use Finish Build" trigger (branch filter +:<default>)
  Configure artifact dependency using "Build from the same chain"
  Add a Configuration parameter from build.vcs.number to %env.BUILD_NUMBER%
  Add Command Line build step
    Custom script       : .\release.ps1 %env.TEAMCITY_BUILDCONF_NAME% %build.number%

For Bamboo ...
  Script file           : ${bamboo.build.working.directory}\release.ps1
  Argument              : ${bamboo.deploy.environment} ${bamboo.deploy.release}

For Jenkins (each environment requires a literal definition) ...
  Command               : .\release.ps1 <environment literal> %SVN_REVISION%

For BuildMaster ... (Use "Deploy Artifact" to download to $WorkingDirectory, then use "PSExec" as follows)
  Set workspace         : cd $WorkingDirectory
  Run Delivery          : .\release.ps1 ${EnvironmentName} ${ReleaseNumber}

For Azure DevOps/Server (formerly Visual Studio Team Services (VSTS)/Team Foundation Server (TFS))
  Verify the queue for each Environment definition, and ensure Environment names do not contain spaces.
  Run an build with artefacts initially to load the workspace, which can then be navigated to for following configuration.
  From an empty release configuration, bind to the existing build and within the stage, add a "PowerShell" step.
    Command Filename    : $(System.DefaultWorkingDirectory)\myproduct\drop\release.ps1
    Command arguments   : "$(Release.EnvironmentName)" "$(Release.ReleaseName)"
    Working folder      : $(System.DefaultWorkingDirectory)\myproduct\drop
    Release name format : $(Release.DefinitionName)-$(Build.BuildNumber)
      For re-release    : $(Release.DefinitionName)-$(Build.BuildNumber)-$(rev:r)
```

> Next: [Configuration Management][mydoc_configuration_management]

{% include links.html %}
