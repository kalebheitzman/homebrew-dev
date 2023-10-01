# Homebrew Dev Environment

There's something to be said for developing on virtual machines that are a one-to-one replica of production environments. I will never deny that.

But... there's also something to be said about using Homebrew for my development needs and it giving me the least amount of problems. Docker's endless configuration, Canonical's multipass mac firewall issue, UTM's gui cruft that I don't need, etc. This is my reminder doc about how I've set up homebrew to do web development.

## Basic wants, processes, and procedures

- Brew for installing packages like nginx, php, and mariadb
- A centralized code folder
- mkcert for locally-trusted development certificates
- Easy to start and stop daemonized services

Brew gives me all of the tools on macOS that I would expect when setting up a production server on Ubuntu. All code goes into `~/Developer` so I can easily get to everything in one spot. AND... I use `mkcert` to generate certificates that I can use locally by wiring them up in nginx. Being able to test https locally is essential.

Dead simple daemon control comes with `brew services` so I can launch web services and shut them down at will.

![brew services](images/brew-services.png)

## Installing Brew and some basic development tools

Homebrew, the missing [package manager](https://brew.sh/) for macOS (or linux).

```zsh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

This will install everything to the prefix `/opt/homebrew` including things like nginx/postgres configuration. On a typical Ubuntu sytem, you'll find nginx configuration at `/etc/nginx`. That same path becomes `/opt/homebrew/etc/nginx` on macOS.

**Initial Dev Environment setup**

Watch for any help messages you need to be aware of during install. These are the very basics for a LEMP environment using latest packages along with git for code repository management.

```zsh
brew install git mkcert dnsmasq nginx mariadb php
```

I use git heavily for development and dnsmasq to setup an automatic `.mbp` domain ending for development purposes.

Open `/opt/homebrew/etc/dnsmasq.conf` and add something similar to the address area. I'm using the a `.mbp` domain to indicate I'm developing on my macbook pro but you can change this to anything you like. Avoid choosing a TLD (top-level domain) suffix unless you know what you're doing like `.local`.

```conf
# Add domains which you want to force to an IP address here.
# The example below send any host in double-click.net to a local
# web-server.
#address=/double-click.net/127.0.0.1
address=/.mbp/127.0.0.1
```
