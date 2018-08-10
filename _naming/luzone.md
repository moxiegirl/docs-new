---
layout: naming
title: Lookup a name's public key & zone file
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

```bash
$ curl https://core.blockstack.org/v1/names/muneeb.id
{
  "address": "1J3PUxY5uDShUnHRrMyU6yKtoHEUPhKULs",
  "blockchain": "bitcoin",
  "expire_block": 599266,
  "last_txid": "7e16e8688ca0413a398bbaf16ad4b10d3c9439555fc140f58e5ab4e50793c476",
  "status": "registered",
  "zonefile": "$ORIGIN muneeb.id\n$TTL 3600\n_http._tcp URI 10 1 \"https://gaia.blockstack.org/hub/1J3PUxY5uDShUnHRrMyU6yKtoHEUPhKULs/0/profile.json\"\n",
  "zonefile_hash": "37aecf837c6ae9bdc9dbd98a268f263dacd00361"
}
```

Note that the `zonefile` field is given with the off-chain data that hashes
to the `zonefile_hash` field.
