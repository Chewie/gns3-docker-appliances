# A set of basic docker-based appliances for GNS3

This repository contains appliances that can be installed as-is on GNS3, saving
you the hassle of building a base image yourself.

To make things easier for non-docker gurus, the appliances run systemd,
allowing the starting of services just like any other machine.

## The host

The host is a centos 7 base image, with common networking tools like
`iproute2` and `bind-utils` installed.

## The router

The router is very similar to the host image, but also ships with the ISC DHCP
server, BIND, and the BIRD2 routing daemon.


### Acknowledgements

These images were created for the networking classes I teach at EPITA. Feel
free to use them if you find them useful, or suggest improvements!

