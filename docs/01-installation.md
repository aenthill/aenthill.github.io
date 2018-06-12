---
title: Installation
---

[Aenthill](https://github.com/aenthill/aenthill) is distributed in a binary form and can be installed in many ways.
The only requirement is to have *Docker* installed and running on your host (always use the latest version).

## Using wget

```bash
$ wget -qO- https://github.com/aenthill/aenthill/releases/download/version/binary.tar.gz | tar xvz -C .
$ sudo mv ./aenthill /usr/local/bin && chmod +x /usr/local/bin/aenthill
```

You may find available binaries in the [releases page](https://github.com/aenthill/aenthill/releases/).

## Using homebrew

```bash
$ brew install aenthill/tap/aenthill
```

## Using Scoop

```bash
$ scoope bucket add aenthill https://github.com/aenthill/scoop-bucket.git
$ scoop install aenthill
```