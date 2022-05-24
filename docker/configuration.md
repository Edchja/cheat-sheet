# Docker Configuration

This guide will demonstrate how to install and configure docker on a linux distribution.

## Table of Contents

- [Getting started](#getting-started)
- [Uninstall old versions](#uninstall-old-versions)
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

## Uninstall Docker Engine

If you want to uninstall Docker Engine, CLI, Containerd and Docker Compose completely:

```bash
$ sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

After that containers, volumes, networks or customized configuration files on your host ar not automatically removed. To delete all images, containers and volumes:

```bash
$ sudo rm -rf /var/lib/docker
$ sudo rm -rf /var/lib/containerd
```
