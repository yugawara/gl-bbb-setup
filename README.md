Notes on BBB and Associated Servers
===================================

Other Dockerization Attempts
----------------------------

There appears to have been some work in the [BBB source repo][bbbsrc]
on Dockerizing the whole BBB system; see the `labs/docker`
subdirectory.

[bbbsrc]: https://github.com/bigbluebutton/bigbluebutton


Servers
-------

Rough overview of servers involved. (Probably lots of inaccuracies
here.) There may be many more; have a look at `labs/docker/` in the
source code which lists 14 locally-built images in the README along
with several more pre-built images (greenlight, mongodb, redis) in the
`docker-compose.yml`.

- nginx: proxy to other servers below
  - not Dockerized
  - HTTP on ports 80, 443
- BBB: video server
  - not Dockerized
  - ports ??,??: HTTP API (and human-usable pages?)
  - UDP on ports 16384-32768
- mongodb: Used by BBB to synchronize client state
  - not Dockerized
  - BBB install uses 3.4; probably we can use 3.6 from
    <https://hub.docker.com/_/mongo/>
  - ports ???
- coturn (optional): TURN and STUN server for NAT traversal
  - must be on "separate server" from BBB, with a separate hostname
  - port 443 TLS (conflicts with nginx)
  - port 3478 TCP/UDP coturn listening port
  - ports 49152-65535 UDP for relay
- Greenlight: interface to BBB API
  - allows multiple users with different permissions to access different
    parts of BBB API
  - port 127.0.0.1:5000 on host fowarding to port 80 in Docker container
- postgres:9.5
  - containerized PostgreSQL used by Greenlight
  - 127.0.0.1:5432:5432
