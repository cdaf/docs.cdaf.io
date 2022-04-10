---
title: Executing Script Runner
keywords: db
summary: Incrimental Database Script Runner Usage
sidebar: product1_sidebar
permalink: p1_usage.html
folder: product1
---

## Pre-Requisites

No additional pre-requisites are required for Windows, however, Linux requires Java 8 or above.

## DB Permissions

The user executing the DB utility requires the permissions to change database schemas.

## Database Script Names

The utility is very simple in that it will run all scripts alphabetically. The last script executed is written to the version table. The next run will only execute scripts greater than last one executed.

## Execution with CDAF

In this example, the scripts are located in this directory Database/scripts

    00.00.00.003.sql
    00.00.00.004.sql

To make these available at deploy time the storeFor definition includes all the scripts in this directory

    Database\scripts -Recurse

### Windows

Required argument is the Database name, host, user and password are optional.

```
.\Database.exe test
Database set to : test
Host not supplied, using localhost
Script URL not supplied, using ./Database/scripts/
User name not supplied, will attempt windows integrated authentication
Current Database version : 00.00.00.006
```


{% include links.html %}
