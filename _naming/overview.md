---
layout: naming
title: What is the Blockstack Naming Service?
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

The Blockstack Naming Service (BNS) is a network system that binds names
to off-chain state without relying on any central points of control.
It does so by embedding a log of its control-plane messages within a public blockchain, like Bitcoin.

Each BNS peer determines the state of each name by indexing these specially-crafted
transactions.  In doing so, each peer independently calculates the same global
name state.

Names in BNS have three properties:

* **Names are globally unique.**  The protocol does not allow name collisions, and all
  well-behaved nodes resolve a given name to the same state.
* **Names are human-meaningful.**  Each name is chosen by its creator.
* **Names are strongly-owned.**  Only the name's owner can change the state it
  resolves to.  Specifically, a name is owned by one or more ECDSA private keys.

Internally, a BNS node implements a replicated name database.  Each BNS node keeps itself
synchronized to all of the other ones in the world, so queries on one BNS node
will be the same on other nodes.  BNS nodes allow a name's owner to bind
up to 40Kb of off-chain state to their name, which will be replicated to all
BNS nodes via the [Atlas network](atlas_network.md).

BNS nodes extract the name database log from an underlying blockchain (Blockstack
Core currently uses Bitcoin, and had used Namecoin in the past).
BNS uses the blockchain to establish a shared "ground truth" for the system:  as long as
two nodes have the same view of the blockchain, then they will build up the same
database.

The biggest consequence for developers is that in BNS, reading name state is
fast and cheap but writing name state is slow and expensive.  This is because
registering and modifying names requires one or more transactions to be sent to
the underlying blockchain, and BNS nodes will not process them until they are
sufficiently confirmed.  Users and developers need to acquire and spend the requisite cryptocurrency (i.e. Bitcoin) to send BNS transactions.
