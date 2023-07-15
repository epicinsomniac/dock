# Codex
Codex is a web server comic book browser and reader.

https://hub.docker.com/r/ajslater/codex


# docker-compose.yaml

```
services:
  codex:
      env_file: .env
      image: docker.io/ajslater/codex
      container_name: codex
      volumes:
          - <host path to data>:/config
          - <host path to comics>:/comics:ro
      ports:
          - 9810:9810
      restart: on-failure
```
#  Environment Variables

PUID: Sets the UID for the default user on startup

PGID: Sets the GID for the default user on startup

LOGLEVEL will change how verbose codex's logging is. Valid values are ERROR, WARNING, INFO, VERBOSE, DEBUG. The default is INFO.

TIMEZONE or TZ will explicitly the timezone in long format (e.g. "America/Los Angeles"). This is mostly useful inside Docker because codex cannot automatically detect the host machine's timezone.

CODEX_CONFIG_DIR will set the path to codex config directory. Defaults to $CWD/config

CODEX_RESET_ADMIN=1 will reset the admin user and its password to defaults when codex starts.

CODEX_SKIP_INTEGRITY_CHECK will skip the database integrity repair that runs when codex starts.
