# Docker Configuration

This guide will demonstrate how to install and configure docker on a linux distribution.

## Table of Contents

- [Getting started](#getting-started)
- [Uninstall old versions](#uninstall-old-versions)
- [Install Docker](#install-docker-engine)
- [Uninstall Docker Engine](#uninstall-docker-engine)

## Getting Started

1. Make sure you meet the [prerequisites](https://docs.docker.com/engine/install/ubuntu/#prerequisites) from the official docs.
2. [Uninstall old versions](#uninstall-old-versions)

## Uninstall old versions

Older versions of docker were called `docker`, `docker.io` or `docker-engine`. If these are installed, uninstall them:

```bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

It's OK if apt-get reports that none of these packages are installed.

The contents of `/var/lib/docker`, including images, containers, volumes and networks, are preserved. If you want a clean installation refer to the [uninstall Docker Engine](#uninstall-docker-engine) section.

## Install Docker Engine

- [Set up official Docker repository](#set-up-the-repository)
- [Install Docker Engine](#install-docker-engine)

Before installing Docker Engine, it is necessary to set up the Docker repository first. Afterward, it is possible to install and update Docker from the repository.
Make sure old versions of Docker are uninstalled before installation (Refer to [uninstall old versions](#uninstall-old-versions)).

### **Set up the repository**

Update your system and install packages to allow `apt` to use a repository over HTTPS:

```bash
$ sudo apt update

$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

Add Docker's official GPG key (Check out the official [docs](https://docs.docker.com/engine/install/#server) to get the right key for your linux distribution):

```bash
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

Use the following command set up the **stable** repository:

```bash
$ echo \
    "deb [arch=$(dpkg --print-architecture) \
    signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### **Install Docker Engine**

Update the `apt` index and install the _latest version_ of Docker Engine, containerd and Docker Compose:

```bash
$ sudo apt update
$ sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Verify that Docker Engine is installed correctly by running the `hello-world` image.

```bash
$ sudo docker run hello-world
```

This command downloads a test image and runs it in a container. When the container runs, it prints a message and exits.

## Uninstall Docker Engine

If you want to uninstall Docker Engine, CLI, Containerd and Docker Compose completely:

```bash
$ sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

After that containers, volumes or customized configuration files on your host are not automatically removed. To delete all images, containers and volumes:

```bash
$ sudo rm -rf /var/lib/docker
$ sudo rm -rf /var/lib/containerd
```
