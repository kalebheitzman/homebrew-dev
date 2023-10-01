# Web Development Environment using Homebrew

There's something to be said for developing on virtual machines that are a one-to-one replica of production environments. I will never deny that.

But... there's also something to be said about using Homebrew for my development needs and it giving me the least amount of problems. Docker's endless configuration, Canonical's multipass mac firewall issue, UTM's gui cruft that I don't need, etc. This is my reminder doc about how I've set up homebrew to do web development.

## Basic wants, processes, and procedures

I like to put everything in `~/Developer` so I can easily get to everything in one spot.

```bash
mkdir ~/Developer
```

## Installing Brew and some basic development tools

Homebrew, the missing [package manager](https://brew.sh/) for macOS (or linux).

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

This will install everything to `/opt/homebrew` including things like nginx/postgres configuration.
