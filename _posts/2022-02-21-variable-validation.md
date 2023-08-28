---
title: Variable Validation
published: true
permalink: 2022-02-21-variable-validation.html
summary: VARCHK operation has been added to the execution engine to allow different validation rules and logging.
tags: [news]
---

See [Variable Validation Blog post](https://blog.cdaf.io/posts/2022-02-21-variable-validation/) for full story.

There are 5 rules available, two for plain text and three for secrets. When validating a secret against a known MD5 value, either a literal or variable can be supplied.

```
# Plain text values
OPT_ARG                                # Optional plain text
terraform_version=required             # Required plain text

# Secret values
TERRAFORM_TOKEN=optional               # Optional secret
TERRAFORM_TOKEN=secret                 # Required secret
TERRAFORM_TOKEN=$TERRAFORM_TOKEN_MASK  # Required secret verified against supplied SHA-256 value
```

{% include links.html %}
