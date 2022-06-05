---
title: Introduction
sidebar: mydoc_sidebar
permalink: mydoc_introduction.html
folder: mydoc
keywords: build artefacts, agents, pipelines
---

## _Geared for Enterprise DevOps_

The framework origin is within Enterprises, deploying production systems for internal and external consumption. Although CDAF is used for product shipping, i.e. the framework is used to deliver itself, this is not it's primary purpose.

### Framework Principles

CDAF provides consistency in the solution build, package and delivery mechanics, providing the basis of a code driven delivery, whereby any changes to the methodology are traceable in the source control system. While CDAF focusses on the mechanics of Continuous Delivery, the CI Tools are relied upon for source control integration, artefact retention and providing a graphical user interface for features such as reviewing automated test results and release gating.

![](images/ToolsetIntegration.png)

- **Loose Coupling** : Designed for workstation implemention first, with no tight coupling to any given automation toolset
- **Lowest Common Denominator** : Using the minimum of the toolchain plugins & capabilities, to ensure loose coupling
- **Package Portability** : Package Task execution designed for automated push / pull or manually deployment
- **Task Definition** : Framework to manage logging, exceptions and errors, to allow the user to focus on the tasks to be performed

### Common Denominators

The following are core capabilities of CI/CD orchestration tools, which are factored into the CDAF design.

#### Build Artefacts

The results of the CI process can be retained and re-used in deployment process. This basic capability is critical to embrace the build-once/deploy-many principle.

#### Agents

CI/CD orchestration tools execute the task workload on Agents. There are a broad range of implemenation styles, especially with regards to how the agents communicate with the server,and how tasks are distributed to agents, but the principle is largely the same.

> some agents are obfuscated from the users, and others will execute tasks in isolated containers on the agent, which will be explored in more detail in the Containers section.

#### Gating

As CDAF is geared toward enterprises, promotion to production is typically gated (Continuous Delivery) with Continuous Deployment being uncommon, therefore in this material, CD is a reference to Continuous Delivery unless otherwise stated.

#### Git

Source Control in all the documentation is oriented to Git. There is nothing stopping the use of the framework with other source control system at all because it is loosely coupled, however, there are considerable additional features which work best with Git.

#### Pipelines

The capability of the CI/CD orchestration tools to decouple the CI and CD functions, with the CD operations being completely independent of source control.

> Next: [Install for Windows][mydoc_install_cdaf_on_windows] or [Install for Linux][mydoc_install_cdaf_on_linux].

{% include links.html %}
