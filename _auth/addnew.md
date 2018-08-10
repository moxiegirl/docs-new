---
layout: auth
title: Add a new chunk
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---
The only way to add a chunk to Atlas is to do so through an on-chain name in
BNS.  Adding a new chunk is a two-step process:

* The name owner announces the chunk hash as a name's state
via a `NAME_REGISTRATION`, `NAME_UPDATE`, `NAME_RENEWAL`, or `NAME_IMPORT` transaction.
* Once the transaction is confirmed and processed by BNS, the name owner
  broadcasts the matching zone file.

Setting a name's state to be the hash of a chunk is beyond the scope of this
document, since it needs to be done through a BNS client.
See the relevant documentation for
[blockstack.js](https://github.com/blockstack/blockstack.js) and the [Blockstack
Browser](https://github.com/blockstack/blockstack-browser) for doing this.

Once the name operation is confirmed, you can announce the data to the
Atlas network.  You can do so with the Python client as follows:

```python
>>> import blockstack
>>> import base64
>>> data = "..."   # this is the chunk data you will announce
>>> data_b64 = base64.b64encode(data)
>>> result = blockstack.lib.client.put_zonefiles('https://node.blockstack.org:6263', [data_b64])
>>> assert result['saved'][0] == 1
>>>
```

At most five chunks can be announced in one RPC call.
Note that the data must be base64-encoded before it can be announced.

When the `put_zonefiles()` method succeeds, it returns a `dict` with a list
under the `saved` key.  Here, `result['saved'][i]` will be 1 if the `i`th
chunk given to `put_zonefiles()` was saved by the node, and 0 if not.
The node will not save a chunk if it is too big, or if it has not yet processed
the name operation that contained the chunk's hash.

The `put_zonefiles()` method is idempotent.
