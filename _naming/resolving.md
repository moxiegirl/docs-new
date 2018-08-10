---
layout: naming
title: Resolve subdomains
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---
Developers interact with subdomains the same way they interact with names.
Using the BNS API, a developer can:

#### Look up a subdomain's public key and zone file ([reference](https://core.blockstack.org/#name-querying-get-name-info))

```bash
$ curl https://core.blockstack.org/v1/names/aaron.personal.id
{
  "address": "1PwztPFd1s2STMv4Ntq6UPBdYgHSBr5pdF",
  "blockchain": "bitcoin",
  "last_txid": "85e8273b0a38d3e9f0af7b4b72faf0907de9f4616afc101caac13e7bbc832394",
  "status": "registered_subdomain",
  "zonefile_hash": "a6dda6b74ffecf85f4a162627d8df59577243813",
  "zonefile_txt": "$ORIGIN aaron.personal.id\n$TTL 3600\n_https._tcp URI 10 1 \"https://gaia.blockstack.org/hub/1PwztPFd1s2STMv4Ntq6UPBdYgHSBr5pdF/profile.json\"\n"
}
```

#### Look up a subdomain's transaction history ([reference](https://core.blockstack.org/#name-querying-name-history))

```bash
$ curl https://core.blockstack.org/v1/names/aaron.personal.id/history
{
  "509981": [
    {
      "address": "1PwztPFd1s2STMv4Ntq6UPBdYgHSBr5pdF",
      "block_number": 509981,
      "domain": "personal.id",
      "name": "aaron.personal.id",
      "sequence": 0,
      "txid": "85e8273b0a38d3e9f0af7b4b72faf0907de9f4616afc101caac13e7bbc832394",
      "value_hash": "a6dda6b74ffecf85f4a162627d8df59577243813",
      "zonefile": "JE9SSUdJTiBhYXJvbi5wZXJzb25hbC5pZAokVFRMIDM2MDAKX2h0dHBzLl90Y3AgVVJJIDEwIDEgImh0dHBzOi8vZ2FpYS5ibG9ja3N0YWNrLm9yZy9odWIvMVB3enRQRmQxczJTVE12NE50cTZVUEJkWWdIU0JyNXBkRi9wcm9maWxlLmpzb24iCg=="
    }
  ]
}
```

#### Look up the list of names and subdomains owned by a given public key hash ([reference](https://core.blockstack.org/#name-querying-get-names-owned-by-address))

```bash
$ curl https://core.blockstack.org/v1/addresses/bitcoin/1PwztPFd1s2STMv4Ntq6UPBdYgHSBr5pdF
{
  "names": [
    "aaron.personal.id"
  ]
}
```
