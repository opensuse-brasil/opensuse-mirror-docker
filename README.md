# opensuse-mirror-docker

openSUSE Mirror Docker Image

## About

* [Check out the current mirror server list](https://mirrors.opensuse.org/)
* [Become a mirror](https://en.opensuse.org/openSUSE:Mirror_infrastructure)

## Services

### download

Nginx that act like a download server for mirrored content.

Similar to [download.opensuse.org](http://download.opensuse.org/)

### info

Rsync daemon to allow openSUSE mirror scanner to query information about mirrored content.

### sync

Rsync client that mirrors the desired content from openSUSE servers.

## Volumes

### /srv/pub/opensuse

This path used by rsync and nginx.

All binaries, RPMs, and repo metadata will live in this location.

> You need to mount the same volume in each service.
