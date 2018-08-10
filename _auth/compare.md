---
layout: auth
title: Compared to other stores
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

Atlas is not the only peer-to-peer content-addressible chunk store in existance.  The following
feature table describes Atlas in relation to other popular chunk stores.

| **Features**                | Atlas | BitTorrent | [DAT](https://datproject.org/) | [IPFS](https://ipfs.io) | [Swarm](https://github.com/ethersphere/swarm) |
|-----------------------------|-------|------------|--------------------------------|-------------------------|-----------------------------------------------|
| Each peer stores all chunks | X     | X          |        |                         |                                               |
| Replicas are permanent [1]  | X     | X          | X  |    |    |
| Replicas are free           |       | X          | X  | X   |   |
| Sybil-resistant chunk discovery | X | X          |    |    | X |
| Sybil-resistant peer discovery  | X |  |  |  |  |
| Fixed chunk size             | X      |          | X   |  X  |   X  |

[1] Here, "permanent" means that once a peer has data, they will never evict it
as part of the protocol.
