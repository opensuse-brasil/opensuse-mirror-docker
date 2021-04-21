# sync

Rsync client that mirrors the desired content from openSUSE servers.

This service should run as a cron job in Swarm or Kubernetes.

## What will be mirrored?

You need to set what is going to be mirrored in `/etc/rsync-include.txt`.

`rsync-example.txt` contains a **working example** of content to be mirrored,
but you should review it and adapt to your needs.

By default, the rsync module used is `opensuse-full-with-factory`,
which has 3 TB.

If `/etc/rsync-include.txt` or if it's all inclusive (`*`) it will download
everything from `opensuse-full-with-factory`.

You can change the rsync module to `opensuse-hotstuff-160gb` for example,
or customize `/etc/rsync-include.txt` to clone anything you want from
`opensuse-full-really-everything-including-repositories`.

The `RSYNC_MODULE` setting and the `/etc/rsync-include.txt` file work together,
set them accordingly.

## Container Settings

### RSYNC_SERVER

The mirror server, `rsync.opensuse.org` or `stage.opensuse.org`.

Default: `rsync.opensuse.org`

### RSYNC_MODULE

The mirror module to use.

Default: `opensuse-full-with-factory`

### RSYNC_USER

The mirror user to authenticate.

Default: `opensuse`

### RSYNC_PASSWORD

The mirror password to authenticate.

Default: **Not Set**
