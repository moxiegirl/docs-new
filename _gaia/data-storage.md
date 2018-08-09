---
layout: gaia
title: Data storage format
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
tags: othertag
author:
---

A gaia storage hub will store the written data _exactly_ as
given. This means that the storage hub _does not_ provide many
different kinds of guarantees about the data. It does not ensure that
data is validly formatted, contains valid signatures, or is
encrypted. Rather, the design philosophy is that these concerns are
client-side concerns. Client libraries (such as `blockstack.js`) are
capable of providing these guarantees, and we use a liberal definition of
the end-to-end principle to guide this design decision.
