# A home server set up with Traefik

[Traefik]: https://docs.traefik.io
[Docker Compose]: https://docs.docker.com/compose/

This is an example of setting up more or less the same services as was done using Ansible in [playbooks](https://github.com/aheimsbakk/playbooks) with [Docker Compose][] and [Traefik][].

Traefik in a nutshell.

```
Endpoint -> Routers listen enpoint(s) -> Middelwares applyed -> Service, e.g. container
```

## Test

Test the setup with `vagrant up`. This should create the services below.

* [Gitlab registry](https://registry.10.0.0.10.xip.io:5487/v2)
* [Gitlab](https://git.10.0.0.10.xip.io)
* [Gotify](https://gotify.10.0.0.10.xip.io), default username `admin` and password `admin`
* [Munin](https://munin.10.0.0.10.xip.io)
* [Nextcloud](https://futhark.10.0.0.10.xip.io), default username `admin` and password `password`
* [Traefik Dashboard](https://traefik.10.0.0.10.xip.io)

## Customize

1. Override template with your own customizations.
    ```bash
    cp docker-compose.override.yml.template docker-compose.override.yml
    vim docker-compose.override.yml
    ```
2. Override Docker Compose environment variables.
    ```bash
    cp .env.template .env
    vim .env
    ```

## Caveats

Could not reproduce with only environment variable configuration of Traefik. I suspect a bug in Traefik.

<!---
# vim: set spell spelllang=en:
-->
