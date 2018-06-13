---
title: Introduction
---

[Aenthill](https://github.com/aenthill/aenthill) is a solution for allowing Docker containers to communicate with each other in order to fulfill a task in the current host directory.

Each of those Docker containers (called *aent*) is not aware of its peers. It is however able to receive and communicate events to them. In other words, an *aent* is not necessarily smart
but it shares a part of the task to handle like an ant within its colony.