---
layout: naming
title: Decentralized Identifiers (DIDs)
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---
BNS nodes are compliant with the emerging
[Decentralized Identity Foundation](http://identity.foundation) protocol
specification for decentralized identifiers (DIDs).

Each name in BNS has an associated DID.  The DID format for BNS is:

```
    did:stack:v0:{address}-{index}
```

Where:
* `{address}` is an on-chain public key hash (e.g. a Bitcoin address).
* `{index}` refers to the `nth` name this address created.

For example, the DID for `personal.id` is
`did:stack:v0:1dARRtzHPAFRNE7Yup2Md9w18XEQAtLiV-0`, because the name
`personal.id` was the first-ever name created by
`1dARRtzHPAFRNE7Yup2Md9w18XEQAtLiV`.

As another example, the DID for `jude.id` is `did:stack:v0:16EMaNw3pkn3v6f2BgnSSs53zAKH4Q8YJg-1`.
Here, the address `16EMaNw3pkn3v6f2BgnSSs53zAKH4Q8YJg` had created one earlier
name in history prior to this one (which happens to be `abcdefgh123456.id`).

The purpose of a DID is to provide an eternal identifier for a public key.
The public key may change, but the DID will not.

Blockstack Core implements a DID method of its own
in order to be compatible with other systems that use DIDs for public key resolution.
In order for a DID to be resolvable, all of the following must be true for a
name:

* The name must exist
* The name's zone file hash must be the hash of a well-formed DNS zone file
* The DNS zone file must be present in the BNS [Atlas Network](atlas_network.md)
* The DNS zone file must contain a `URI` resource record that points to a signed
  JSON Web Token
* The public key that signed the JSON Web Token (and is included with it) must
  hash to the address that owns the name

Not all names will have DIDs that resolve to public keys.  However, names created by the [Blockstack
Browser](https://github.com/blockstack/blockstack-browser) will have DIDs that
do.

Developers can programmatically resolve DIDs via the Python API:

```Python
>>> import blockstack
>>> blockstack.lib.client.resolve_DID('did:stack:v0:16EMaNw3pkn3v6f2BgnSSs53zAKH4Q8YJg-1', hostport='https://node.blockstack.org:6263')
{'public_key': '020fadbbcea0ff3b05f03195b41cd991d7a0af8bd38559943aec99cbdaf0b22cc8'}
```

A RESTful API is under development.
