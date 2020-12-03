# A set of basic docker-based appliances for GNS3

This repository contains appliances that can be installed as-is on GNS3, saving
you the hassle of building a base image yourself.

To make things easier for non-docker gurus, the appliances run systemd,
allowing the starting of services just like any other machine.


## The host

The host is a centos 8 base image, with common networking tools like
`iproute2` and `bind-utils` installed.

The following directories are persisted through VOLUMEs:
    * `/etc/sysconfig`

## The server

Exactly like the host, but ships with NGINX enabled, that returns a JSON
containing the client's IP and the server hostname on each query.

When symlinks will be handled in project exports, this appliance will probably disappear.

The following directories are persisted through VOLUMEs:
    * `/etc/sysconfig`

## The router

The router is very similar to the host image, but also ships with the ISC DHCP
server, BIND, radvd, and the BIRD2 routing daemon.

The following directories are persisted through VOLUMEs:
    * `/etc/sysconfig`
    * `/etc/bird` (an override moves the bird.conf from `/etc/` to this directory)


### Acknowledgements

These images were created for the networking classes I teach at EPITA. Feel
free to use them if you find them useful, or suggest improvements!

