# Vault Proxy

Tested on: Debian 11

This role sets up NGINX (SOSETH/nginx) as a proxy to be able to keep a vault cluster private.

## Note
This role assumes that TLS certificates for `vault_proxy_domain` will be provisioned at:
* `/etc/vault.d/server.pem`
* `/etc/vault.d/server.key`
* `/etc/vault.d/ca.pem`

## Configuration
|Var|Default value|Description|
|---|-------------|-----------|
|vault_proxy_domain|`vault.example.org`|Domain to use for proxying to vault|
|vault_proxy_port|`443`|Port to bind nginx to|
|vault_pki_proxy_domain|`pki.example.org`|Domain to use for proxying vault PKI's public endpoints|
|vault_server_ips|`[]`|List of vault servers|

## Details
This role will make vault available on `vault_proxy_domain`, enforcing client certificates along the way.
Additionally, it'll expose vault PKI's public endpoints (CAs for X.509 AIA as well as CRLs) on `vault_pki_proxy_domain`.