---
title: Hermes
---

[Hermes](https://github.com/aenthill/hermes) is a tool which can be used directly inside an *Aent* to send events.

Its goal is to ease the communication of your *Aent* with others *Aents* of your ecosystem.

## Installation

Below an example of <code>Dockerfile</code>: 

```
FROM alpine:3.7

[...]

# Required for Hermes to know which interpret to use when calling the Docker client binary.
ENV SHELL "/bin/sh"

# Installs Docker client.
ENV DOCKER_VERSION "18.03.1-ce"
RUN wget -qO- https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz | tar xvz -C . &&\
    mv ./docker/docker /usr/bin &&\
    rm -rf ./docker

# Installs Hermes.
ENV HERMES_VERSION "latest version"
RUN wget -qO- https://github.com/aenthill/hermes/releases/download/$HERMES_VERSION/hermes_linux_amd64.tar.gz | tar xvz -C . &&\
    mv ./hermes /usr/bin &&\
    rm -f LICENSE README.md

[...]
```

## Commands

### dispatch

```bash
$ hermes dispatch event [payload]
```

[Hermes](https://github.com/aenthill/hermes) will send the given event and payload to all *Aents* in the *Manifest* which handles it.

### reply

```bash
$ hermes reply event [payload]
```

[Hermes](https://github.com/aenthill/hermes) will send the given event and payload back to the *Aent* which which has awaken yours.

It uses the environment variable <code>PHEROMONE_FROM</code> to know which *Aent* to reply to.