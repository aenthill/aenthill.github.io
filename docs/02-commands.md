---
title: Commands
---

[Aenthill](https://github.com/aenthill/aenthill) provides the <code>aenthill</code> command-line program, which contains many useful commands.

## init

[Aenthill](https://github.com/aenthill/aenthill) relies on an <code>aenthill.json</code> file (called *manifest*) which gathers all *aents* of your ecosystem.

You may create this file in your current directory by running:

```bash
$ aenthill init
```

## add

Once your *manifest* created, you may add *aents* by using:

```bash
$ aenthill add image [image...]
```

[Aenthill](https://github.com/aenthill/aenthill) will add them to your *manifest* and send the event <code>ADD</code> to them.

## rm

You may also remove *aents* by using:

```bash
$ aenthill rm image [image...]
```

[Aenthill](https://github.com/aenthill/aenthill) will remove them from your *manifest* and send the event <code>REMOVE</code> to them.