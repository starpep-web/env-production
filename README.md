# docker-compose-stack

A Docker Compose stack to deploy this application.

## Requirements

In order to deploy the full application stack you need to have [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/) installed in your machine.

## Running

Clone this repository:

```text
git clone https://github.com/WebPeptide/docker-compose-stack
```

And start the stack:

```text
docker-compose up -d
```

Or with:

```text
docker compose up -d
```

> Both commands depends on the version of Docker Compose that you have installed, both do exactly the same thing.

You should now have the web application exposed on port 20000 available at http://localhost:20000

Both the datamining API and the database aren't exposed to the host machine and are only accessible by the services inside the stack.
