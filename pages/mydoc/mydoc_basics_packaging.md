---
title: Packaging
tags: [getting_started, tasks]
keywords: artefact, artifact, package, zip, gzip, tar, base64
last_updated: March 3, 2022
summary: "Artefact retention within release package."
sidebar: mydoc_sidebar
permalink: mydoc_basics_packaging.html
folder: mydoc
---

# Build-Once/Deploy-Many

An objective of Continuous Delivery is to have a predictable, repeatable, deployment process. A fundamental principle of CDAF to achieve this producing an immutable release package. This decouples the deployment process from the source management process. The release package is a self-contained deployment asset, and should be executable anywhere, i.e. on the automation developers desktop, within the pipeline or even manually file transfered to a remote server.

## storeFor

Create this file in your solution definition directot=ry. Directories and files in this list will be included in the release package.

This example places 4 files into the root of deployment directory, while the relative path of Database\scripts is preserved.

```
aspdotnet\obj\Release\Package\aspdotnet.deploy.cmd -Flat
aspdotnet\obj\Release\Package\aspdotnet.SetParameters.xml -Flat
aspdotnet\obj\Release\Package\aspdotnet.SourceManifest.xml -Flat
aspdotnet\obj\Release\Package\aspdotnet.zip -Flat

Database\scripts -Recurse
```

## Other File Locations

Files placed in the following locations within your solution directot=ry will also be automatically included in the root of your deployment directory

- crypt
- cryptLocal
- cryptRemote
- custom
- customLocal
- customRemote

An explanation of the local and container extensions will be explained in following sections.

> Next: [Local Tasks][mydoc_basics_local_tasks]

{% include links.html %}
