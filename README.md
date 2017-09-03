# hub.docker.com/tiredofit/nginx-proxy-cloudflare-companion

# Introduction

Dockerfile to build a Container to automatically update Cloudflare DNS records upon container start. A time saver if you are regularly moving containers around to different systems.

* This Container uses a [customized Alpine Linux base](https://hub.docker.com/r/tiredofit/alpine) which includes [s6 overlay](https://github.com/just-containers/s6-overlay) enabled for PID 1 Init capabilities, [zabbix-agent](https://zabbix.org) based on TRUNK compiled for individual container monitoring, Cron also installed along with other tools (bash,curl, less, logrotate, nano, vim) for easier management. It also supports sending to external SMTP servers..


[Changelog](CHANGELOG.md)

# Authors

- [Dave Conroy](http://github/tiredofit/)

# Table of Contents

- [Introduction](#introduction)
    - [Changelog](CHANGELOG.md)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
    - [Environment Variables](#environmentvariables)   
- [Maintenance](#maintenance)
    - [Shell Access](#shell-access)
   - [References](#references)

# Prerequisites

This image assumes that you are using a reverse proxy such as [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy) and optionally the [Let's Encrypt Proxy Companion @ https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion](https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion) in order to serve your pages. However, it will run just fine on it's own if you map appropriate environment variables



# Installation

Automated builds of the image are available on [Docker Hub](https://hub.docker.com/tiredofit/nginx-proxy-cloudflare-companion) and is the recommended method of installation.


```bash
docker pull hub.docker.com/tiredofit/nginx-proxy-cloudflare-companion:(imagetag)
```

* `latest` - Most recent release w/Python 2 and Alpine 3.6

# Quick Start

* The quickest way to get started is using [docker-compose](https://docs.docker.com/compose/). See the examples folder for a working [docker-compose.yml](examples/docker-compose.yml) that can be modified for development or production use.

* Set various [environment variables](#environment-variables) to understand the capabilities of this image.

# Configuration

### Environment Variables

Along with the Environment Variables from the [Base image](https://hub.docker.com/r/tiredofit/alpine), below is the complete list of available options that can be used to customize your installation. By Default Cron and SMTP are disabled.

| Parameter | Description |
|-----------|-------------|
| `CF_EMAIL` | Your Cloudflare Email Address |
| `CF_TOKEN` | Token for the Domain |
| `CF_ZONE_ID`   | Cloudflare Zone ID |
| `CF_TARGET_DOMAIN | Destination Host to forward records to e.g. `host.example.com` |

# Maintenance
#### Shell Access

For debugging and maintenance purposes you may want access the containers shell. 

```bash
docker exec -it (whatever your container name is e.g. nginx-proxy-cloudflare-companion) bash
```

# References

* https://www.cloudflare.com
* https://github.com/code5-lab/dns-flare