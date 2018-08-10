---
layout: naming
title: Get the fee
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

```bash
$ curl -sL https://core.blockstack.org/v1/prices/names/helloworld.id | jq -r ".name_price"
{
  "btc": 2.5e-05,
  "satoshis": 2500
}
```

Note the use of `jq -r` to select the `"name_price"` field.  This API
endpoint may return other ancilliary data regarding transaction fee estimation,
but this is the only field guaranteed by this specification to be present.

#### Getting the Current Consensus Hash ([reference](https://core.blockstack.org/#blockchain-operations-get-consensus-hash))

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
