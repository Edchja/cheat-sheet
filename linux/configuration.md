# Linux Configuration

This guide will demonstrate how to configure a Linux distribution.

## Table of Contents

- [Getting started with Linux](#getting-started)
- [Basic commands](#basic-commands)
- [Update script](#update-script)
- [Useful software](#useful-software-and-tools)
- [Terminal – Oh-My-Zsh](#oh-my-zsh)
- [Secure Shell Protocol (SSH)](/linux/tools.md#secure-shell-protocol-ssh)
  - [Configure public key authentication](#configure-public-key-authentication)

## Getting Started

1. Install a Linux distribution. _I recommend [Kali](https://www.kali.org/get-kali) Linux or [Pop_OS!](https://pop.system76.com/)._
2. Upgrade the system. _[Refer to basic commands](#basic-commands)_
3. Install software. _[See useful software](#useful-software-and-tools)_
4. Have fun learning how to use the tools.

## Basic Commands

> :bulb:**Tip:** By using `man` you can look up the documentation for a tool or command.

Updating all installed packages:

```bash
sudo apt update
```

Upgrade packages:

```bash
sudo apt full-upgrade -y
```

Upgrade your system:

```bash
sudo apt dist-upgrade -y
```

Remove automatically installed packages:

```bash
sudo apt autoremove -y
```

Cleanup repositories after updating, deletes unnecessary files:

```bash
sudo apt auto-clean -y
```

Change keyboard layout, for example to german:

```bash
sudo setxkbmap -layout de
```

> :bulb:**Tip:** If a command won't work, log in as the **root** user and try again. Since you need elevated privileges to update the system anyway, I would log in as the **root** user.

### Update Script

Here is a handy shell script that will fully update, upgrade and remove unused dependencies from your system

```bash
function apt-upd {
        apt update;
        apt full-upgrade -y;
        apt dist-upgrade -y;
        apt autoremove -y;
        apt-get clean -y;
        apt-get autoclean -y

      if [ $? -eq 0 ]
      then
        printf '%.0s\n' {1..3}
        echo -e "\e[92mSystem is updated.\e[0m"
      else
          echo "Failed to update the system"
      fi
}
```

To use that script, create a `.zsh_aliases` file in your **root** user directory and paste the code above into it. After that, you'll need to add the following code to your `.zshrc` file. So that the function can be used in your zsh terminal.

```bash
if [ -f ~/.zsh_aliases ]; then
    . ~/.zsh_aliases
fi
```

If you want, you can copy the function directly into the `.zshrc` file.

For the changes to be loaded, you'll need to enter `source ~/.zshrc` in your terminal. Now, you can type `apt-upd` as root inside of a terminal and your system will be updated.

## Useful Software and Tools

- Code Editor ([Visual Studio Code](https://code.visualstudio.com))
- Docker (Refer to the [Docker](/docker/README.md) section in this repository or the official [Docker documentation](https://docs.docker.com) page)
- Git
- [Oh-My-Zsh](https://github.com/ohmyzsh/ohmyzsh)
- [Tor Browser](/linux/tools.md#tor-browser)
- VPN Client
- [Screen](/linux/tools.md#screen)

## Oh-My-Zsh

- [Install Zsh and Oh-My-Zsh](#install-zsh)
- [Configure Oh-My-Zsh](#configure-oh-my-zsh)
- [Install Plugins](#install-plugins)
  - [Recommended Plugins](#recommended-plugins)
- [Install a Font](#install-a-font)

### Install Zsh

If _Zsh_ isn't already pre-installed, install it by using the apt manager

```bash
sudo apt install zsh -y
```

### Install Oh-My-Zsh

After that, you can install Oh-My-Zsh from [GitHub](https://github.com/ohmyzsh/ohmyzsh)

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Configure Oh-My-Zsh

First, change the default theme to [Powerlevel10k](https://github.com/romkatv/powerlevel10k).

Clone the repository into the directory `.oh-my-zsh/custom/themes`

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Edit your `~/.zshrc` file and replace the theme with

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

### Install Plugins

All plugins listed on [GitHub](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins) are pre-installed with Oh-My-Zsh at `~/.oh-my-zsh/plugins`. Custom plugins can be installed at `~/.oh-my-zsh/custom/plugins`. To use a plugin, you can simply add it to the plugins list in your `~/.zshrc` file.

> :warning:**Warning:** Add plugins wisely, as too many plugins could slow down the shell startup.

Add a whitespace in between each plugin in the `.zshrc` file.

### Recommended Plugins

Already installed in `~/.oh-my-zsh/plugins`:

- git
- colored-man-pages
- docker
- docker-compose

Plugins that are needed to be cloned:

- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

```bash
git clone --depth=1 https://github.com/zsh-users/zsh-syntax-highlighting \
${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

```bash
git clone --depth=1 https://github.com/zsh-users/zsh-autosuggestions \
${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

### Install a Font

Download and unzip a patched font with glyphs (icons) from [Nerd Font](https://nerdfonts.com).

Move the **.ttf** files to `~/.local/share/fonts`, maybe you'll need to create a _fonts_ directory first via `mkdir -p ~/.local/share/fonts`.

Set up the installed font in your terminal as the default font.

## Configure public key authentication

To setup _SSH public key authentication_, you will need to execute the following commands.

First, you have to create a `private` and `public` key pair.

```bash
ssh-keygen -t ed25519 -f ~/.ssh/<certificate-name> -C "your e-mail address or pc name"
```

> :bulb:**Tip:** You can use `man ssh-keygen` to get a detailed description about all possible parameters and options.

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

After that, you can save the `public key` to GitHub, on your Linux server or somewhere else.

If the setup is done for the first time, you will have to create a `config` file. The config file is needed, so that the host can establish a connection with the server. If you want to have an ssh key for each service or application, you can do this by adding them to the config file.

The convention of the `config` file will look like this, for **each** entry:

```bash
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/test
```

The `Host` keyword restricts the following declarations to be only for those hosts that match with the passed host name on the command line. It can be used to declare aliases, thus that will not work on Git repository hosting services like GitHub, GitLab, Bitbucket etc.

`HostName` specifies the real host name to log into. Numeric IP addresses are also permitted, e.g. `120.245.228.101`.

With the `User` keyword, it is possible to set a username which will be used to log into a server. It can simplify the use of multiple usernames like _root_, _non-root_-users, etc. With that, you don't need to pass the username on the command line.

Last but not least, the `IdentityFile` keyword. That keyword specifies a file, from which the user's **private key** is read when using _public key authentication_.

After you've set up you SSH key, you can test your connection e.g. GitHub with the following command:

```bash
ssh -T git@github.com
```

It will try to establish a connection with the server by using your SSH key you created earlier. If you set a passphrase for you **private key** you'll need to enter it first.
You may see a warning like this:

```console
The authenticity of host 'github.com (IP ADDRESS)' can't be established.
ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

You can _verify_ if the fingerprint in the message matches with [GitHub's public key fingerprint](https://docs.github.com/en/github/authenticating-to-github/githubs-ssh-key-fingerprints). If it does, then type `yes`:

```console
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

> **Note:** The remote command should exit with code 1.

Verify that the resulting message contains your **username**. If you receive a "permission denied" message, refer to [Error: Permission denied (publickey)](https://docs.github.com/en/articles/error-permission-denied-publickey).
