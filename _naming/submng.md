---
layout: naming
title: Subdomain creation and management
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

Unlike an on-chain name, a subdomain owner needs an on-chain name owner's help
to broadcast their subdomain operations.  In particular:
* A subdomain-creation transaction can only be processed by the owner of the on-chain
name that shares its suffix.  For example, only the owner of `res_publica.id`
can broadcast subdomain-creation transactions for subdomain names ending in
`.res_publica.id`.
* A subdomain-transfer transaction can only be broadcast by the owner of the
on-chain name that created it.  For example, the owner of
`cicero.res_publica.id` needs the owner of `res_publica.id` to broadcast a
subdomain-transfer transaction to change `cicero.res_publica.id`'s public key.
* In order to send a subdomain-creation or subdomain-transfer, all
  of an on-chain name owner's zone files must be present in the Atlas network.
  This lets the BNS node prove the *absence* of any conflicting subdomain-creation and
subdomain-transfer operations when processing new zone files.
* A subdomain update transaction can be broadcast by *any* on-chain name owner,
  but the subdomain owner needs to find one who will cooperate.  For example,
the owner of `verified.podcast` can broadcast a subdomain-update transaction
created by the owner of `cicero.res_publica.id`.

That said, to create a subdomain, the subdomain owner generates a
subdomain-creation operation for their desired name
and gives it to the on-chain name owner.
The on-chain name owner then uses Atlas to
broadcast it to all other BNS nodes.

Once created, a subdomain owner can use any on-chain name owner to broadcast a
subdomain-update operation.  To do so, they generate and sign the requisite
subdomain operation and give it to an on-chain name owner, who then packages it
with other subdomain operations into a DNS zone file
and sends them all out on the Atlas network.

If the subdomain owner wants to change the address of their subdomain, they need
to sign a subdomain-transfer operation and give it to the on-chain name owner
who created the subdomain.  They then package it into a zone file and broadcast
it.
