---
title: Supported features
tags: [getting_started, tasks]
keywords: "features, capabilities, abstraction, obfuscation"
last_updated: "February 27, 2022"
summary: "This page provides reference material for Continuous Delivery Automation Framework."
published: true
sidebar: mydoc_sidebar
permalink: mydoc_supported_features.html
folder: mydoc
---

>  Without context, many of these may seem meaningless, please read the [introduction][mydoc_introduction] first.

## Supported features

Feature                | Notes
-----------------------|-----------
Properties Abstraction | Tabular representation of properties, providing human readable state and environment variants
Tasks Executor         | Line by line execution with logging and error handling

## Task Execution Engine

The execution engine provides common task operations.

| Keyword | Description                       | Example                         |
| --------|-----------------------------------|---------------------------------|
| ASSIGN  | set a variable                    | ASSIGN $test="Hello World"      |
| CMDTST  | Returns true if command exists    | CMDTST vagrant                  |
| CMPRSS  | Compress directory to file        | CMPRSS packageName dirName      |
| CMPRSS  | Compress directory to file        | CMPRSS packageName              |
| DCMPRS  | Decompress package file           | DCMPRS packageName              |
| DECRYP  | decrypt file using DSAPI          | DECRYP encrypt.dat              |
|         | decrypt using PKI or AES key      | DECRYP encrypt.dat $thumbPrint  |
| DETOKN  | Detokenise file with target prop  | DETOKN token.yml                |
|         | Detokenise with specific file     | DETOKN token.yml PROPERTY_FILE  |
|         | Detokenise with encrypted file    | DETOKN token.yml crypt/FIL $key |
| ELEVAT  | Execute as elevated NT SYSTEM     | ELEVAT "$(pwd)/custom.ps1"      |
| EXCREM  | Execute Remote Command            | EXCREM hostname                 |
|         | Execute Remote script             | EXCREM ./capabilities.ps1       |
| EXITIF  | Exit normally is argument set     | EXITIF $ACTION -eq clean        |
| INVOKE  | call a custom script              | INVOKE ./script "Hello"         |
| MAKDIR  | Create a directory and path (opt) | MAKDIR directory/and/path       |
| PROPLD  | Load properties as variables      | PROPLD prop.file                |
| REMOVE  | Delete files, including wildcard  | REMOVE *.war                    |
| REPLAC  | Replace token in file             | REPLAC fileName %token% $value  |
| VARCHK  | Variable validation check         | VARCHK varlistFileName          |
| VECOPY  | Verbose copy                      | VECOPY *.war                    |

### Windows Only Execution Operations

| Keyword | Description                       | Example                         |
| --------|-----------------------------------|---------------------------------|
| IMGTXT  | Display image file as text        | IMGTXT sample.jpg               |

{% include links.html %}

### Task Variables

| Variable       | Description                                                   |
| ---------------|---------------------------------------------------------------|
| BUILDNUMBER    | The first argument passed, if not passed, this is generated   |
| ACTION         | The second argument passed, has some hardcoded functions<br/> • clean: only remove temp files<br/> • packageonly: skip any build tasks |
| AUTOMATIONROOT | The install location of CDAF                                  |
| SOLUTIONROOT   | The location of your CDAF.solution file                       |
| SOLUTION       | The solutionName from CDAF.solution file                      |
