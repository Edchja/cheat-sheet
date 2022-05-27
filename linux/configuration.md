# Linux Configuration

This guide will demonstrate how to configure a linux distribution.

## Table of Contents

- [Getting started](#getting-started)
- [Basic commands](#basic-commands)
- [Update script](#update-script)
- [Useful software](#useful-software-and-tools)
- [Oh-My-Zsh](#oh-my-zsh)
- [Install Tor Browser](#install-tor-browser)

## Getting Started

1. Install a linux distribution. _I recommend [Kali](https://www.kali.org/get-kali) linux._
2. Upgrade the system. _[See basic commands](#basic-commands)_
3. Install software. _[Useful software](#useful-software-and-tools)_

## Basic Commands

> :bulb: **Tip:** You can look up the documentation about commands by using `man`.

Updating all installed packages:

```bash
$ sudo apt update
```

Upgrade packages:

```bash
$ sudo apt full-upgrade -y
```

Upgrade your system:

```bash
$ sudo apt dist-upgrade -y
```

Change keyboard layout for example to german:

```bash
$ sudo setxkbmap -layout de
```

### Update Script

Here is a handy shell script, that will fully update, upgrade and remove unused dependencies from your system

```bash
function apt-upd {
        apt update;
        apt full-upgrade -y;
        apt dist-upgrade -y;
        apt autoremove -y;
        apt-get clean -y;
        apt-get autoclean -y

        printf '%.0s\n' {1..3}
        echo -e "\e[92mSystem is updated.\e[0m"
        }
```

To use that script, create a `.zsh_aliases` file in your **root** directory and paste the code above. After that you'll need to add the following code to your `.zshrc` file. So that the code can be used in zsh

```bash
if [ -f ~/.zsh_aliases ]; then
    . ~/.zsh_aliases
fi
```

For the changes to be loaded, you need to enter `source ~/.zshrc` in your terminal. Now, you can type `apt-upd` as root, and everything will be updated.

## Useful Software and Tools

- Code Editor (_I recommend [Visual Studio Code](https://code.visualstudio.com/)_)
- Docker (Refer to the [Docker](/docker/README.md) section or the official [Docker documentation](https://docs.docker.com/) page)
- Git
- [Oh-My-Zsh](https://github.com/ohmyzsh/ohmyzsh)
- [Tor Browser](#install-tor-browser)
- VPN Client

## Oh-My-Zsh

- [Install Zsh](#install-zsh)
- [Install Oh-My-Zsh](#install-oh-my-zsh)
- [Configure Oh-My-Zsh](#configure-oh-my-zsh)
- [Install Plugins](#install-plugins)
- [Recommended Plugins](#recommended-plugins)
- [Install a Font](#install-a-font)

### Install Zsh

If _Zsh_ isn't already pre-installed, install by using the apt manager

```bash
$ sudo apt install zsh -y
```

### Install Oh-My-Zsh

After that, you can install Oh-My-Zsh from [Github](https://github.com/ohmyzsh/ohmyzsh)

```bash
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Configure Oh-My-Zsh

First, change the default theme to [Powerlevel10k](https://github.com/romkatv/powerlevel10k)

Clone the repository into the directory `.oh-my-zsh/custom/themes`

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

## Install Tor Browser

The Tor Browser is a internet browser that allows users to surf the web _anonymously_ (If used the right way). It also gives you access to the **dark web**.

Tor Browser can be installed very easily by using `apt`.

Open a terminal then run the following commands:

```bash
$ sudo apt update
$ sudo apt install -y tor torbrowser-launcher
```

After the process completes, run the following command as **non-root** user:

```bash
$ torbrowser-launcher
```

The first time, it will download and install Tor Browser including the signature verification.

Next time it will be used to update and launch Tor Browser.

> :warning: **Warning:** It is true that you are more **anonymous** when using the Tor Browser instead of a normal browser like Chrome or Firefox.
>
> But to be more **secure** and **anonymous** while browsing the web with `Tor Browser`, get a good and secure `VPN`. A good `VPN` Client will encrypt your data and hide your IP address as well. The possibility of being tracked will be very low.
