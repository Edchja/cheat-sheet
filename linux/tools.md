# Linux Tools

This is a collection about various Linux tools.

## Table of Contents

- [Tor Browser](#tor-browser)
- [Secure Shell Protocol (SSH)](#secure-shell-protocol-ssh)
- [Visual Studio Code](#visual-studio-code)
- [Screen Tool](#screen)
- [Sherlock - Find Usernames Across Social Networks](#sherlock)

## Tor Browser

The Tor Browser is a internet browser that allows users to surf the web _anonymously_ (If used the right way). It also gives you access to the **dark web**.

Tor Browser can be installed very easily by using `apt`.

Open a terminal, then run the following commands:

```bash
sudo apt update
sudo apt install -y tor torbrowser-launcher
```

After the process completes, run the following command as **non-root** user:

```bash
torbrowser-launcher
```

The first time, it will download and install Tor Browser, including the signature verification.
Next time, it will be used to update and launch Tor Browser.

> :warning: **Warning:** It is true that you are more **anonymous** when using the Tor Browser instead of a normal browser like Chrome or Firefox.
>
> But to be even more `secure` and `anonymous` while browsing the web with `Tor Browser`, get a good and secure _VPN_.
A good _VPN_ will encrypt your data and hide your IP address as well. The possibility of being tracked will be very low and hard to accomplish.

## Secure Shell Protocol (SSH)

- [What is SSH](#what-is-ssh)
- [What are SSH keys](#what-are-ssh-keys)
- [Configure public key authentication](./configuration.md#configure-public-key-authentication)

### What is SSH

**SSH** also known as Secure Shell, is a network protocol that gives users, a secure way to access a computer over an unsecured network. **SSH** provides strong password authentication and public key verification, as well as encrypted data communication between two computers connecting over an open network.

Secure Shell was created to replace insecure terminal emulation or login programs, such as [Telnet](https://wikipedia.org/wiki/Telnet) and [rsh](https://wikipedia.org/wiki/Remote_Shell) (remote shell). **SSH** enables the same functions, like logging in to and running terminal sessions on remote systems. **SSH** also replaces file transfer programs, such as File Transfer Protocol ([FTP](https://wikipedia.org/wiki/File_Transfer_Protocol)) and rcp (remote copy).

The most basic use of `SSH` is to connect to a remote host for a terminal session. The command for that would be

```bash
ssh UserName@server.example.com
```

This command will establish a connection between the local host and the server, the user will be prompted with the remote host's public key fingerprint

```console
The authentication of host 'sample.ssh.com' cannot be established.
ECDSA key fingerprint is SHA256:fIeOO+66eOvuFtoF54z4UT7gS3oTTbrO0sxfxvhzBHw.
Are you sure you want to continue connecting (yes/no)?
```

If you answer with _yes_, the session will continue and the host key is stored in the local system `known_hosts` file. This file is located in your home directory and is called `~/.ssh/known_hosts`.
Once the key has been stored in the `known_hosts` file, the client can connect directly to that server again without the need for any approvals.

### What are SSH keys

**SSH keys** are comparable to a very long password. SSH keys always come as a pair, and every pair is made up of a `private` and `public` key. If you want to connect to an SSH server, the `private` key will remain on the host machine and will be used to **decrypt** information that is exchanged over the **SSH** protocol.

> :warning: **Warning:** Private keys should always be handled securely - i.e. the system is fully encrypted and the **private** key is secured with a passphrase.

The `public` key is used to **encrypt** information, it can be shared, and is used by the user as well as by the server. The key will be stored in an `authorized_keys` file on the server, which can contain a list of authorized public keys. The file is usually located in `~/.ssh/authorized_keys`.

If you want to setup SSH keys, check the [configure public key authentication](./configuration.md#configure-public-key-authentication) section.

## Visual Studio Code

**[Visual Studio Code](https://code.visualstudio.com)** is a free, powerful code editor that runs on every machine.

## Screen

**Screen** is a terminal multiplexer. In other words, it means that you can start a screen session and then open any number of windows (virtual terminals) inside that session. Processes running in Screen will continue to run when their window is not visible, even if you get disconnected.

- [Install Screen](#install-screen)
- [Start Screen](#start-screen)
- [Start Named Screen](#start-named-session)
- [Useful Screen Commands](#useful-screen-commands)
- [Window Splitting](#window-splitting)
- [Detach from a Screen session](#detach-from-screen-session)
- [Reattach to a Screen session](#reattach-to-a-screen-session)

### Install Screen

You can install `Screen` by using the `apt` manager

```bash
sudo apt update
sudo apt install screen
```

### Start Screen

To start a **Screen** session, simply type `screen` in your terminal.
Now that you have a screen session open, you can get a list of commands by typing:

```bash
Ctrl + a (Shift) ?
```

### Start Named Session

You can as well start a named session, for example if you are running multiple screen sessions. To create a named session:

```bash
screen -S session_name
```

### Useful Screen Commands

> :bulb: **Tip:** You can use `man` to see a detailed documentation about `screen`.

To create a new window with shell

```bash
Ctrl + a + c
```

To list all windows

```bash
Ctrl + a + "
```

Switch to a window

```bash
Ctrl + a + 0..9
```

Rename a current window

```bash
Ctrl + a + A
```

### Window splitting

Split current region horizontally into two regions

```bash
Ctrl + a + S
```

Split current region vertically into two regions

```bash
Ctrl + a + |
```

Switch the input focus to the next regions

```bash
Ctrl + a + Tab
```

Toggle between the current and previous windows

```bash
Ctrl + a Ctrl + a
```

Close all regions except the current one

```bash
Ctrl + a + Q
```

Close the current region

```bash
Ctrl + a + X
```

### Detach from Screen session

You can detach from a `screen` session anytime by typing

```bash
Ctrl + a + d
```

The program running in the screen session will continue to run after you detach from the session.

### Reattach to a Screen session

To resume your `screen` session, use the following command

```bash
screen -r
```

If you have multiple screen sessions running on your machine, you will need to append the screen session ID after the `r` switch.

To find the session ID, list the current running `screen` sessions with

```bash
screen -ls
```

The output will look like this

```console
user@hostname:~# screen -ls
There are screens on:
        20131.pts-0.hostname    (05/30/2022 12:43:27 AM)    (Detached)
        29062.pts-0.hostname    (05/30/2022 12:41:46 AM)    (Detached)
2 Sockets in /run/screen/S-root.
```

If you want to restore screen `29062.pts-0`, then type the following command

```bash
screen -r 29062
```

## Sherlock

**Sherlock** is a [python](https://www.python.org/) tool, that can find social media accounts by username across various [social networks](https://github.com/sherlock-project/sherlock/blob/master/sites.md).

- [Install Sherlock](#install-sherlock)
- [How to use Sherlock](#sherlock-usage)

### Install Sherlock

Sherlock can be installed very easily by using the following commands:

Clone the [official repository](https://github.com/sherlock-project/sherlock) into a desired location first:

```bash
git clone https://github.com/sherlock-project/sherlock.git
```

After that, change the working directory to sherlock:

```bash
cd sherlock
```

:bulb: You may need to install `python3` and `pip` first, before you can install the necessary requirements:

Update your system:

```bash
apt update
```

Then install python3 and pip:

```bash
apt install python3
apt install python3-pip
```

The last step is installing the python requirements:

```bash
python3 -m pip install -r requirements.txt
```

### Sherlock Usage

A detailed description about all possible arguments `Sherlock` provides can be looked up with:

```bash
python3 sherlock --help
```

Or on the official [GitHub repository](https://github.com/sherlock-project/sherlock#usage).

To search only for one user:

```bash
python3 sherlock user123
```

To search for more than one user:

```bash
python3 sherlock user1 user2 user3 ...
```

> If accounts are found, they will be stored in an individual text file with the corresponding username (e.g. `user1.txt`, `user2.txt`).
