---
title: Extended Processes
tags: [feature_configuration]
keywords: prebuild.tsk, postbuild.tsk, package.tsk, wrap.tsk
last_updated: June 14, 2023
summary: Pre and Post, Build and Package Processes.
sidebar: mydoc_sidebar
permalink: mydoc_extended_processes.html
folder: mydoc
---

## Pre and Post, Build and Package Processes

By placing these files in your solution root, the processes will execute as described

File Name | Description
--|--
prebuild.tsk | Execute after Configuration Management processing, but before any build tasks
postbuild.tsk | Execute after solution and project level build tasks are complete
package.tsk | Execute after package workspace has been cleaned
wrap.tsk | Execute after package but prior to creating self-extracting release

> Next: [Sensitive Data Strategies][mydoc_sensitive_data_strategies]

{% include links.html %}
