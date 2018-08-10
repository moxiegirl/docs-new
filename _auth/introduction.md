---
layout: auth
title: Where to start
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

While the Blockstack software stack expects that Atlas-hosted data is made up of
DNS zone files, Atlas itself does not enforce this (nor does it care about the
format of its chunks).  It is designed as a general-purpose chunk store.
Nevertheless, the ubiquitous use of Atlas to store data as DNS zone files has
had an influence on its API design---fields and method names frequently allude
to zone files and zone file hashes.  This is intentional.

The [public BNS API endpoint](https://core.blockstack.org) does not support
resolving Atlas chunks that do not encode Gaia routing information or subdomain
information.  To directly interact with Atlas, developers will need to install
[Blockstack Core](https://github.com/blockstack/blockstack-core) and use its
Python client libraries for these examples.
