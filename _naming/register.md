---
layout: naming
title: Overview of registration
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

Registering a BNS name costs cryptocurrency.  This cost comes from two sources:

* **Transaction fees:** These are the fees imposed by the cost of storing the
  transaction data to the blockchain itself.  They are independent of BNS, since
all of the blockchain's users are competing to have their transactions included
in the next block.  The blockchain's miners receive the transaction fee.

* **Registration fees:** Each BNS namespace imposes an *additional* fee on how
  much a name costs.  The registration fee is sent to the namespace creator
during the first year that a namespace exists, and is sent to a burn address
afterwards.  The registration fee is different for each name and is
determined by the namespace itself, but can be queried in advance by the user.

Registering a name takes two transactions.  They are:

* **`NAME_PREORDER` transaction**:  This is the first transaction to be sent.
  It tells all BNS nodes the *salted hash* of the BNS name, and it pays the
registration fee to the namespace owner's designated address (or the burn
address).  In addition, it proves to the BNS nodes that the client knows about
the current state of the system by including a recent *consensus hash*
in the transaction (see the section on [BNS forks](#bns-forks) for details).

* **`NAME_REGISTRATION` transaction**:  This is the second transaction to be
  sent.  It reveals the salt and the name to all BNS nodes, and assigns the name
an initial public key hash and zone file hash

The reason this process takes two transactions is to prevent front-running.
The BNS consensus rules stipulate that a name can only be registered if its
matching preorder transaction was sent in the last 24 hours.  Because a name
must be preordered before it is registered, someone watching the blockchain's
peer network cannot race a victim to claim the name they were trying to
register (i.e. the attacker would have needed to send a `NAME_PREORDER`
transaction first, and would have had to have sent it no more than 24 hours
ago).

Registering a name on top of the Bitcoin blockchain takes 1-2 hours.  This is
because you need to wait for the `NAME_PREORDER` transaction to be sufficiently
confirmed before sending the `NAME_REGISTRATION` transaction.  The BNS nodes
only register the name once both transactions have at least 6 confirmations
(which itself usually takes about an hour).

Names are registered on a first-come first-serve basis.
If two different people try to register the same name at the same time, the
person who completes the two-step process *earliest* will receive the name.  The
other person's `NAME_REGISTRATION` transaction will be ignored, since it will
not be considered valid at this point.  The registration fee paid by the
`NAME_PREORDER` will be lost.  However, this situation is rare in practice---
as of early 2018, we only know of one confirmed instance in the system's 3+ years
of operation.

Fully-qualified names can be between 3 and 37 characters long, and consist of
the characters `a-z`, `0-9`, `+`, `-`, `_`, and `.`.  This is to prevent
[homograph attacks](https://en.wikipedia.org/wiki/IDN_homograph_attack).
`NAME_REGISTRATION` transactions that do not conform to this requirement will be
ignored.
