---
layout: naming
title: Why are BNS names powerful?
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

We rely on naming systems in everyday life, and they play a critical
role in many different applications.  For example, when you look up a
friend on social media, you are using the platform's naming service to resolve
their name to their profile.  When you look up a website, you are using the
Domain Name Service to
resolve the hostname to its host's IP address.  When you check out a Git branch, you
are using your Git client to resolve the branch name to a commit hash.
When you look up someone's PGP key on a keyserver, you are resolving
their key ID to their public key.

What kinds of things do we want to be true about names?  In BNS, names are
globally unique, names are human-meaningful, and names are strongly-owned.
However, if you look at these examples, you'll see that each of them only
guarantees *two* of these properties.  This limits how useful they can be.

* In DNS and social media, names are globally unique and human-readable, but not
strongly-owned.  The system operator has the
final say as to what each names resolves to.
   * **Problem**:  Clients must trust the system to make the right
     choice in what a given name resolves to.  This includes trusting that
     no one but the system administrators can make these changes.

* In Git, branch names are human-meaningful
and strongly-owned, but not globally unique.  Two different Git nodes may resolve the same
branch name to different unrelated repository states.
   * **Problem**:  Since names can refer to conflicting state, developers
     have to figure out some other mechanism to resolve ambiguities.  In Git's
     case, the user has to manually intervene.

* In PGP, names are key IDs.  They are
are globally unique and cryptographically owned, but not human-readable.  PGP
key IDs are derived from the keys they reference.
   * **Problem**:  These names are difficult for most users to
     remember since they do not carry semantic information relating to their use in the system.

BNS names have all three properties, and none of these problems.  This makes it a
powerful tool for building all kinds of network applications.  With BNS, we
can do the following and more:

* Build domain name services where hostnames can't be hijacked.
* Build social media platforms where user names can't be stolen by phishers.
* Build version control systems where repository branches do not conflict.
* Build public-key infrastructure where it's easy for users to discover and
  remember each other's keys.
