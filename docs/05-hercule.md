---
title: Hercule
---

[Hercule](https://github.com/aenthill/hercule) is a tool for manipulating a *manifest* inside an *aent*.


## Installation

Below an example of <code>Dockerfile</code>: 

```
FROM alpine:3.7

[...]

# Installs Hercule.
ENV HERCULE_VERSION "latest version"
RUN wget -qO- https://github.com/aenthill/hercule/releases/download/$HERCULE_VERSION/hercule_linux_amd64.tar.gz | tar xvz -C . &&\
    mv ./hercule /usr/bin &&\
    rm -f LICENSE README.md

[...]
```

## Commands

### set:handled-events

```bash
$ hercule set:handled-events [event...]
```

This command allows your *aent* to specify which events it handles by updating the *manifest*.

Next time [Hermes](https://github.com/aenthill/hermes) will dispatch an event, your *aent* will be awaken only if it handles it.

**If no event given, your *aent* will always be awaken by incoming events!**

This command should be called when your *aent* is awaken by the <code>ADD</code> event from [Aenthill](https://github.com/aenthill/aenthill)