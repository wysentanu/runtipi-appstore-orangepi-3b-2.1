# Overview
Fleet is an open-source endpoint management platform for osquery, MDM, software management, patching, scripts, and vulnerability workflows.

This Runtipi app follows Fleet's official Docker Compose guide with Fleet, MySQL, Redis, and a one-time init container that fixes Fleet volume ownership before the server starts.

## Important Notes
- **Architecture**: Fleet's official Docker image is currently published as `linux/amd64`. This app is marked amd64-only. On Orange Pi / arm64 hosts, it requires Docker amd64 emulation configured at the Docker host level.
- **TLS**: Fleet is configured with `FLEET_SERVER_TLS=false` so Runtipi or another reverse proxy can terminate HTTPS. Fleet MDM enrollment needs a trusted HTTPS URL when used outside a local test setup.
- **First setup**: Open Fleet after install and follow the setup screen to create the first admin account and organization.
- **Data persistence**: MySQL data, Redis data, Fleet data, logs, and vulnerability databases are stored under `${APP_DATA_DIR}/data`.
- **Optional license**: Leave `FLEET_LICENSE_KEY` blank to use Fleet Free.
- **Optional S3**: Configure the S3 fields only if you want Fleet to store software installers in S3-compatible storage.

## Configurable Environment Variables
- `MYSQL_ROOT_PASSWORD` - Random MySQL root password.
- `MYSQL_PASSWORD` - Random password for the `fleet` MySQL user.
- `FLEET_SERVER_PRIVATE_KEY` - Random base64 key used by Fleet to encrypt session tokens.
- `FLEET_LICENSE_KEY` - Optional Fleet Premium license key.
- `FLEET_SESSION_DURATION` - Fleet session duration, default `24h`.
- `FLEET_LOGGING_JSON` - Enable JSON logs.
- `FLEET_OSQUERY_LABEL_UPDATE_INTERVAL` - Label refresh interval, default `1h`.
- `FLEET_VULNERABILITIES_PERIODICITY` - Vulnerability check interval, default `1h`.
- `FLEET_S3_SOFTWARE_INSTALLERS_BUCKET` - Optional S3 bucket for software installers.
- `FLEET_S3_SOFTWARE_INSTALLERS_ACCESS_KEY_ID` - Optional S3 access key ID.
- `FLEET_S3_SOFTWARE_INSTALLERS_SECRET_ACCESS_KEY` - Optional S3 secret access key.
- `FLEET_S3_SOFTWARE_INSTALLERS_FORCE_S3_PATH_STYLE` - Enable path-style S3 requests for compatible storage.
- `FLEET_S3_SOFTWARE_INSTALLERS_ENDPOINT_URL` - Optional S3-compatible endpoint URL.
- `FLEET_S3_SOFTWARE_INSTALLERS_REGION` - Optional S3 region.

## Links:
- [Fleet Website](https://fleetdm.com)
- [Fleet GitHub Repository](https://github.com/fleetdm/fleet)
- [Docker Compose Deployment Guide](https://fleetdm.com/guides/deploy-fleet-on-docker-compose)
- [Fleet Server Configuration](https://fleetdm.com/docs/deploying/configuration)

## Preview
![Fleet dashboard](https://fleetdm.com/images/press-kit/press-kit-fleet-screenshots-preview-600x336@2x.png)
