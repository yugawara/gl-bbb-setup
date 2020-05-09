Notes on BBB and Associated Servers
===================================

Rough overview of servers involved. (Probably lots of inaccuracies here.)

- nginx: proxy to other servers below
  - not Dockerized
  - HTTP on ports 80, 443
- BBB: video server
  - not Dockerized
  - ports ??,??: HTTP API (and human-usable pages?)
  - UDP on ports 16384-32768
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
