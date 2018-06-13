---
title: Installation
---

[Aenthill](https://github.com/aenthill/aenthill) is distributed in a binary form and
the only requirement is to have Docker installed and running on your host (always use the latest version).

In order to get <code>aenthill</code>, run the following command:

```bash
$ curl -sf https://raw.githubusercontent.com/aenthill/aenthill/master/install.sh | BINDIR=/usr/local/bin sh
```

This will install the latest release of [Aenthill](https://github.com/aenthill/aenthill) in the <code>/usr/local/bin</code>
directory.

**You may of course change the destination directory by updating the <code>BINDIR</code> value.**

If you want to install a specific version of [Aenthill](https://github.com/aenthill/aenthill), you may also run:

```bash
$ curl -sf https://raw.githubusercontent.com/aenthill/aenthill/master/install.sh | BINDIR=/usr/local/bin sh -s version
```

You may find all available versions in the [releases page](https://github.com/aenthill/aenthill/releases/).

The binary <code>aenthill</code> also let you update to the latest version with the following command:

```bash
$ aenthill upgrade [-t version]
```

Last but not least, verify installation with:

```bash
$ aenthill --version
```