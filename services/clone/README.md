# Clone

An rsync client that mirrors the desired content from openSUSE servers.

This service should run as a cron job in Swarm or Kubernetes, it is not a daemon.

## File Configuration

### /etc/rsync-include.txt

You need to set what is going to be mirrored in `/etc/rsync-include.txt`.

By default, the rsync module used is `opensuse-full-with-factory`,
which is currently 3 TB.

If `/etc/rsync-include.txt` is empty or if it's all inclusive (`*`) it will download
everything from `opensuse-full-with-factory`.

You can change the rsync module to `opensuse-hotstuff-160gb` for example,
or customize `/etc/rsync-include.txt` to clone anything you want from
`opensuse-full-really-everything-including-repositories` or another module.

The `RSYNC_MODULE` env var and the `/etc/rsync-include.txt` file work together,
set them accordingly.

## Environment Variables

### RSYNC_SERVER

The mirror server, should be `rsync.opensuse.org` or `stage.opensuse.org`.

Default: `rsync.opensuse.org`

### RSYNC_MODULE

The mirror module to use.
Check available modules [here](https://mirrors.opensuse.org/list/rsyncinfo-stage.o.o.txt).

Default: `opensuse-full-with-factory`

### RSYNC_USER

The mirror user to authenticate.

Default: `opensuse`

### RSYNC_PASSWORD

The mirror password to authenticate (stage mirror only).

Default: **Not Set**

### RSYNC_CHOWN

The `user:group` that will own the files.

Default: `1000:1000`

## Volumes

### /srv/pub/opensuse

The path where all synced files (rpms, isos and metadata) will be placed.

You **MUST** mount this path to a path in the host machine.

## Logs

### /var/log/rsync.log

The rsync clone log.

Redirects to Docker StdOut.
