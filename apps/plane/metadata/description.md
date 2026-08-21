# Overview

Plane Community Edition is an open-source project management platform for teams. It includes work items, cycles, modules, pages, project views, and real-time collaboration.

This Runtipi app packages Plane's official Community Edition Docker Compose stack. It runs the frontend services, API, background workers, database migration job, PostgreSQL, Valkey, RabbitMQ, MinIO, and Plane's internal reverse proxy together.

## Important notes

- The bundled `proxy` service is the Runtipi main service. It routes the frontend, API, admin, public spaces, WebSocket, and upload paths.
- Runtipi handles the external application route and TLS. Plane's proxy listens on HTTP port 80 inside the app network.
- Runtipi reserves host port 8085 for local access by default; expose the app through Runtipi's domain routing when available.
- The first launch runs Plane's database migrator before the API and workers become available.
- Plane's Community Edition is licensed under AGPL-3.0.
- Plane is a substantial multi-service stack. Allow enough memory and storage for PostgreSQL, uploads, logs, and message queues.

## Persistent data

All persistent data is stored below `${DATA_FOLDER_HOST}/AppData/plane`, including:

- `postgres` - PostgreSQL data
- `redis` - Valkey data
- `rabbitmq` - RabbitMQ data
- `uploads` - MinIO object storage
- `logs-api`, `logs-worker`, `logs-beat-worker`, and `logs-migrator` - service logs
- `proxy-config` and `proxy-data` - Plane proxy configuration and state

The included `docker-compose.user_config.yml` supplies the migrator's external
log path and keeps that one-shot job from restarting after it exits; apply that
override in Runtipi before starting the app.

Use Runtipi's backup facilities before uninstalling or upgrading. Removing the app deletes its app data.

## Configurable secrets

Runtipi generates secure values for:

- `POSTGRES_PASSWORD`
- `RABBITMQ_PASSWORD`
- `AWS_SECRET_ACCESS_KEY`
- `SECRET_KEY`
- `LIVE_SERVER_SECRET_KEY`

The application URL and protocol are provided by Runtipi through `${APP_DOMAIN}` and `${APP_PROTOCOL}`.

## Links

- [Plane website](https://plane.so)
- [Plane GitHub repository](https://github.com/makeplane/plane)
- [Plane Community Edition documentation](https://developers.plane.so/self-hosting/methods/docker-compose)
- [Plane environment variables](https://developers.plane.so/self-hosting/govern/environment-variables)
