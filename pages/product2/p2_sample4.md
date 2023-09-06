---
title: Docker on Linux
keywords: sample
summary: Native Docker Execution on Linux
sidebar: product2_sidebar
permalink: p2_sample4.html
---

# Native Linux Containers

Native Linux Containers can run different distributions from the host.

    curl -s https://raw.githubusercontent.com/cdaf/linux/master/install.sh | bash -
    ./automation/provisioning/installDocker.sh

> Note: for Redhat Enterprise Linux Podman & Buildah are installed by default and is largely Docker compatible.

# CDAF Image for Ubuntu 22.04

Get latest image

    docker pull cdaf/linux

Verify image capabilities

    docker run cdaf/linux capabilities.sh

Execute Emulation

    docker run --volume "$(pwd):/solution/workspace" cdaf/linux

Interactive Terminal (-it) in container

    docker run -it --volume "$(pwd):/solution/workspace" cdaf/linux bash

Agent in Default Pool with hostname as agent name

    docker run -d cdaf/linux /solution/register-and-run.sh $ORG_URL $POOL_TOKEN

Agent in named Pool with agent name (useful to recycle the container and replace the existing agent)

    docker run -d cdaf/linux /solution/register-and-run.sh $ORG_URL $POOL_TOKEN pool-name agent-name

Deployment Group

    docker run -d cdaf/linux /solution/register-and-run.sh $ORG_URL $GROUP_TOKEN project@deployment-group linux-target-1

# CDAF Image for Ubuntu 20.04

> note: the tools installed are designed to align with Azure DevOps agent capabilities

Get latest image

    docker pull cdaf/linux-ado-agent

Verify image capabilities

    docker run cdaf/linux-ado-agent capabilities.sh

Execute Emulation

    docker run --volume "$(pwd):/solution/workspace" cdaf/linux-ado-agent

Interactive Terminal (-it) in container

    docker run -it --volume "$(pwd):/solution/workspace" cdaf/linux-ado-agent bash

Agent in Default Pool with hostname as agent name

    docker run -d cdaf/linux-ado-agent /solution/register-and-run.sh $ORG_URL $POOL_TOKEN

Agent in named Pool with agent name (useful to recycle the container and replace the existing agent)

    docker run -d cdaf/linux-ado-agent /solution/register-and-run.sh $ORG_URL $POOL_TOKEN pool-name agent-name

Deployment Group

    docker run -d cdaf/linux-ado-agent /solution/register-and-run.sh $ORG_URL $GROUP_TOKEN project@deployment-group linux-target-1

{% include links.html %}
