---
title: Hermes
---

[Hermes](https://github.com/aenthill/hermes) is a tool which can be used directly inside an *aent* to send events.

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

It uses the environment variable <code>PHEROMONE_FROM</code> to know which *aent* to reply to.