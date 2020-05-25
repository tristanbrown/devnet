======
devnet
======

A docker network for hosting development infrastructure.

Install
=======

Coming soon

Dev Notes
=========

Port-forwarding formats:
- "host:container"
- "container" (randomly generates the host value in "host:container")
- Use expose: - "container" to document a port accessible in the container,
 but not on the host.
- Container ports are accessible within Docker networks by default.
