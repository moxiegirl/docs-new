---
layout: naming
title: Overview of name resolution
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

BNS names are bound to both public keys and to about 40Kb of off-chain state.
The off-chain state is encoded as a [DNS zone file](https://en.wikipedia.org/wiki/Zone_file),
which contains routing information for discovering the user's Blockstack data
(such as their profile and app data, which are hosted in the [Gaia storage
system](https://github.com/blockstack/gaia)).

The blockchain is not used to store this information directly.  Instead, the
blockchain stores the *public key hash* and the *zone file hash*.  When
indexing the blockchain, each BNS node builds a database with
three columns:  all the on-chain BNS names that have been registered, each
name's public key hash, and each name's zone file's hash.
In addition, each BNS node maintains the *transaction history* of each name.
A developer can resolve a name to any configuration it was in at any prior
point in time.

Below is an example name table pulled from a live BNS node:

| Name | Public key hash | Zone File Hash |
|------|-----------------|--------------|
| `ryan.id` | `15BcxePn59Y6mYD2fRLCLCaaHScefqW2No` | `a455954b3e38685e487efa41480beeb315f4ec65` |
| `muneeb.id` | `1J3PUxY5uDShUnHRrMyU6yKtoHEUPhKULs` | `37aecf837c6ae9bdc9dbd98a268f263dacd00361` |
| `jude.id` | `16EMaNw3pkn3v6f2BgnSSs53zAKH4Q8YJg` | `b6e99200125e70d634b17fe61ce55b09881bfafd` |
| `verified.podcast` | `1MwPD6dH4fE3gQ9mCov81L1DEQWT7E85qH` | `6701ce856620d4f2f57cd23b166089759ef6eabd` |
| `cicero.res_publica.id` | `1EtE77Aa5AA8etzF2irk56vvkS4v7rZ7PE` | `7e4ac75f9d79ba9d5d284fac19617497433b832d` |
| `podsaveamerica.verified.podcast` | `1MwPD6dH4fE3gQ9mCov81L1DEQWT7E85qH` | `0d6f090db8945aa0e60759f9c866b17645893a95` |

In practice, the zone file hash is the `RIPEMD160` hash of the `SHA256` hash of
the zone file, and the public key is the `base58check`-encoded `RIPEMD160` hash
of the double-`SHA256` hash of the ECDSA public key (i.e. a Bitcoin address).

The BNS consensus rules ensure that
a BNS name can only be registered if it is not already taken, and that only the
user who owns the name's private key can change its public key hash or zone file
hash.  This means that a name's public key and zone file can be stored anywhere,
since they can be authenticated using the hashes discovered by indexing the
blockchain under the BNS consensus rules.

BNS nodes implement a decentralized storage system for zone files called the
[Atlas network](atlas_network.md).  In this system, BNS nodes eagerly replicate
all the zone files they know about to one another, so that eventually every BNS
node has a full replica of all zone files.

The public keys for names are stored off-chain in [Gaia](https://github.com/blockstack/gaia).
The user controls where their public keys are hosted using the zone file
contents (if they are hosted online anywhere at all).

Developers can query this table via the BNS API.
