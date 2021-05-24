# Docker Swarm Deploy

Examples file for Swarm deployment

## Assumptions

- The host path where files are going to be stored is `/storage/opensuse`
- The owner of `/storage/opensuse` is the user:groud defined by `RSYNC_CHOWN`
- Your swarm cluster is empty
- Your load balancer/proxy/ingress will be Traefik
- You have a domain name (eg: `something.com`)

## What will be cloned?

There are some examples called `rsync-include-example-<n>.txt` that you can use,
but most likely, you want to customize it.

Use the command below to query opensuse servers and understand it better:

```bash
rsync -h --list-only rsync.opensuse.org::opensuse-full-with-factory/opensuse/
```

Use the command below to check how much space your `rsync-include.txt` will take:

```bash
rsync --stats --dry-run -h -rlpt rsync.opensuse.org::opensuse-full-with-factory/opensuse/ --include-from=rsync-include.txt
```

## Deployment

### Create volumes

Create a volume named `opensuse` that points to `/storage/opensuse`

`docker volume create --name opensuse --opt type=none --opt device=/storage/opensuse --opt o=bind`

Create a volume named `fancyindex` if you want to edit the HTMLs of your download server.

`docker volume create fancyindex`

### Create networks

Create a network for Traefik and all services.

`docker network create --driver overlay traefik`

### Create configurations

Create `rsync-include` that will hold what you want to mirror.

`docker config create rsync-include rsync-include.txt`

### Deploy to swarm

Deploy Traefik.

`docker stack deploy -c traefik.yml traefik`

Deploy the cron job runner.

`docker stack deploy -c cron.yml cron`

Deploy mirror services.

`docker stack deploy -c services.yml opensuse-mirror`

### Volumes

### /srv/pub/opensuse

This volume is used by Clone, Content and Download services.

All binaries, RPMs, and repo metadata will live in this location.

> You need to mount the same volume in each service.
