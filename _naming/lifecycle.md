---
layout: naming
title: Subdomain lifecycle
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

Note that `1yeardaily.verified.podcast` has a different public key
hash (address) than `verified.podcast`.  A BNS node will only process a
subsequent subdomain operation on `1yeardaily.verified.podcast` if it includes a
signature from this address's private key.  `verified.podcast` cannot generate
updates; only the owner of `1yeardaily.verified.podcast can do so`.

The lifecycle of a subdomain and its operations is shown in Figure 2.

```
   subdomain                  subdomain                  subdomain
   creation                   update                     transfer
+----------------+         +----------------+         +----------------+
| cicero         |         | cicero         |         | cicero         |
| owner="1Et..." | signed  | owner="1Et..." | signed  | owner="1cJ..." |
| zf0="7e4..."   |<--------| zf0="111..."   |<--------| zf0="111..."   |<---- ...
| seqn=0         |         | seqn=1         |         | seqn=2         |
|                |         | sig="xxxx"     |         | sig="xxxx"     |
+----------------+         +----------------+         +----------------+
        |                          |                          |
        |        off-chain         |                          |
~ ~ ~ ~ | ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~|~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ | ~ ~ ~ ~ ~ ~ ~ ...
        |         on-chain         |                          |
        V                          V (zone file hash    )     V
+----------------+         +----------------+         +----------------+
| res_publica.id |         |    jude.id     |         | res_publica.id |
|  NAME_UPDATE   |<--------|  NAME_UPDATE   |<--------|  NAME_UPDATE   |<---- ...
+----------------+         +----------------+         +----------------+
   blockchain                 blockchain                 blockchain
   block                      block                      block


Figure 2:  Subdomain lifetime with respect to on-chain name operations.  A new
subdomain operation will only be accepted if it has a later "sequence=" number,
and a valid signature in "sig=" over the transaction body.  The "sig=" field
includes both the public key and signature, and the public key must hash to
the previous subdomain operation's "addr=" field.

Thesubdomain-creation and subdomain-transfer transactions for
"cicero.res_publica.id" are broadcast by the owner of "res_publica.id".
However, any on-chain name ("jude.id" in this case) can broadcast a subdomain
update for "cicero.res_publica.id".
```

Subdomain operations are ordered by sequence number, starting at 0.  Each new
subdomain operation must include:

* The next sequence number
* The public key that hashes to the previous subdomain transaction's address
* A signature from the corresponding private key over the entire subdomain
  operation.

If two correctly-signed but conflicting subdomain operations are discovered
(i.e. they have the same sequence number), the one that occurs earlier in the
blockchain's history is accepted.  Invalid subdomain operations are ignored.

Combined, this ensures that a BNS node with all of the zone files with a given
subdomain's operations will be able to determine the valid sequence of
state-transitions it has undergone, and determine the current zone file and public
key hash for the subdomain.
