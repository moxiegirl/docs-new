---
layout: naming
title: List all names the node recognizes
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

```bash
$ curl https://core.blockstack.org/v1/names?page=0
[
  "judecn.id",
  "3.id",
  "4.id",
  "8.id",
  "e.id",
  "h.id",
  "5.id",
  "9.id",
  "i.id",
  "l.id",
  "p.id",
  "w.id",
  "ba.id",
  "df.id",
...
]
```

Each page returns 100 names.  While no specific ordering is mandated by the
protocol, the reference implementation orders names by their order of creation
in the blockchain.
