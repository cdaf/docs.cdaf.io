---
title: Legacy Features
tags: [feature_configuration, tasks]
keywords: local testing, loop-back, loop back
last_updated: May 4, 2022
summary: Supported features of CDAF, whos use is discouraged
sidebar: mydoc_sidebar
permalink: mydoc_legacy_features.html
folder: mydoc
---

## Remote Deployment

Machine to machine deployments are increasingly uncommon, as local agents/runners are readily available, making on-premise deployments from the build server an infrequent use case. While there is no plan to deprecate this capability, it's complexity makes local testing i.e. shift-left complicated, especially in windows. For CDAF configuration, see [Remote Tasks][mydoc_basics_remote_tasks].

### Windows Remote PowerShell

This approach uses the local host for both target (CD) and build (CI) execution. Provision the host with both roles

    .\automation\provisioning\mkdir.ps1 C:\deploy
    .\automation\provisioning\CredSSP.ps1 server

    .\automation\provisioning\trustedHosts.ps1 *
    .\automation\provisioning\CredSSP.ps1 client

### Linux SSH

Generate PKI key and public certificate, and perform a loop-back connection to local host to place the public certificate in the authorised hosts configuration.

    .\automation\provisioning\agent.sh deployer@localhost

## Symetric Encryption

With the implementation of 12-Factor applications, secret management in files is less common, and the storage of encrypted files in source control for subsequent decryption is now uncommon. While this capability is not planned for deprecation, it is recommended to use [sensitive data strategies][mydoc_sensitive_data_strategies] instead.

{% include links.html %}
