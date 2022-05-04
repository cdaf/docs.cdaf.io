---
title:  Configuration Management
tags: [getting_started, tasks]
keywords: configuration management, name value, properties, settings, tokenisation
last_updated: Mar 4, 2022
summary: Configuration Management is the principle of controlling the properties and settings of environments from source control, to provide transparency and traceability of current state and changes over time.
sidebar: mydoc_sidebar
permalink: mydoc_basics_configuration_management.html
folder: mydoc
simple_map: true
map_name: usermap
box_number: 1
folder: mydoc
---

CDAF origin was to ensure consistent configuration of servers accross environments, based on a source of truth. The partner construct to this approach is tokenisation, i.e. a way of abstracting environment variations away from the syntax of the consuming application.

## Tabular Properties

To provide a human readable, single pane-of-glass view of the multiple environment configurations, a tabular approach is used. An example of this follows. The first two columns, context and target are mandatory, all others can be any values needed for your solution.

```
context  target  databaseFQDN        dBpassword
local    TEST    db1.nonprod.local   $db1Pass
local    UAT     db2.nonprod.local   $db2Pass
local    PROD    cluster.prod.local  $prodPass
```

> Configuration Management files should never container sensitive data or secrets. These are supplied as variables, see more on [sensitive data strategies][mydoc_basics_sensitive_data_strategies].

The configuration managment tables can be any file name with .cm extension, in your solution root. All .cm files are processed prior to the [build task][mydoc_basics_build_tasks] in the CI process.

## Tokenisation

The partner files in source control are in whatever syntax required by the application, with tokens only for values that vary between environment. By default, tokens are in the form ``%name%``. Following examples highlight how the configuration management is intended to provide an abstraction from the complexities of the application configuration files.

### ASP.NET

``` xml
  <connectionStrings>
    <add name="aspdotnetEntities"
      connectionString="metadata=res://*/Models.aspdotnet.csdl|res://*/Models.aspdotnet.ssdl|res://*/Models.aspdotnet.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=%databaseFQDN%;initial catalog=aspdotnetapp;integrated security=True;multipleactiveresultsets=True;application name=EntityFramework&quot;" providerName="System.Data.EntityClient"
      xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
  </connectionStrings>
```

### dotnet core

``` json
{
  "ConnectionStrings": {
    "appDB": "Server=%databaseFQDN%;Database=dotnetcoreapp;Trusted_Connection=True;"
  }
}
```

### Python

``` yaml
database: 

dbopt:
   host: %databaseFQDN%
   dbname: pythonapp
   user: pythonappdbuser
   password: @dBpassword@
```

### Java

``` properties
jdbcConnection=jdbc:mysql://%databaseFQDN%/javaapp
jdbcDiver=com.mysql.jdbc.Driver
```

With the properties for the application defined, now it is time to build the application.

> Next: [build tasks][mydoc_basics_build_tasks]

{% include links.html %}
