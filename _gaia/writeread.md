---
layout: gaia
title: Write-to and Read-from URL Guarantees
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
tags: othertag
author:
---

#A performance and simplicity oriented guarantee of the Gaia
specification is that when an application submits a _write_ to a URL
`https://myhub.service.org/store/foo/bar`, the application is guaranteed to
be able to read from a URL `https://myreads.com/foo/bar`. While the
_prefix_ of the read-from URL may change between the two, the suffix
must be the same as the write-to URL.

This allows an application to know _exactly_ where a written file can
be read from, given the read prefix. To obtain that read prefix,
the Gaia service defines an endpoint:

```
GET /hub_info/
```

which returns a JSON object with a `read_url_prefix`.


For example, if my service returns:

```javascript
{ ...,
  "read_url_prefix": "https://myservice.org/read/"
}
```

I know that if I submit a write request to:

```
https://myservice.org/store/1DHvWDj834zPAkwMhpXdYbCYh4PomwQfzz/0/profile.json
```

That I will be able to read that file from:

```
https://myservice.org/read/1DHvWDj834zPAkwMhpXdYbCYh4PomwQfzz/0/profile.json
```
