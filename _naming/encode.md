---
layout: naming
title: DID encoding
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---
Every name and subdomain in BNS has a DID.  The encoding is slightly different
for subdomains, so the software can determine which code-path to take.

* For on-chain BNS names, the `{address}` is the same as the Bitcoin address
  that owns the name.  Currently, both version byte 0 and version byte 5
addresses are supported (i.e. addresses starting with `1` or `3`, meaning `p2pkh` and
`p2sh` addresses).

* For off-chain BNS subdomains, the `{address}` has version byte 63 for
  subdomains owned by a single private key, and version byte 50 for subdomains
owned by a m-of-n set of private keys.  That is, subdomain DID addresses start
with `S` or `M`, respectively.

The `{index}` field for a subdomain's DID is distinct from the `{index}` field
for a BNS name's DID, even if the same created both names and subdomains.
For example, the name `abcdefgh123456.id` has the DID `did:stack:v0:16EMaNw3pkn3v6f2BgnSSs53zAKH4Q8YJg-0`,
because it was the first name created by `16EMaNw3pkn3v6f2BgnSSs53zAKH4Q8YJg`.
However, `16EMaNw3pkn3v6f2BgnSSs53zAKH4Q8YJg` *also* created `jude.statism.id`
as its first subdomain name.  The DID for `jude.statism.id` is
`did:stack:v0:SSXMcDiCZ7yFSQSUj7mWzmDcdwYhq97p2i-0`.  Note that the address
`SSXMcDiCZ7yFSQSUj7mWzmDcdwYhq97p2i` encodes the same public key hash as the address
`16EMaNw3pkn3v6f2BgnSSs53zAKH4Q8YJg` (the only difference between these two
strings is that the first is base58check-encoded with version byte 0, and the
second is encoded with version byte 63).

You can see this play out in practice with the following code snippit:

```python
>>> import blockstack
>>> blockstack.lib.client.get_name_record('jude.statism.id', hostport='https://node.blockstack.org:6263')['address']
u'16EMaNw3pkn3v6f2BgnSSs53zAKH4Q8YJg'
>>> import virtualchain
>>> virtualchain.address_reencode('16EMaNw3pkn3v6f2BgnSSs53zAKH4Q8YJg', version_byte=63)
'SSXMcDiCZ7yFSQSUj7mWzmDcdwYhq97p2i'
>>> blockstack.lib.client.resolve_DID('did:stack:v0:SSXMcDiCZ7yFSQSUj7mWzmDcdwYhq97p2i-0', hostport='https://node.blockstack.org:6263')
{'public_key': '020fadbbcea0ff3b05f03195b41cd991d7a0af8bd38559943aec99cbdaf0b22cc8'}
```
