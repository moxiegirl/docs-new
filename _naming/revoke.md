---
layout: naming
title: NAME_REVOKE
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

A `NAME_REVOKE` transaction makes a name unresolvable.  The BNS consensus rules
stipulate that once a name is revoked, no one can change its public key hash or
its zone file hash.  The name's zone file hash is set to `null` to prevent it
from resolving.

You should only do this if your private key is compromised, or if you want to
render your name unusable for whatever reason.  It is rarely used in practice.

The `NAME_REVOKE` operation is generated using only the name.  See the
[transaction format](wire-format.md) document for details on how to construct
it.
