---
title: How does it work?
---

As explained before, an ecosystem of *Aents* is working by sending events to each other.

An event may be sent by [Aenthill](https://github.com/aenthill/aenthill) directly or by another *Aent*.

Let start with [Aenthill](https://github.com/aenthill/aenthill):

```bash
$ aenthill add aenthill/cassandra
```

This command will send the event <code>ADD</code> to the *Aent* <code>aenthill/cassandra</code> by running:

```bash
$ docker run -ti --rm
-v "/var/run/docker.sock:/var/run/docker.sock"
-v "/host/project/dir:/aenthill"
-e "PHEROMONE_FROM="
-e "PHEROMONE_WHOAMI=aenthill/cassandra"
-e "PHEROMONE_HOST_PROJECT_DIR=/host/project/dir"
-e "PHEROMONE_CONTAINER_PROJECT_DIR=/aenthill"
-e "PHEROMONE_LOG_LEVEL=INFO"
aenthill/cassandra aent ADD
```

There are several things to note:

* [Aenthill](https://github.com/aenthill/aenthill) starts the *Aent* <code>aenthill/cassandra</code> by calling its binary <code>aent</code> with the event name as first argument
* It mounts the current project directory (<code>/host/project/dir</code>) to the *Aent* directory <code>/aenthill</code>
* It binds the host Docker socket (more on that later)
* Its populates some environment variables

