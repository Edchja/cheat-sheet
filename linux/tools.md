# Linux Tools

This is a collection about various Linux tools.

## Table of Contents

- [Tor Browser](#tor-browser)
- [Screen Tool](#screen)

## Tor Browser

The Tor Browser is a internet browser that allows users to surf the web _anonymously_ (If used the right way). It also gives you access to the **dark web**.

Tor Browser can be installed very easily by using `apt`.

Open a terminal then run the following commands:

```bash
$ sudo apt update
$ sudo apt install -y tor torbrowser-launcher
```

After the process completes, run the following command as **non-root** user:

```console
$ torbrowser-launcher
```

The first time, it will download and install Tor Browser including the signature verification.
Next time it will be used to update and launch Tor Browser.

> :warning: **Warning:** It is true that you are more **anonymous** when using the Tor Browser instead of a normal browser like Chrome or Firefox.
>
> But to be more `secure` and `anonymous` while browsing the web with `Tor Browser`, get a good and secure _VPN_. A good _VPN_ will encrypt your data and hide your IP address as well. The possibility of being tracked will be very low and hard to accomplish.

## Screen

**Screen** is a terminal multiplexer. In other words, it means that you can can start a screen session and then open any number of windows (virtual terminals) inside that session. Processes running in Screen will continue to run when their window is not visible even if you get disconnected.

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
$ sudo apt update
$ sudo apt install screen
```

### Start Screen

To start a **Screen** session, simply type `screen` in your terminal.
Now that you have a screen session open, you can get a list of commands by typing:

```
Ctrl + a (Shift) ?
```

### Start Named Session

You can as well start a named session for example if you are running multiple screen sessions. To create a named session:

```bash
$ screen -S session_name
```

### Useful Screen Commands

> :bulb: **Tip:** You can use `man` to see a detailed documentation about `screen`.

To create a new window with shell

```
Ctrl + a + c
```

To list all windows

```
Ctrl + a + "
```

Switch to a window

```
Ctrl + a + 0..9
```

Rename a current window

```
Ctrl + a + A
```

### Window splitting

Split current region horizontally into two regions

```
Ctrl + a + S
```

Split current region vertically into two regions

```
Ctrl + a + |
```

Switch the input focus to the next regions

```
Ctrl + a + Tab
```

Toggle between the current and previous windows

```
Ctrl + a Ctrl + a
```

Close all regions except the current one

```
Ctrl + a + Q
```

Close the current region

```
Ctrl + a + X
```

### Detach from Screen session

You can detach from a `screen` session anytime by typing

```
Ctrl + a + d
```

The program running in the screen session will continue to run after you detach from the session.

### Reattach to a Screen session

To resume your `screen` session use the following command

```bash
$ screen -r
```

If you have multiple screen sessions running on your machine, you will need to append the screen session ID after the `r` switch.

To find the session ID list the current running `screen` sessions with

```console
$ screen -ls
```

The output will look like this

```console
There are screens on:
        20131.pts-0.hostname    (05/30/2022 12:43:27 AM)    (Detached)
        29062.pts-0.hostname    (05/30/2022 12:41:46 AM)    (Detached)
2 Sockets in /run/screen/S-root.
```

If you want to restore screen `29062.pts-0`, then type the following command

```bash
$ screen -r 29062
```
