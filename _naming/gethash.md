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

The consensus hash must be included in the `NAME_PREORDER` transaction.  The BNS
clients do this automatically.  See the [transaction format
document](wire-format.md) for details as to how to include this in the
transaction.
