---
layout: naming
title: List all namespaces
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---
#### List all namespaces in existence ([reference](https://core.blockstack.org/#namespace-operations-get-all-namespaces)).

```bash
$ curl https://core.blockstack.org/v1/namespaces
[                                                                                                                                                                                                                                                                                                                             
  "id",
  "helloworld",
  "podcast"
]
```

#### List all names within a namespace ([reference](https://core.blockstack.org/#namespace-operations-get-all-namespaces))

```bash
$ curl https://core.blockstack.org/v1/namespaces/id/names?page=0
[
  "0.id",
  "0000.id",
  "000000.id",
  "000001.id",
  "00000111111.id",
  "000002.id",
  "000007.id",
  "0011sro.id",
  "007_007.id",
  "00n3w5.id",
  "00r4zr.id",
  "00w1k1.id",
  "0101010.id",
  "01jack.id",
  "06nenglish.id",
  "08.id",
  "0cool_f.id",
  "0dadj1an.id",
  "0nelove.id",
  "0nename.id"
...
]
```

Each page returns a batch of 100 names.
