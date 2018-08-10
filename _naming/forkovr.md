---
layout: naming
title: BNS forks
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---
BNS effectively uses a public blockchain to store a database log.  A BNS peer
bootstraps itself by downloading and replaying the database log from the
blockchain, and in doing so, will calculate the same name database state as
every other (honest) BNS peer that has the same view of the blockchain.

Crucially, BNS is built on top of a public blockchain that is *unaware* of BNS's existence.
This means that the blockchain peers do not validate BNS transactions.  Instead,
the BNS peer needs to do so, and must know how to *reject* both invalid transactions
as well as well-formed transactions from dishonest peers (i.e. peers that do not
follow the same consensus rules).

BNS nodes do not directly communicate with one another---by design, the set of
BNS peers is not enumerable.  The only shared communication medium between BNS
peers is the blockchain.

To identify and reject invalid and malicious transactions without the blockchain's help,
the log of name operations embedded in the blockchain is constructed as a
[fork\*-consistent](http://www.scs.stanford.edu/~jinyuan/bft2f.pdf) database
log.  Fork\*-consistency is a [consistency
model](https://en.wikipedia.org/wiki/Consistency_model) whereby the state
replicas in all of the nodes exhibit the following properties:

* Each correct peer maintains a history of well-formed, valid state operations.  In this
  case, each correct BNS node maintains a copy of the history blockchain transactions
that encoded well-formed, valid name operations.

* Each honest peer's history contains the sequence of all operations that it
  sent.  That is, a user's BNS peer's transaction log will contain the sequence of all valid
transactions that the user's client wrote to the blockchain.

* If two peers accept operations *op* and *op'* from the same correct client,
  then both of their logs will have the both operations in the same order.  If
*op'* was accepted before *op*, then both peers' logs are identical up to *op'*.
In BNS, this means that if two peers both accept a given transaction, then it
means that they have accepted the same sequence of prior transactions.

This means that unlike with blockchains,
there can be *multiple long-lived conflicting forks* of the BNS database log.
However, due to fork\*-consistency, a correct BNS peer will only process *one*
of these forks, and will *ignore* transactions from peers in other forks.  In other words,
fork\*-consistency partitions the set of BNS peers into different **fork-sets**,
where all peers in a fork-set process each other's transactions, but the
completely ignore peers in other fork-sets.

BNS nodes identify which fork set they belong to using a **consensus hash**.  The
consensus hash is a cryptographic digest of a node's operation
history.  Each BNS peer calculates a new consensus hash each time it processes a
new block, and stores the history of consensus hashes for each block it
processed.

Two honest BNS peers can quickly determine if they are in the same fork-set by querying
each other's consensus hashes for a given block.  If they match, then they are
in the same fork-set (assming no hash collisions).

A BNS client executes a name operation on a specific fork-set by including a
recent consensus hash from that fork-set in the blockchain transaction.
At the same time, the BNS consensus rules state that a transaction can only be
accepted if it included a recent valid consensus hash.
This means that all BNS nodes in the client's desired fork-set will accept
the transaction, and all other BNS nodes not in the fork-set will ignore it.
You can see where the consensus hash is included in blockchain transactions by reading
the [transaction wire format](wire-format.md) document.
