---
layout: gaia
title: HTTP API
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
tags: othertag
author:
---

The Gaia storage API defines only three endpoints.

```
GET ${read-url-prefix}/${address}/${path}
```

This returns the data stored by the gaia hub at `${path}`. In order
for this to be usable from web applications, this read path _must_
set the appropriate CORS headers. The HTTP Content-Type of the file
should match the Content-Type of the corresponding write.

```
POST ${hubUrl}/store/${address}/${path}
```

This performs a write to the gaia hub at `${path}`.

On success, it returns a `202` status, and a JSON object:

```javascript
{
 "publicUrl": "${read-url-prefix}/${address}/${path}"
}
```

The `POST` must contain an authentication header with a bearer token.
The bearer token's content and generation is described in
the [access control](#address-based-access-control) section of this
document.

```
GET ${hubUrl}/hub_info/
```

Returns a JSON object:

```javascript
{
 "challenge_text": "text-which-must-be-signed-to-validate-requests",
 "read_url_prefix": "${read-url-prefix}"
 "latest_auth_version": "v1"
}
```

The latest auth version allows the client to figure out which auth versions the
gaia hub supports.
