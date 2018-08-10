---
layout: auth
title: Lookup chunks
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

All Atlas chunks are addressed by the RIPEMD160 hash of the SHA256 hash of the
chunk data.  A client can query up to 100 chunks in one RPC call.

A client can look up a chunk with the `get_zonefiles()` method.  If successful,
the returned payload will be a `dict` with a `zonefiles` key that maps the chunk
hashes to their respective data.

```python
>>> import blockstack
>>> data = blockstack.lib.client.get_zonefiles('https://node.blockstack.org:6263', ['1b89a685f4c4ea245ce9433d0b29166c22175ab4'])
>>> print data['zonefiles']['1b89a685f4c4ea245ce9433d0b29166c22175ab4']
$ORIGIN duckduckgo_tor.id
$TTL 3600
tor TXT "3g2upl4pq6kufc4m.onion"

>>>
```

(This particular chunk happens to be associated with the BNS name
`duckduckgo_tor.id`).
