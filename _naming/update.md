---
layout: naming
title: NAME_UPDATE
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

A `NAME_UPDATE` transaction changes the name's zone file hash.  You would send
one of these transactions if you wanted to change the name's zone file contents.
For example, you would do this if you want to deploy your own [Gaia
hub](https://github.com/blockstack/gaia) and want other people to read from it.

A `NAME_UPDATE` transaction is generated from the name, a recent [consensus
hash](#bns-forks), and the new zone file hash.  The reference clients gather
this information automatically.  See the [transaction format](wire-format.md)
document for details on how to construct this transaction.
