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

## Getting started

To get started, see [Getting Started][index].

{% include links.html %}
