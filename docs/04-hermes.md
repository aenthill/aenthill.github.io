---
title: Hermes
---

[Hermes](https://github.com/aenthill/hermes) is a tool which can be used directly inside an *aent* 
for sending events and for manipulating the *manifest*.

Its goal is to ease the communication of your *aent* with others *aents* of your ecosystem.

## Installation

Below an example of <code>Dockerfile</code>: 

```
FROM alpine:3.7

[...]

# Required for Hermes to know which interpreter to use when calling the Docker client binary.
ENV SHELL "/bin/sh"

# Installs Docker client.
ENV DOCKER_VERSION "18.03.1-ce"
RUN wget -qO- https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz | tar xvz -C . &&\
    mv ./docker/docker /usr/bin &&\
    rm -rf ./docker

# Installs Hermes. You may find all available versions in the releases page: https://github.com/aenthill/hermes/releases/.
ENV HERMES_VERSION "version"
RUN curl -sf https://raw.githubusercontent.com/aenthill/hermes/master/install.sh | BINDIR=/usr/bin sh -s $HERMES_VERSION

[...]
```

## Commands

### dispatch

```bash
$ hermes dispatch event [payload]
```

[Hermes](https://github.com/aenthill/hermes) will send the given event and payload to all *aents* in the *manifest* which handles it.

### reply

```bash
$ hermes reply event [payload]
```

[Hermes](https://github.com/aenthill/hermes) will send the given event and payload back to the *aent* which which has awaken yours.

It uses the environment variable <code>PHEROMONE_FROM_CONTAINER_ID</code> to know which *aent* to reply to.

### set:dependencies

```bash
$ hermes set:dependencies image [images...]
```

This command works almost the same as the add command from [Aenthill](https://github.com/aenthill/aenthill). 
Only difference being that if an *aent* already exists in the *manifest*, the event <code>ADD</code> will not be sent to it.

### set:handled-events

```bash
$ hermes set:handled-events [events...]
```

This command allows your *aent* to specify which events it handles by updating the *manifest*.

Next time [Hermes](https://github.com/aenthill/hermes) will dispatch an event from another *aent*, 
your *aent* will be awaken only if it handles it.

**If no event given, your *aent* will always be awaken by incoming events!**

This command should be called when your *aent* is awaken by the <code>ADD</code> event from [Aenthill](https://github.com/aenthill/aenthill).