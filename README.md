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

This will install everything to the prefix `/opt/homebrew` including things like nginx/postgres configuration. On a typical Ubuntu sytem, you'll find nginx configuration at `/etc/nginx`. This path becomes `/opt/homebrew/etc/nginx` on macOS.

## Using mkcert to generate local development certificates

I use `mkcert` to generate local development certicates and add entries to `/etc/hosts` to map domains to nginx. You can setup `dnsmasq` to resolve a domain suffix of your choice but I have avoided this because there have been issues with people masking entire TLDs like `.local` and `.dev` and messing up thier networks and access to websites. I personally like using `.dev` mapped to my hosts file but I avoid using domains that map to real world domains like [wordpress.dev](https://wordpress.dev).

```zsh
brew install mkcert
mkcert wordpress.local "*.wordpress.local"
```

```zsh
sudo nano /etc/hosts
```

![hosts](images/hosts-etc.png)

### Basic LEMP environment setup

Watch for any help messages you need to be aware of during install. These are the very basics for a LEMP environment using latest packages along with git for code repository management.

```zsh
brew install git nginx mariadb php
brew services start nginx
brew services start mariadb
brew services start php
```
