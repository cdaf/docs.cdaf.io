---
title: Execution Engine
tags: [feature_config]
keywords: ci, cd, make
last_updated: May 5, 2022
summary: Line-by-line Execution.
sidebar: mydoc_sidebar
permalink: mydoc_execution_engine.html
---

## Motivation

To alleviate the burden of argument passing, exception handling and logging, the execution engine has been provided. The execution engine will essentially execute the native interpretive language (PowerShell or bash), line by line, but each execution will be tested for exceptions (trivial in bash, significantly more complex in PowerShell).

### Where is it used

In all places using .tsk files, i.e. build, package, wrap and deploy. The following operations are available to all tasks, however, some are more applicable to specfic processes, see Build, Local and Remote task execution for more details of how these can be used.

### Operations

The following operations are provided to simplify common tasks.

| Keyword | Description                                                | Example
| --------|------------------------------------------------------------|--------
| ASSIGN  | Display and expand as necessary                            | ASSIGN $test="$varcontainingvar"
| CMPRSS  | Compress directory to file                                 | CMPRSS packageName dirName
| DCMPRS  | Decompress package file                                    | DCMPRS packageName
| DECRYP  | decrypt using private_key.pem                              | DECRYP crypt/encrypt.dat
|         | decrypt using AES key                                      | DECRYP crypt/encrypt.dat $key
| DETOKN  | Detokenise file with target prop                           | DETOKN token.yml
|         | Detokenise with specific file                              | DETOKN token.yml PROP_FILE
|         | Detokenise with encrypted file                             | DETOKN token.yml crypt/FIL $key
|         | Expand and reveal embedded variables and detokenise        | DETOKN token.yml $TARGET reveal
|         | Expand but do not reveal embedded variables and detokenise | DETOKN token.yml manifest.txt resolve
| EXCREM  | Execute command                                            | EXCREM hostname
|         | Execute script                                             | EXCREM ./capabilities.sh
| EXITIF  | Exit normally if argument set                              | EXITIF $ACTION
|         | Exit normally if set to value                              | EXITIF $ACTION clean
| INVOKE  | call a custom script                                       | INVOKE ./script "Hello"
| MAKDIR  | Create a directory and path (opt)                          | MAKDIR directory/and/path
| PROPLD  | Load properties as variables                               | PROPLD PROP_FILE
|         | Expand and reveal embedded variables                       | PROPLD $TARGET reveal
|         | Expand but do not reveal embedded variables                | PROPLD manifest.txt resolve
| REMOVE  | Delete files, including wildcard                           | REMOVE *.war
| REPLAC  | Replace token in file                                      | REPLAC fileName %token% $value
| VARCHK  | Variable validation check                                  | VARCHK varlistFileName
| VECOPY  | Verbose copy                                               | VECOPY *.war

#### Windows only

The following operations are only available in PowerShell version

| Keyword | Description                       | Example                         |
| --------|-----------------------------------|---------------------------------|
| CMDTST  | Returns true if command exists    | CMDTST vagrant                  |
| ELEVAT  | Execute as elevated NT SYSTEM     | ELEVAT "$(pwd)/custom.ps1"      |
| IMGTXT  | Display image file as text        | IMGTXT sample.jpg               |

Notes on EXCREM use, the properties are similar to those used for remote tasks, where the minimum requried is the host, if other properties are not used, must be set to NOT_SUPPLIED, i.e.

  deployHost=localhost
  remUser=NOT_SUPPLIED
  remCred=NOT_SUPPLIED
  remThb=NOT_SUPPLIED

# Runtime variables

These are automatically set at execution start-up

| Variable        | Description
|-----------------|----------------------------------
| $AUTOMATIONROOT | The directory of the Continuous Delivery Automation Framework
| $SOLUTIONROOT   | The solution directory identified by CDAF.solution file
| $TMPDIR         | Automatically set to the temp dir
| $WORKSPACE      | The working directory at start-up

> Next: [Environment Variables][mydoc_environment_variables]

{% include links.html %}
