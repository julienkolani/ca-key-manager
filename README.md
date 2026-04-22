# CA Key Manager

Gestion d'une Autorité de Certification (CA) OpenSSL pour les certificats TLS d'un lab multi-services.

## Services couverts

- `gitlab-ce.server.net`
- `jupyter.server.net`
- `registry.server.net`
- `rocketchat.server.net`
- `documentation.server.net`
- `cotia.tg`

## Structure

- `ca/` — Certificat racine de la CA
- `domains/<service>/` — Fichiers `.cnf`, `.csr`, `.crt` par service

## Générer un certificat

```bash
# Créer la clé privée et la CSR
openssl req -new -newkey rsa:2048 -nodes -keyout service.key -out service.csr -config service.cnf
# Signer avec la CA
openssl x509 -req -in service.csr -CA ca/ca.crt -CAkey ca/ca.key -CAcreateserial -out service.crt -days 365
```

## Sécurité

Les clés privées (`*.key`) sont exclues du dépôt. Voir `SECURITY.md`.
