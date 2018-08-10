---
layout: naming
title: Manage BNS names
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

Once you register a BNS name, you have the power to change its zone file hash,
change its public key hash, destroy it (i.e. render it unresolvable),
or renew it.  The BNS consensus rules ensure that *only* you, as the owner of
the name's private key, have the ability to carry out these operations.

Each of these operations are executed by sending a specially-formatted
blockchain transaction to the blockchain, which BNS nodes read and process.
The operations are listed below:

| Transaction Type | Description |
|------------------|-------------|
| `NAME_UPDATE`    | This changes the name's zone file hash.  Any 20-byte string is allowed. |
| `NAME_TRANSFER`  | This changes the name's public key hash.  In addition, the current owner has the option to atomically clear the name's zone file hash (so the new owner won't "receive" the zone file). |
| `NAME_REVOKE`    | This renders a name unresolvable.  You should do this if your private key is compromised. |
| `NAME_RENEWAL`   | This pushes back the name's expiration date (if it has one), and optionally both sets a new zone file hash and a new public key hash. |

The reference BNS clients---
[blockstack.js](https://github.com/blockstack/blockstack.js) and the [Blockstack
Browser](https://github.com/blockstack/blockstack-browser)---can handle creating
and sending all of these transactions for you.

### NAME_UPDATE ([live example](https://www.blocktrail.com/BTC/tx/e2029990fa75e9fc642f149dad196ac6b64b9c4a6db254f23a580b7508fc34d7))

A `NAME_UPDATE` transaction changes the name's zone file hash.  You would send
one of these transactions if you wanted to change the name's zone file contents.
For example, you would do this if you want to deploy your own [Gaia
hub](https://github.com/blockstack/gaia) and want other people to read from it.

A `NAME_UPDATE` transaction is generated from the name, a recent [consensus
hash](#bns-forks), and the new zone file hash.  The reference clients gather
this information automatically.  See the [transaction format](wire-format.md)
document for details on how to construct this transaction.
