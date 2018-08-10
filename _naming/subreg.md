---
layout: naming
title: Subdomain registrars
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---
Because subdomain names are cheap, developers may be inclined to run
subdomain registrars on behalf of their applications.  For example,
the name `personal.id` is used to register Blockstack application users without
requiring them to spend any Bitcoin.

We supply a reference
implementation of a [BNS Subdomain Registrar](https://github.com/blockstack/subdomain-registrar)
to help developers broadcast subdomain operations.  Users would still own their
subdomain names; the registrar simply gives developers a convenient way for them
to register and manage them in the context of a particular application.
Please see the [tutorial on running a subdomain registrar](subdomains.md) for
details on how to use it.
