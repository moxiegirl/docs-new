---
layout: naming
title: Namespace objects
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---

Namespaces are the top-level naming objects in BNS.
They control a few properties about the names within them:
* How expensive they are to register
* How long they last before they have to be renewed
* Who (if anyone) receives the name registration fees
* Who is allowed to seed the namespace with its initial names.

At the time of this writing, by far the largest BNS namespace is the `.id`
namespace.  Names in the `.id` namespace are meant for resolving user
identities.  Short names in `.id` are more expensive than long names, and have
to be renewed by their owners every two years.  Name registration fees are not
paid to anyone in particular---they are instead sent to a "black hole" where they are
rendered unspendable (the intention is to discourage ID sqautters).

Unlike DNS, *anyone* can create a namespace and set its properties.
Namespaces are created on a first-come first-serve basis, and once created, they
last forever.

However, creating a namespace is not free.  The namespace creator must *burn*
cryptocurrency to do so.  The shorter the namespace, the more cryptocurrency
must be burned (i.e. short namespaces are more valuable than long namespaces).
For example, it cost Blockstack PBC 40 BTC to create the `.id` namespace in
2015 (in transaction `5f00b8e609821edd6f3369ee4ee86e03ea34b890e242236cdb66ef6c9c6a1b281`).

Namespaces can be between 1 and 19 characters long, and are composed of the
characters `a-z`, `0-9`, `-`, and `_`.


### Using Namespaces

The intention is that each application can create its own BNS
namespace for its own purposes.  Applications can use namespaces for things like:

* Giving users a SSO system, where each user registers their public key under a
  username.  Blockstack applications do this with names in the `.id` namespace,
for example.
* Providing a subscription service, where each name is a 3rd party that provides
a service for users to subscribe to.  For example, names in
`.podcast` point to podcasts that users of the
[DotPodcast](https://dotpodcast.co) app can subscribe to.
* Implementing software licenses, where each name corresponds to an access key.
  Unlike conventional access keys, access keys implemented as names
can be sold and traded independently.  The licensing fee (paid as a name
registration) would be set by the developer and sent to a developer-controlled
blockchain address.

Names within a namespace can serve any purpose the developer wants.  The ability
to collect registration fees for 1 year after creating the namespace not only
gives developers the incentive to get users to participate in the app, but also
gives them a way to measure economic activity.

Developers can query individual namespaces and look up names within them using
the BNS API.  The API offers routes to do the following: 
