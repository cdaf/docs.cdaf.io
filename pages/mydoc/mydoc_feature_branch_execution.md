---
title: Feature Branch Execution
tags: [feature_configuration]
keywords: feature-branch.properties, feature-branch
last_updated: March 3, 2024
summary: 
sidebar: mydoc_sidebar
permalink: mydoc_feature_branch_execution.html
folder: mydoc
---

# Entry Point Wrapper

Place feature-branch.properties in your SOLUTIONROOT to allow dynamic delivery execution, based on Git Branch name. This capability is limited to entry.sh/entry.bat/entry.ps1, which are Git aware, and the recommended loose coupling entry scripts for CDAF.

```
# Separate environments for features and bugs
feature=DEV1
bugfix=DEV2

# Hotfixes deploy to all environments
hotfix=DEV1
hotfix=DEV2
```

See CDAF Samples for complete implementations in [Linux](https://github.com/cdaf/linux/tree/master/samples/feature-branch-environments) and [Windows](https://github.com/cdaf/windows/tree/master/samples/feature-branch-environments).

> Next: [Sensitive Data Strategies][mydoc_sensitive_data_strategies]

{% include links.html %}
