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

- [Install Screen]()
- [Start Screen]()
- [Start Named Screen]()
- [Useful Screen Commands]()

**Screen** is a terminal multiplexer. In other words, it means that you can can start a screen session and then open any number of windows (virtual terminals) inside that session. Processes running in Screen will continue to run when their window is not visible even if you get disconnected.

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
