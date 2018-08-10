---
layout: naming
title: Organization and features
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

BNS names are organized into a global name hierarchy.  There are three different
layers in this hierarchy related to naming:

* **Namespaces**.  These are the top-level names in the hierarchy.  An analogy
  to BNS namespaces are DNS top-level domains.  Existing BNS namespaces include
`.id`, `.podcast`, and `.helloworld`.  All other names belong to exactly one
namespace.  Anyone can create a namespace, but in order for the namespace
to be persisted, it must be *launched* so that anyone can register names in it.
Namespaces are not owned by their creators.

* **BNS names**.  These are names whose records are stored directly on the
  blockchain.  The ownership and state of these names are controlled by sending
blockchain transactions.  Example names include `verified.podcast` and
`muneeb.id`.  Anyone can create a BNS name, as long as the namespace that
contains it exists already.  The state for BNS names is usually stored in the [Atlas
network](atlas_network.md).

* **BNS subdomains**.  These are names whose records are stored off-chain,
but are collectively anchored to the blockchain.  The ownership and state for
these names lives within the [Atlas network](atlas_network.md).  While BNS
subdomains are owned by separate private keys, a BNS name owner must
broadcast their subdomain state.  Example subdomains include `jude.personal.id`
and `podsaveamerica.verified.podcast`.  Unlike BNS namespaces and names, the
state of BNS subdomains is *not* part of the blockchain consensus rules.

A feature comparison matrix summarizing the similarities and differences
between these name objects is presented below:

| Feature | **Namespaces** | **BNS names** | **BNS Subdomains** |
|---------|----------------|---------------|--------------------|
| Globally unique | X | X | X |
| Human-meaningful | X | X | X |
| Owned by a private key |  | X | X |
| Anyone can create | X | X | [1] |
| Owner can update |   | X  | [1] |
| State hosted on-chain | X | X |  |
| State hosted off-chain |  | X | X |
| Behavior controlled by consensus rules | X | X |  |
| May have an expiration date |  | X  |  |

[1] Requires the cooperation of a BNS name owner to broadcast its transactions
