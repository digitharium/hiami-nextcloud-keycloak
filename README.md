# Template Repository
[![License: BSD3](https://img.shields.io/badge/License-BSD3-blue.svg)](https://opensource.org/license/bsd-3-clause/)

[![Trigger Jenkins Pipe](https://github.com/digitharium/hiami-nextcloud-keycloak/actions/workflows/main.yml/badge.svg)](https://github.com/digitharium/hiami-nextcloud-keycloak/actions/workflows/main.yml)

## Introduction
This repository is a template for all the repositories that will be used at the hackathon 2024 part of the symposium.

## Contributors
* [Abdul Kader Kabore](https://github.com/nih4me)
* [Badr Kandouz](https://github.com/bkandouz)

## Instructions
This section will highlight the instructions needed for this repository

## Integrate Keycloak in Nextcloud

### Manual Integration

#### Run Keycloak and Nextcloud using Docker

- Keycloak

```sh
docker run -d --name keycloak -p 8080:8080
-e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin
quay.io/keycloak/keycloak:23.0.4 start-dev
```

- Nextcloud

```sh
docker run -d -p 8086:80 -v nextcloud:/var/www.html nextcloud
```

>FInalize the installation of Keycloak `(http://<ip-address>:8080)` and Nextcloud `(http://<ip-address>:8086)`


#### Edits on the code

- Add `'allow_local_remote_servers' => true` to the variable `$CONFIG` in `nextcloud/config/config.php`
- Add Keycloak's domain or the IP address (and port number) to `'trusted_domains'` array in `nextcloud/config/config.php`

#### Addional Apps

- Install `Social Logins`

#### Configurations 

1. Open the social logins app on Netxcloud
2. Complete the form Custom Oauth2 
   - Use the information found in Keycloak `Realm Settings -> Endpoints (OpenId Endpoint Configurations)`
   - For scope use : `openid email profile`

### Automated procedure

#### Run the following command

```sh
git clone https://github.com/digitharium/hiami-nextcloud-keycloak.git
cd hiami-nextcloud-keycloak/nextcloud-keycloak-integration
docker compose build --progress=plain nextcloud
docker compose build --progress=plain keycloak
docker compose up --force-recreate -V
```