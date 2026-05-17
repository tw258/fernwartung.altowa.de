# fernwartung.altowa.de

This repository contains the static website and deployment files for a customer-facing remote support download portal.

## Contents

- `docker/docker-compose-prod.yaml` – Production compose file for Nginx, serving the `html/` folder as a static site.
- `html/index.html` – Main download page that detects the user OS and shows download buttons.
- `html/css/style.css` – Light, high-contrast styling optimized for older users.
- `html/assets/altowa.exe` – Prebuilt Windows minimal client that connects to the private relay server without installation.
- `RelayServer.md` – Notes for self-hosting the RustDesk relay server components (`hbbs`/`hbbr`).

## Purpose

The site is intended as a simple download hub for customers:

- Windows users are recommended to download the **Altowa Minimal Client**.
- The official RustDesk release is offered as the **full version** alternative.
- `RelayServer.md` documents how to deploy a private RustDesk relay server.

## Deployment

The portal is typically deployed with Nginx using `docker/docker-compose-prod.yaml`.

## Creating new custom clients

New versions for custom clients can be created here: https://rdgen.crayoneater.org/
