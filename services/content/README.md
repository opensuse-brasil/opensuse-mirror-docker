# Content

An rsync server that allows openSUSE mirror scanner to query your mirrored data.

This server will provide an rsync module called `opensuse` containing all files in `/srv/pub/opensuse`.

The scanning happens from `195.135.220.0/22`.

> Recomendation: Restrict access to the IP above in your network security groups, server firewall or iptables.

## File Configuration

### /etc/rsyncd.conf

Default configuration has all the parameters required for mirror scanner to work.

Check the [Linux man page](https://linux.die.net/man/5/rsyncd.conf) for more information.

## Volumes

### /srv/pub/opensuse

The path used for opensuse module in rsync.

You need mount this path to the same host path used by Clone service.

## Logs

### /var/log/rsyncd.log

The rsync access and error log.

Redirects to Docker StdOut.
