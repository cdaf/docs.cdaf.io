---
title: Getting started with the Continuous Delivery Automation Framework
keywords: cdaf
tags: [getting_started]
sidebar: mydoc_sidebar
permalink: index.html
summary: What CDAF is and what it is not.
---

This documentation works through increasingly complex use cases. It is discouraged to open the CDAF code and try to determine it's purpose from the code (although it's open source, so you're most welcome). The framework uses a significant amount of dependeny injection, and without an understanding of the purpose, the code will be quite difficult to follow.

| What CDAF isn't | What CDAF is |
|-----------------|--------------|
| The Continuous Delivery Automation Framework Does not give you DevOps | The Continuous Delivery Automation Framework is optionated to help you achieve DevOps principles for Continuous Delivery |
| CDAF is not a replacement of your CI/CD orchestration tool. | CDAF is loosely coupled, allowing you to test your automation before executing in your orchestration tool. |
| It does not replace your build tools, such as MSBuild, Maven, Ant, etc. | It provides a execution engine for your build tasks, to cater for logger and error handling. |
| CDAF does not know how to deploy your application nor;<br/>does it know how to manage the configuration. | CDAF provides delivery helpers for common deployment tasks.<br/>A tabular abstraction engine is provided to support tokenised configuration files |

{% include note.html content="If you know all this and just want to install it, go to [Install for Windows][mydoc_install_cdaf_on_windows] or [Install for Linux][mydoc_install_cdaf_on_linux]."%}

Before jumping in, we recommend reading the [Introduction][mydoc_introduction] to understand the core objectives of CDAF and the principles appied to reach these goals.

> Next: [Introduction][mydoc_introduction]

{% include links.html %}
