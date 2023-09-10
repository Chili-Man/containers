# Containers
[![GitHub Super-Linter](https://github.com/chili-man/containers/actions/workflows/main.yaml/badge.svg)](https://github.com/marketplace/actions/super-linter)

Containers used for home automation purposes.

## Usage
Each subdirectory corresponds to a Dockerfile built for a specific purpose.
**All containers are available through DockerHub, under [habanero](https://hub.docker.com/u/habanero)**

- [certificate-manager](./certificate-manager):
    Uses [ofelia](https://github.com/mcuadros/ofelia) and [lego](https://github.com/go-acme/lego)
    to manage TLS certificates through ACME from [Let's Encrypt](https://letsencrypt.org/)
