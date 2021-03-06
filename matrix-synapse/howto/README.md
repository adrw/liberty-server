# Matrix-Synapse

![Network Map of Matrix-Synapse behind Traefik](matrix-telegram-docker.svg)

Matrix synapse has to be started once with the "generate"-command. Run this from your /path/to/my/mydatafolder/matrix-synapse.

## First start: generate the config files

```bash
  docker run -it --rm \
    -v $PWD/data:/data \
    -e SYNAPSE_SERVER_NAME=your.domain.name \
    -e SYNAPSE_REPORT_STATS=yes \
    matrixdotorg/synapse:latest generate
```

## Second start: use docker run

Use ```docker ps --all```-command to list all your containers. Run the matrix-synapse container.

If you like to use matrix-synapse behind the traefik v2 reverse proxy, you have to either add all the necessary labels or to delete the existing container and set up a new one with docker-compose.

## If configuration already exists: Start with docker-compose

```
docker-compose up -d
```

## Set up your DNS

Matrix-Synapse by default communicates over Port 8001. If you want to pipe it through SSL port 443 of your Reverse Proxy, you need to add a "SRV record" to your DNS-Setup. For Matrix this entry looks like this:

```
SRV: _matrix._tcp.matrix 10 5 443 subdomain.domain.tld.
```

This tells clients and other federation servers to communicate through port 443/tcp when accessing your Matrix server.
The details, how to set up an SRV record is different for each hoster or DNS provider.

## Test your setup

With the Matrix Federation Tester you can easily find out if your DNS-Setup works: <https://federationtester.matrix.org/>
