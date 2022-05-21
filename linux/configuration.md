# Linux Configuration

This guide will demonstrate how to configure a linux distribution.

## Table of Contents

- [Getting started](#getting-started)
- [Basic commands](#basic-commands)
- [Useful software](#useful-software-and-tools)
- [Oh-My-Zsh](#oh-my-zsh)

## Getting Started

1. Install a linux distribution. _I would recommend [Kali](https://www.kali.org/get-kali) linux._
2. Upgrade the system. _[See basic commands](#basic-commands)_
3. Install software. _[Useful software](#useful-software-and-tools)_

## Basic Commands

> :bulb: **Tip:** You can look up the documentation about commands by using `man`.

Updating all installed packages.

```bash
$ sudo apt update
```

Upgrade packages.

```bash
$ sudo apt full-upgrade -y
```

Upgrade your system.

```bash
$ sudo apt dist-upgrade -y
```

## Useful Software and Tools

- Code Editor (_I recommend [Visual Studio Code](https://code.visualstudio.com/)_)
- Docker (Check official Docker page. [Docker docs](https://docs.docker.com/))
- Git
- [Oh-My-Zsh](https://github.com/ohmyzsh/ohmyzsh)
- Tor Browser
- VPN Client

## Oh-My-Zsh

- [Install Zsh](#install-zsh)
- [Install Oh-My-Zsh](#install-oh-my-zsh)
- [Configure Oh-My-Zsh](#configure-oh-my-zsh)
- [Install Plugins](#install-plugins)
- [Recommended Plugins](#recommended-plugins)
- [Install a Font](#install-a-font)

### Install Zsh

If _Zsh_ isn't already pre-installed, install by using the apt manager.

```bash
$ sudo apt install zsh -y
```

### Install Oh-My-Zsh

After that, you can install Oh-My-Zsh from [Github](https://github.com/ohmyzsh/ohmyzsh).

```bash
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Configure Oh-My-Zsh

First, change the default theme to [Powerlevel10k](https://github.com/romkatv/powerlevel10k).

Clone the repository into the directory `.oh-my-zsh/custom/themes`.

```bash
$ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Edit your `~/.zshrc` file and replace the theme with

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

### Install Plugins

All plugins listed on the [plugins Github](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins) page are pre-installed with Oh-My-Zsh at `~/.oh-my-zsh/plugins`. Custom plugins can be installed at `~/.oh-my-zsh/custom/plugins`. To use a plugin, you can simply add it to the plugins list in your `~/.zshrc` file.

> :warning: **Warning:** Add plugins wisely, as too many plugins will slow down the shell startup.

Add a whitespace in between each plugin.

### Recommended Plugins

Already installed:

- git
- colored-man-pages
- docker
- docker-compose

Plugins needed to be installed:

- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

Clone the repositories into `~/.oh-my-zsh/custom/plugins`, see [Install Plugins](#install-plugins).

### Install a Font

Download and unzip a patched font with glyphs (icons) from [Nerd Font](https://nerdfonts.com).

Move the **.ttf** files to `~/.local/share/fonts`, maybe you need to create a _fonts_ directory first via `mkdir -p ~/.local/share/fonts`.

Set up the installed font in your terminal as default.
