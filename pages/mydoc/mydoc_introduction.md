---
title: Introduction
sidebar: mydoc_sidebar
permalink: mydoc_introduction.html
folder: mydoc
---

| What CDAF isn't | What CDAF is |
|-----------------|--------------|
| The Continuous Delivery Automation Framework Does not give you DevOps | The Continuous Delivery Automation Framework is optionated to help you achieve DevOps principles for Continuous Delivery |
| CDAF is not a replacement of your CI/CD orchestration tool. | CDAF is loosely coupled, allowing you to test your automation before executing in your orchestration tool. |
| It does not replace your build tools, such as MSBuild, Maven, Ant, etc. | It provides a execution engine for your build tasks, to cater for logger and error handling. |
| CDAF does not know how to deploy your application nor;<br/>does it know how to manage the configuration. | CDAF provides delivery helpers for common deployment tasks.<br/>A tabular abstraction engine is provided to support tokenised configuration files |

## Overview

This documentation works through increasingly complex use cases. It is discouraged to open the CDAF code and try to determine it's purpose from the code (although it's open source, so you're most welcome). The framework uses a significant amount of dependeny injection, and without an understanding of the purpose, the code will be quite difficult to follow.

## _Geared for Enterprise DevOps_

The framework origin is within Enterprises, deploying production systems for internal and external consumption. Although CDAF is used for product shipping, i.e. the framework is used to deliver itself, this is not it's primary purpose.

### Common Denominators

There are some common capabilities of CI/CD orchestration tools which are factored into the CDAF design.

#### Build Artefacts

The results of the CI process can be retained and re-used in deployment process. This basic capability is critical to embrace the build-once/deploy-many principle.

#### Agents

CI/CD orchestration tools execute the task workload on Agents. There are a broad range of implemenation styles, especially with regards to how the agents communicate with the server,and how tasks are distributed to agents, but the principle is largely the same.

> some agents are obfuscated from the users, and others will execute tasks in isolated containers on the agent, which will be explored in more detail in the Containers section.

#### Continuous Delivery, not Continuous Deployment

As CDAF is geared toward enterprises, promotion to production is typically gated and Continuous Deployment is uncommon, therefore in this material, CD is a reference to Continuous Delivery.

#### Git

Source Control in all the documentation is oriented to Git. There is nothing stopping the use of the framework with other source control system at all because it is loosely coupled, however, there are considerable additional features which work best with Git.

#### Pipeline

The capability of the CI/CD orchestration tools to decouple the CI and CD functions, with the CD operations being completely independent of source control.

> Next: [Getting Started][index].

{% include links.html %}
