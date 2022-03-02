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

## Build-Once/Deploy-Many

An objective of Continuous Delivery is to have apredictable, repeatable deployment process. A fundamental principle of CDAF to achieve this is the production of an immutable release package. This decouples the deployment process from the source management process. The release package is a self-contained deployment asset, and should be executable anywhere, i.e. on the automation developers desktop and within the pipeline.



> Next: [Local Tasks][mydoc_basics_local_tasks]

{% include links.html %}
