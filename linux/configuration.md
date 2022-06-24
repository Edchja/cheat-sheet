# Linux Configuration

This guide will demonstrate how to configure a Linux distribution.

## Table of Contents

- [Getting started](#getting-started)
- [Basic commands](#basic-commands)
- [Update script](#update-script)
- [Useful software](#useful-software-and-tools)
- [Oh-My-Zsh](#oh-my-zsh)
- [Secure Shell Protocol (SSH)](/linux/tools.md#secure-shell-protocol-ssh)
- [Configure public key authentication](#configure-public-key-authentication)

## Getting Started

1. Install a Linux distribution. _I recommend [Kali](https://www.kali.org/get-kali) Linux._
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

Change keyboard layout, for example to german:

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

To use that script, create a `.zsh_aliases` file in your **root** directory and paste the code above. After that, you'll need to add the following code to your `.zshrc` file. So that the code can be used in zsh

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
- [Tor Browser](/linux/tools.md#tor-browser)
- VPN Client
- [Screen](/linux/tools.md#screen)

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

After that, you can install Oh-My-Zsh from [GitHub](https://github.com/ohmyzsh/ohmyzsh)

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

All plugins listed on the [plugins GitHub](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins) page are pre-installed with Oh-My-Zsh at `~/.oh-my-zsh/plugins`. Custom plugins can be installed at `~/.oh-my-zsh/custom/plugins`. To use a plugin, you can simply add it to the plugins list in your `~/.zshrc` file.

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

## Configure public key authentication

To setup SSH _public key authentication_, you will need to execute the following commands.

First, you have to create a `private` and `public` key pair.

```bash
$ ssh-keygen -t ed25519 -f ~/.ssh/<certificate-name> -C "your e-mail address or pc name"
```

> :bulb: **Tip:** You can use `man ssh-keygen` to get a detailed description about all possible parameters and options.

The output will look like this:

```console
$ ssh-keygen -t ed25519 -f ~/.ssh/test
Generating public/private ed25519 key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/<name>/.ssh/test
Your public key has been saved in /home/<name>/.ssh/test.pub
The key fingerprint is:
SHA256:Jr7aTrZyDNxDEW8vQHl4YEJ/a8n0kiUzTXjB9J6y814 edgar@BEAST-PC
The key's randomart image is:
+--[ED25519 256]--+
|   .o == ++.     |
|     =+.+oo.     |
|      o+O.o .    |
|      .* @ . .   |
|   . o. S + o    |
|    o.o+ o o     |
|     o+.  o   E  |
|    .+oo   o .   |
|    .==    .o    |
+----[SHA256]-----+
```

After that, you can save the `public key` to GitHub, on your linux server or somewhere else.

If the setup is done for the first time, you will have to create a `config` file. The config file is needed, so that the host can establish a connection with the server. If you want to have an ssh key for each service or application, you can do this by adding them to the config file.

The convention of the `config` file will look like this for each entry:

```bash
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/test
```

The `Host` keyword restricts the following declarations to be only for those hosts that match with the passed host name on the command line. It can be used to declare aliases thus that will not work on repository services like GitHub, GitLab, Bitbucket etc.

`HostName` specifies the real host name to log into. Numeric IP addresses are also permitted, e.g. `120.345.678.901`.

With the `User` keyword, it is possible to set a username which will be used to log into a server. It can simplify the use of multiple usernames like _root_, _non-root-users_, etc. With that, you don't need to pass the username on the command line.

Last but not least, the `IdentityFile` keyword. That keyword specifies a file from which the user's **private key** is read when using public key authentication.
