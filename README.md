# CA Key Manager

OpenSSL Certificate Authority configuration for managing TLS certificates across multiple internal services.

## Overview

Manages a custom CA and per-service certificates for a self-hosted homelab. Covers GitLab, Jupyter, Docker registry, and documentation servers under internal domains.

## Services Covered

- `gitlab-ce.server.net`
- `jupyter.server.net`
- `registry.server.net`
- `documentation.server.net`
- `cotia.tg`

## Structure

- `ca/` - Root CA configuration and certificate
- Per-domain folders with `.cnf`, `.csr`, `.crt` files

## Usage

Generate a certificate for a new service:
```bash
openssl req -new -newkey rsa:2048 -nodes -keyout service.key -out service.csr -config service.cnf
openssl x509 -req -in service.csr -CA ca/ca.crt -CAkey ca/ca.key -CAcreateserial -out service.crt -days 365
```

## Security

Private key files (`*.key`) are not tracked. Generate them locally using the provided `.cnf` files.
