---
layout: naming
title: Get the consensus hash
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---


```bash
$ curl -sL https://core.blockstack.org/v1/blockchains/bitcoin/consensus
{
  "consensus_hash": "98adf31989bd937576aa190cc9f5fa3a"
}
```

A recent consensus hash is required to create a `NAMESPACE_PREORDER` transaction.  The reference
BNS clients do this automatically.  See the [transaction format](wire-format.md)
document for details on how the consensus hash is used to construct the
transaction.
