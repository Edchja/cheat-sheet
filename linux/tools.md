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
