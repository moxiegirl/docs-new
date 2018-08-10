---
layout: auth
title: Propagate chunks
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

Atlas peers will each store a copy of the chunks you announce.  In the
background, they will asynchronously announce to one another which chunks they
have available, and replicate them to one another in a rarest-first order (much
like how BitTorrent works).  Eventually, every Atlas peer will receive the
chunk.

However, developers can accelerate this process by eagerly propagating chunks.
To do so, they can ask an Atlas peer for its immediate neighbors in the Atlas
peer graph, and replicate the chunk to each of them as well.

For example, this code will replicate the chunk to not only
`https://node.blockstack.org:6263`, but also to its immediate neighbors.

```python
>>> import blockstack
>>> import base64
>>> data = "..."   # this is the chunk you will replicate widely
>>> data_b64 = base64.b64encode(data)
>>>
>>> result = blockstack.lib.client.get_atlas_peers('https://node.blockstack.org:6263')
>>> neighbors = result['peers']
>>> print ", ".join(neighbors)
13.65.207.163:6264, 52.225.128.191:6264, node.blockstack.org:6264, 23.102.162.7:6264, 52.167.230.235:6264, 23.102.162.124:6264, 52.151.59.26:6264, 13.92.134.106:6264
>>>
>>> for neighbor in neighbors:
...    result = blockstack.lib.client.put_zonefiles(neighbor, [data_b64])
...    assert result['saved'][0] == 1
...
>>>
```

This is not strictly necessary, but it does help accelerate chunk replication
and makes it less likely that a chunk will get lost due to individual node
failures.
