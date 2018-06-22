---
title: How does it work?
---

As explained before, an ecosystem of *aents* is working by sending events to each other.

An event may be sent by [Aenthill](https://github.com/aenthill/aenthill) directly or by another *aent*.

Let's start with [Aenthill](https://github.com/aenthill/aenthill):

```bash
$ aenthill add aenthill/cassandra
```

This command will send the event <code>ADD</code> to the *aent* <code>aenthill/cassandra</code> by running:

```bash
$ docker run -ti --rm
-v "/var/run/docker.sock:/var/run/docker.sock"
-v "HostProjectDir:/aenthill"
-e "PHEROMONE_FROM_IMAGE_NAME="
-e "PHEROMONE_FROM_CONTAINER_ID="
-e "PHEROMONE_WHOAMI=aenthill/cassandra"
-e "PHEROMONE_HOST_PROJECT_DIR=/host/project/dir"
-e "PHEROMONE_CONTAINER_PROJECT_DIR=/aenthill"
-e "PHEROMONE_LOG_LEVEL=ERROR"
aenthill/cassandra aent "ADD"
```

There are several things to note:

* [Aenthill](https://github.com/aenthill/aenthill) starts the *aent* <code>aenthill/cassandra</code> by calling its binary <code>aent</code> with the event name as first argument
* It mounts the current host working directory <code>/host/project/dir</code> to the *aent* directory <code>/aenthill</code>
* It binds the host Docker socket
* It populates some environment variables

Those environment variables allows the *aent* to understand within which context it has been awaken.

<details>
  <summary><code>PHEROMONE_FROM_IMAGE_NAME</code></summary>
  <p>The event sender image name (empty if sended by [Aenthill](https://github.com/aenthill/aenthill)).</p>
</details>

<details>
  <summary><code>PHEROMONE_FROM_CONTAINER_ID</code></summary>
  <p>The event sender container ID (empty if sended by [Aenthill](https://github.com/aenthill/aenthill)).</p>
</details>

<details>
  <summary><code>PHEROMONE_WHOAMI</code></summary>
  <p>The event recipient image name (the *aent* itself).</p>
</details>

<details>
  <summary><code>HOSTNAME</code></summary>
  <p>The event recipient container ID (populated by Docker).</p>
</details>

<details>
  <summary><code>PHEROMONE_HOST_PROJECT_DIR</code></summary>
  <p>The host project directory.</p>
</details>

<details>
  <summary><code>PHEROMONE_CONTAINER_PROJECT_DIR</code></summary>
  <p>The path of the project directory in the *aent*.</p>
</details>

<details>
  <summary><code>PHEROMONE_LOG_LEVEL</code></summary>
  <p>The log level as defined by the user with [Aenthill](https://github.com/aenthill/aenthill).</p>
</details>

## aent

As you understand, an *aent* is a Docker image which has a binary called <code>aent</code>. This binary should accept two arguments:

* The event name (a string)
* The payload (a string too) which contains the data associated to the event

The last argument has to be optional (for instance, it is never filled by [Aenthill](https://github.com/aenthill/aenthill)).

**The entire process will stop if the binary <code>aent</code> returns an exit code different than 0.**

You may now wondering how an *aent* is able to communicate with another *aent*.

There are actually two cases:

1. dispatching an event to all *aents*
2. replying to an *aent*

### Dispatching an event

The *aent* parses the *manifest* (located at <code>${PHEROMONE_CONTAINER_PROJECT_DIR}/aenthill.json</code>) to retrieve all available *aents*.
Then it loops over them and runs the following Docker command:

```bash
$ docker run -ti --rm
-v "/var/run/docker.sock:/var/run/docker.sock"
-v "${PHEROMONE_HOST_PROJECT_DIR}:/aenthill"
-e "PHEROMONE_FROM_IMAGE_NAME=${PHEROMONE_WHOAMI}"
-e "PHEROMONE_FROM_CONTAINER_ID=${HOSTNAME}"
-e "PHEROMONE_WHOAMI=the_recipient_aent_image_name"
-e "PHEROMONE_HOST_PROJECT_DIR=${PHEROMONE_HOST_PROJECT_DIR}"
-e "PHEROMONE_CONTAINER_PROJECT_DIR=/aenthill"
-e "PHEROMONE_LOG_LEVEL=${PHEROMONE_LOG_LEVEL}"
the_recipient_aent_image_name aent "AN_EVENT" ["A_PAYLOAD"]
```

Notice that your events may be associated with a payload.

### Replying to an event

If another *aent* has awaken your *aent*, you may also reply to it by running:

```bash
$ docker exec -ti
${PHEROMONE_FROM_CONTAINER_ID} aent "AN_EVENT" ["A_PAYLOAD"]
```

Too much complicated? Don't worry, we provide [Hermes](https://github.com/aenthill/hermes) to help you!