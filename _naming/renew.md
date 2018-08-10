---
layout: naming
title: NAME_RENEWAL
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---
Depending in the namespace rules, a name can expire.  For example, names in the
`.id` namespace expire after 2 years.  You need to send a `NAME_RENEWAL` every
so often to keep your name.

A `NAME_RENEWAL` costs both transaction fees and registration fees.  You will
pay the registration cost of your name to the namespace's designated burn address when you
renew it.  You can find this fee using the `/v1/prices/names/{name}` endpoint.

When a name expires, it enters a month-long "grace period" (5000 blocks).  It
will stop resolving in the grace period, and all of the above operations will
cease to be honored by the BNS consensus rules.  You may, however, send a
`NAME_RENEWAL` during this grace period to preserve your name.

If your name is in a namespace where names do not expire, then you never need to
use this transaction.

When you send a `NAME_RENEWAL`, you have the option of also setting a new public
key hash and a new zone file hash.  See the [transaction format](wire-format.md)
document for details on how to construct this transaction.
