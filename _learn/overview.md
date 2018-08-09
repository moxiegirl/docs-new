---
layout: learn
title: What is Blockstack?
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
---
Blockstack is a new internet for decentralized apps where users own their data.

Blockstack applications follow a **can't-be-evil** design
philosophy.  They *cannot* alter, transfer, or revoke the user's identity, and
they *cannot* read or write the user's data without permission.  Blockstack provides the
platform, network, and SDKs for building can't-be-evil
applications using existing Web tools.
If you are Web developer, all of your skills are
immediately transferrable to Blockstack.

Blockstack applications look and feel like traditional Web applications.
Under the hood they use Blockstack APIs for user authentication and storage.
Blockstack handles user authentication using the [Blockstack Naming
Service](docs/blockstack_naming_service.md)
(BNS), a decentralized naming and public key infrastructure built on top of the Bitcoin
blockchain.  It handles storage using [Gaia](https://github.com/blockstack/gaia), a scalable decentralized
key/value storage system that looks and feels like `localStorage`,
but lets users securely store and share application data
via existing storage systems like Dropbox or S3.

Blockstack applications differ from traditional Web applications in two key
ways.  First, **users own their identities**.
The [Blockstack Browser](https://github.com/blockstack/blockstack-browser)
gives users direct control over their private keys and profile data,
and fulfills the role of a SSO provider to Blockstack apps.
Blockstack Core provides BNS as a way for users to discover each other's public
keys.

The second key difference is that **users own their data**.  Users
choose *where* their app data gets hosted, and *who* is allowed to read it.
Gaia loads and stores data with the user's
chosen storage providers, and automatically signs and encrypts it with
their app-specific keys.  Only the intended recipients can authenticate and read
the data; the storage providers are treated as untrusted middlemen.

### Why use Blockstack?

Blockstack is a win/win for users and developers.  Users are not locked into
apps or services.  Instead, users take their identities and data with them from app to app.
Apps can only read user data if the user chooses to allow it.  If an app goes
offline, the user still keeps their data.  If users find a better app, they
can seamlessly switch over to using it.  Because data is end-to-end encrypted
and hosted separately from the app, data breaches are inconsequential to users
because there is nothing for hackers to steal.

Developers benefit from Blockstack as well.  Apps are simpler to build with
Blockstack and require less operational overhead, since they no longer have to
store user data.  Many non-trivial applications can be implemented
as single-page Javascript applications using
[blockstack.js](https://github.com/blockstack/blockstack.js), and deployed as a
static Web page.  The Blockstack API is small, simple, and straightforward to
integrate into existing Web apps.
