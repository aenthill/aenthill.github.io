---
title: Installation
---

[Aenthill](https://github.com/aenthill/aenthill) is distributed in a binary form and can be installed in many ways.

## Using wget

Find the binary corresponding to your architecture and install it using the following command:

```bash
$ wget -qO- https://github.com/aenthill/aenthill/releases/download/{{ version }}/aenthill_linux_{{ architecture }}.tar.gz | tar xvz -C .
$ sudo mv ./aenthill /usr/local/bin && chmod +x /usr/local/bin/aenthill
```

## Using homebrew

```bash
$ brew install aenthill/tap/aenthill
```

## Using Scoop

```bash
$ scoope bucket add aenthill https://github.com/aenthill/scoop-bucket.git
$ scoop install aenthill
```