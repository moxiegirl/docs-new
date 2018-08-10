---
layout: auth
title: Query Chunk Inventories
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

Developers can query a node's inventory vector as follows:

```python
>>> import blockstack
>>> result = blockstack.lib.client.get_zonefile_inventory("https://node.blockstack.org:6263", 0, 524288)
>>> print len(result['inv'])
11278
>>>
```

The variable `result['inv']` here is a big-endian bit vector, where the *i*th
bit is set to 1 if the *i*th chunk in the chunk sequence is present.  The bit at
`i=0` (the earliest chunk) refers to the leftmost bit.

A sample program that inspects a set of Atlas nodes' inventory vectors and determines
which ones are missing which chunks can be found
[here](https://github.com/blockstack/atlas/blob/master/atlas/atlas-test).
