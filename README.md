# Environment - Production

This repository contains a Docker Compose environment to spin-up the complete application stack in a production environment.

For the `files` container, you'll need to acquire the static assets to serve, so make sure to check the [assets](https://github.com/starpep-web/assets) repo for more information on how to acquire those files.

The services are exposed through a [Traefik](https://traefik.io/traefik/) reverse proxy and served through a [Cloudflare Tunnel](https://www.cloudflare.com) to avoid having to open any ports, these services are provided by the `proxy` and `tunnel` containers respectively.
Feel free to edit or remove these containers if you wish to deploy this application in a different environment.

## Requirements

In order to develop for this repository you need:

* [Docker](https://www.docker.com/products/docker-desktop/)
* A [Cloudflare](https://www.cloudflare.com) account to use their tunneling service.

## Configuration

First, clone this repository:

```bash
git clone https://github.com/starpep-web/env-production
```

Create an `.env` file with the following contents:

```text
TIMEZONE=America/Guayaquil

CLOUDFLARE_TUNNEL_TOKEN=

DOMAIN_PORTAINER=
DOMAIN_PROXY=
DOMAIN_FILES_SERVER=
DOMAIN_CMS=
DOMAIN_WEB=

SHARED_INTERNAL_SECRET=

ASSETS_FILES_LOCATION=
ASSETS_TEMP_ARTIFACTS_LOCATION=

CMS_APP_KEYS=
CMS_API_TOKEN_SALT=
CMS_ADMIN_JWT_SECRET=
CMS_TRANSFER_TOKEN_SALT=
CMS_JWT_SECRET=

WEB_PUBLIC_URL=
WEB_PUBLIC_ASSETS_URL
WEB_CMS_TOKEN=
WEB_CMS_URL=
```

| **Variable**                     | **Description**                                                                                                                                                                                                     | **Example Value**               |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------|
| `TIMEZONE`                       | The UNIX timezone to use across services.                                                                                                                                                                           | `America/Guayaquil`             |
| `CLOUDFLARE_TUNNEL_TOKEN`        | The Cloudflare tunnel token acquired when creating a new tunnel in [Zero Trust Dashboard](http://one.dash.cloudflare.com).                                                                                          | `JWT_TOKEN_HERE`                |
| `DOMAIN_PORTAINER`               | The domain from which the Portainer instance is accessible from.                                                                                                                                                    | `docker.starpepweb.org`         |
| `DOMAIN_PROXY`                   | The domain from which the Traefik proxy dashboard is accessible from.                                                                                                                                               | `proxy.starpepweb.org`          |
| `DOMAIN_FILES_SERVER`            | The domain from which the `static-file-server` service is accessible from.                                                                                                                                          | `dl.starpepweb.org`             |
| `DOMAIN_CMS`                     | The domain from which the Strapi CMS is accessible from.                                                                                                                                                            | `cms.starpepweb.org`            |
| `DOMAIN_WEB`                     | The domain from which the main application is accessible from.                                                                                                                                                      | `starpepweb.org`                |
| `SHARED_INTERNAL_SECRET`         | A secret value set by you to be used as a secret for internal messaging between services.                                                                                                                           | `SOME_SECRET_VALUE`             |
| `ASSETS_FILES_LOCATION`          | The absolute path in the host machine where the [assets](https://github.com/starpep-web/assets) are located.                                                                                                        | `/home/user/assets/files`       |
| `ASSETS_TEMP_ARTIFACTS_LOCATION` | The absolute path in the host machine where the artifacts (for example, search exports) are located.                                                                                                                | `/home/user/assets/artifacts`   |
| `CMS_APP_KEYS`                   | The app keys used by Strapi. You can make up these secrets yourself.                                                                                                                                                | `"toBeModified1,toBeModified2"` |
| `CMS_API_TOKEN_SALT`             | The API token salt used by Strapi. You can make up this secret yourself.                                                                                                                                            | `tobemodified`                  |
| `CMS_ADMIN_JWT_SECRET`           | The admin JWT token used by Strapi. You can make up this secret yourself.                                                                                                                                           | `tobemodified`                  |
| `CMS_TRANSFER_TOKEN_SALT`        | The transfer token salt used by Strapi. You can make up this secret yourself.                                                                                                                                       | `tobemodified`                  |
| `CMS_JWT_SECRET`                 | The JWT secret used by Strapi. You can make up this secret yourself.                                                                                                                                                | `tobemodified`                  |
| `WEB_PUBLIC_URL`                 | The public URL from which the web application is accessible from.                                                                                                                                                   | `https://starpepweb.org`        |
| `WEB_PUBLIC_ASSETS_URL`          | The public URL from which the `static-file-server` service is accessible from.                                                                                                                                      | `https://dl.starpepweb.org`     |
| `WEB_CMS_TOKEN`                  | The Strapi token used to query the GraphQL CMS service. Check the CMS's [first time setup](https://github.com/starpep-web/web-cms?tab=readme-ov-file#first-time-setup) for more information on how to acquire this. | `JWT_TOKEN_HERE`                |
| `WEB_CMS_URL`                    | The public URL from which the CMS is accessible from.                                                                                                                                                               | `https://cms.starpepweb.org`    |

Start the environment:

```bash
docker compose up -d
```

And that's it, the application will now be up and served by the reverse proxy.
