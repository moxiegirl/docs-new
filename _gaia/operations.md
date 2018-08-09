---
layout: gaia
title: Operation of a Gaia Hub
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
tags: othertag
author:
---

## Configuration files

A configuration JSON file should be stored either in the top-level directory
of the hub server, or a file location may be specified in the environment
variable `CONFIG_PATH`.

An example configuration file is provided in (./hub/config.sample.json)
You can specify the logging level, the number of social proofs required
for addresses to write to the system, the backend driver, the credentials
for that backend driver, and the readURL for the storage provider.

### Private hubs

A private hub services requests for a single user. This is controlled
via _whitelisting_ the addresses allowed to write files. In order to
support application storage, because each application uses a different
app- and user-specific address, each application you wish to use must
be added to the whitelist separately. An extensible authentication
approach would obviate the need for this manual whitelisting, but that
remains as future work.

### Open-membership hubs

An open-membership hub will allow writes for _any_ address top-level directory,
each request will still be validated such that write requests must provide valid
authentication tokens for that address. Operating in this mode is recommended
for service and identity providers who wish to support many different users.

In order to limit the users that may interact with such a hub to users
who provide social proofs of identity, we support an execution mode
where the hub checks that a user's profile.json object contains
_social proofs_ in order to be able to write to other locations. This
can be configured via the [config.json](#configuration-files).
