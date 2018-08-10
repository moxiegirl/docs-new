---
layout: naming
title: NAME_TRANSFER
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

A `NAME_TRANSFER` transaction changes the name's public key hash.  You would
send one of these transactions if you wanted to:

* Change your private key
* Send the name to someone else

When transferring a name, you have the option to also clear the name's zone
file hash (i.e. set it to `null`).
This is useful for when you send the name to someone else, so the
recipient's name does not resolve to your zone file.

The `NAME_TRANSFER` transaction is generated from the name, a recent [consensus
hash](#bns-forks), and the new public key hash.  The reference clients gather
this information automatically.  See the [transaction format](wire-format.md)
document for details on how to construct this transaction.
