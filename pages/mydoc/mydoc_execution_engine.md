---
title: Execution Engine
tags: [feature_configuration]
keywords: ASSIGN, CMPRSS, DCMPRS, DECRYP, DETOKN, EXCREM, EXITIF, INVOKE, MAKDIR, MASKED, MD5MSK, PROPLD, REFRSH; REMOVE, REPLAC, VARCHK, VECOPY, CMDTST, ELEVAT, IMGTXT, AUTOMATIONROOT, SOLUTIONROOT, BUILDNUMBER, ACTION, TMPDIR, WORKSPACE
last_updated: May 5, 2022
summary: Line-by-line Execution.
sidebar: mydoc_sidebar
permalink: mydoc_execution_engine.html
---

## Motivation

To alleviate the burden of argument passing, exception handling and logging, the execution engine has been provided. The execution engine will essentially execute the native interpretive language (PowerShell or bash), line by line, but each execution will be tested for exceptions (trivial in bash, significantly more complex in PowerShell).

### Where is it used

In all places using .tsk files, i.e. build, package, wrap and deploy. The following operations are available to all tasks, however, some are more applicable to specific processes, see Build, Local and Remote task execution for more details of how these can be used.

### Operations

The following operations are provided to simplify common tasks.

| Keyword | Description                                                  | Example
| --------|--------------------------------------------------------------|--------
| ASSIGN  | Display, and expand as necessary, variable assignment        | ASSIGN $test="$varcontainingvar"
| CMPRSS  | Compress directory to file                                   | CMPRSS packageName dirName
| DCMPRS  | Decompress package file                                      | DCMPRS packageName
| DECRYP  | decrypt using private key (PKI)                              | DECRYP crypt/encrypt.dat
|         | &nbsp;&nbsp;&nbsp;decrypt using AES/GPG key                  | DECRYP crypt/encrypt.dat $key
| DETOKN  | Detokenise file with target prop                             | DETOKN token.yml
|         | &nbsp;&nbsp;&nbsp;Detokenise with specific file              | DETOKN token.yml PROP_FILE
|         | &nbsp;&nbsp;&nbsp;Detokenise with encrypted file             | DETOKN token.yml crypt/FIL $key
|         | &nbsp;&nbsp;&nbsp;Expand and reveal embedded variables and detokenise        | DETOKN token.yml $TARGET reveal
|         | &nbsp;&nbsp;&nbsp;Expand but do not reveal embedded variables and detokenise | DETOKN token.yml manifest.txt resolve
| EXCREM  |   Execute command                                            | EXCREM hostname
|         | &nbsp;&nbsp;&nbsp;Execute script                             | EXCREM ./capabilities.sh
| EXITIF  | Exit normally if argument set                                | EXITIF $ACTION
|         | &nbsp;&nbsp;&nbsp;Exit normally if set to value              | EXITIF $ACTION clean
| IMGTXT  | Display image file as text (wrapper for jp2a in Linux)       | IMGTXT sample.jpg               |
| INVOKE  | call a custom script                                         | INVOKE ./script "Hello"
| MAKDIR  | Create a directory and path (opt)                            | MAKDIR directory/and/path
| MASKED  | Return an uppercase hexadecimal checksum using SHA256        | MASKED $password
| MD5MSK  | Deprecated. Return an uppercase hexadecimal checksum         | MD5MSK $password
| PROPLD  | Load properties as variables                                 | PROPLD PROP_FILE
|         | &nbsp;&nbsp;&nbsp;Expand and reveal embedded variables                       | PROPLD $TARGET reveal
|         | &nbsp;&nbsp;&nbsp;Expand but do not reveal embedded variables                | PROPLD manifest.txt resolve
| REFRSH  | Refresh directory contents                                   | REFRSH manifest.txt ~/temp_dir
|         | &nbsp;&nbsp;&nbsp;clear directory contents (create if not existing)          | REFRSH ~/temp_dir
| REMOVE  | Delete files, including wildcard                             | REMOVE *.war
| REPLAC  | Replace token in file                                        | REPLAC fileName %token% $value
| VARCHK  | Variable validation using default file properties.varchk     | VARCHK
|         | &nbsp;&nbsp;&nbsp;Variable validation using names file                       | VARCHK vars.properties
| VECOPY  | Verbose copy                                                 | VECOPY *.war

Notes on EXCREM use, the properties are similar to those used for remote tasks, where the minimum required is the host, if other properties are not used, must be set to NOT_SUPPLIED, i.e.

    deployHost=localhost
    remUser=NOT_SUPPLIED
    remCred=NOT_SUPPLIED
    remThb=NOT_SUPPLIED

#### Windows only

The following operations are only available in PowerShell version

| Keyword | Description                       | Example                         |
| --------|-----------------------------------|---------------------------------|
| CMDTST  | Returns true if command exists    | CMDTST vagrant                  |
| ELEVAT  | Execute as elevated NT SYSTEM     | ELEVAT "$(pwd)/custom.ps1"      |

# Build-time Variables

These are automatically set at execution start-up

| Variable        | Description
|-----------------|----------------------------------
| $AUTOMATIONROOT | The directory of the Continuous Delivery Automation Framework
| $SOLUTIONROOT   | The solution directory identified by CDAF.solution file
| $BUILDNUMBER    | The first argument passed, if not passed, this is generated
| $ACTION         | The second argument passed, has some hardcoded functions<br/> • clean: only remove temp files<br/> • packageonly: skip any build tasks
| $TMPDIR         | Automatically set to the temp dir
| $WORKSPACE      | The working directory at execution start-up

> Next: [Solution Properties][mydoc_solution_properties]

{% include links.html %}
