---
title: Sensitive Data Strategies
tags: [feature_configuration]
keywords: configuration management, environment variables, properties, settings, tokenisation
last_updated: July 3, 2016
summary: 
sidebar: mydoc_sidebar
permalink: mydoc_sensitive_data_strategies.html
folder: mydoc
---

# Loose Coupling

A key approach to support the principle of automation execution in a local desktop context, is the use of environment variables. It's important to remember that environment variables do not necessarily need to be persisted, i.e. stored unencrypted on disk, it's the global availability of the variable that makes it an environment variable.


```
context  target  databaseFQDN        dBpassword
local    TEST    db1.nonprod.local   $DB1_PASSWORD
local    UAT     db2.nonprod.local   $DB2_PASSWORD
local    PROD    cluster.prod.local  $PRD_PASSWORD
```

# Variable Expansion

Variables can be referenced in preoperties files (see [Configuration Management][mydoc_basics_configuration_management]) or CDAF.solution file and then expanded at deploy time into variables or files using ASSIGN, PROPLD or DETOKN in the [execution engine][mydoc_execution_engine].

# Encrypted Files

This approach is to allow secrets in a file to be stored in source control. Encryption key for Windows is an EAS key, while for Linux it's a GPG key. This approach is used when there are a large number of secrets to cater for, and therefore only the key needs to be managed as a secret.

In early generations of secret management, the secrets would be stored as persistent environment variables, however all modern toolsets provide an encrypted store which can load secrets as environment variables.

See the DECRYP & DETOKN operations in the [execution engine][mydoc_execution_engine] for guidance on usage.

# Cloud Storage Integration

Toolset providers who also supply public cloud provide integration to their secret storage offerings, while these can be convenient, this does couple your automation to toolset and makes the execution of locally challenging.

> Next: [Legacy Features][mydoc_legacy_features]

{% include links.html %}
