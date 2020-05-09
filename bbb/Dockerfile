FROM ubuntu:16.04

#   XXX speed debugging
#RUN apt-get update && apt-get -y dist-upgrade

COPY setup-image /tmp/
RUN /bin/bash /tmp/setup-image

COPY newsetup /tmp/
RUN /bin/bash /tmp/setup-wip

#   Probably we'll use host networking instead of
#   mapping ports 80, 443, 16384-32768/udp.
