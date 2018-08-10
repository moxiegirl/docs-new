---
layout: naming
title: Fork-set selection
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---
The blockchain linearizes the history of transactions, which means that
in general, there exists a fork-set for each distinct set of BNS
consensus rules.  For example, the Blockstack Core [2016 hard fork](release_notes/changelog-0.14.md)
and [2017 hard fork](release_notes/changelog-0.17.md) both introduced new consensus
rules, which means at the time of this writing there are three possible fork-sets:
the pre-2016 fork-set, the 2016-2017 fork-set, and the post-2017 fork-set.
The [public BNS nodes](https://node.blockstack.org:6263) are always running
in the fork-set with the latest consensus rules.

BNS clients are incentivized to communicate with peers in the fork-set that has
the most use, since this fork-set's name database will encode name/state
bindings that are the most widely-accepted and understood by users.
To identify this fork-set, a BNS client needs to learn one of
its recent consensus hashes.  Once it has a recent consensus hash, it can
query an *untrusted* BNS node for a copy of
its name database, and use the consensus hash to verify that the name database
was used to generate it.

How does a BNS node determine whether or not a consensus hash corresponds to the
most widely-used fork-set?  There are two strategies:

* Determine whether or not a *characteristic transaction* was accepted by the
widely-used fork-set.  If a client knows that a specific transaction belongs to
the widely-used fork-set and not others, then they can use the consensus hash to
efficiently determine whether or not a given node belongs to this fork-set.

* Determine how much "economic activity" exists in a fork-set by inspecting
the blockchain for burned cryptocurrency tokens.  Namespace and name
registrations are structured in a way that sends cryptocurrency tokens to either
a well-known burn address, or to an easily-queried pay-to-namespace-creator
address.

Both strategies rely on the fact that the consensus hash is calculated as a
[Merkle skip-list](https://github.com/blockstack/blockstack-core/issues/146)
over the BNS node's accepted transactions.  A client can use a consensus hash to
determine whether or not a transaction *T* was accepted by a node with *O(log
n)* time and space complexity.  We call the protocol for resolving a consensus hash to a specific transaction
**Simplified Name Verification** (SNV).  See our [paper on the subject](https://blockstack.org/virtualchain_dccl16.pdf)
for details of how SNV works under the hood.

If the client has a consensus hash and knows of a characteristic transaction in the widely-used fork-set,
it can use SNV to determine whether or not a node belongs to the fork-set that accepted it.

If the client knows about multiple conflicting consensus hashes,
they can still use SNV to determine which one corresponds
to the most-used fork-set.  To do so, the client would use a
[blockchain explorer](https://explorer.blockstack.org) to find the
list of transactions that burned cryptocurrency tokens.  Each of these
transactions will be treated as potential characteristic transactions:
the client would first select the subset of transactions that are well-formed
BNS transactions, and then use SNV to determine which of them correspond to which
consensus hashes.  The client chooses the consensus hash that corresponds
to the fork-set with the highest cumulative burn.

Work is currently underway to automate this process.
