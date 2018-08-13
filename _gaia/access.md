---
layout: gaia
title: Address-based Access-Control
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
tags: featured
author:
---

Access control in a gaia storage hub is performed on a per-address
basis.  Writes to URLs `/store/<address>/<file>` are only allowed if
the writer can demonstrate that they control _that_ address. This is
achieved via an authentication token, which is a message _signed_ by
the private-key associated with that address. The message itself is a
challenge-text, returned via the `/hub_info/` endpoint.

## V1 Authentication Scheme

The V1 authentication scheme uses a JWT, prefixed with `v1:` as a
bearer token in the HTTP authorization field. The expected JWT payload
structure is:

```
{
 'type': 'object',
 'properties': {
   'iss': { 'type': 'string' }
   'exp': { 'type': 'IntDate' }
   'gaiaChallenge': { 'type': 'string' }
 }
 'required': [ 'iss', 'gaiaChallenge' ]
}
```

In addition to `iss`, `exp`, and `gaiaChallenge` claims, clients may
add other properties (e.g., a `salt` field) to the payload, and they will
not affect the validity of the JWT. Rather, the validity of the JWT is checked
by ensuring:

1. That the JWT is signed correctly by verifying with the pubkey hex provided as
`iss`
2. That `iss` matches the address associated with the bucket.
3. That `gaiaChallenge` is equal to the server's challenge text.
4. That the epoch time `exp` is greater than the server's current epoch time.

## Legacy authentication scheme

In more detail, this signed message is:

```
BASE64({ "signature" : ECDSA_SIGN(SHA256(challenge-text)),
         "publickey" : PUBLICKEY_HEX })
```

Currently, challenge-text must match the _known_ challenge-text on
the gaia storage hub. However, as future work enables more extensible
forms of authentication, we could extend this to allow the auth
token to include the challenge-text as well, which the gaia storage hub
would then need to also validate.
