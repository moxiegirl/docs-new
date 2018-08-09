---
layout: gaia
title: Driver Model
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
tags: othertag
author:
---
Gaia hub drivers are fairly simple. The biggest requirement is the ability
to fulfill the _write-to/read-from_ URL guarantee. As currently implemented
a gaia hub driver must implement the following two functions:

```javascript
/**
 * Performs the actual write of a file to `path`
 *   the file must be readable at `${getReadURLPrefix()}/${storageToplevel}/${path}`
 *
 * @param { String } options.path - path of the file.
 * @param { String } options.storageToplevel - the top level directory to store the file in
 * @param { String } options.contentType - the HTTP content-type of the file
 * @param { stream.Readable } options.stream - the data to be stored at `path`
 * @param { Integer } options.contentLength - the bytes of content in the stream
 * @returns { Promise } that resolves to the public-readable URL of the stored content.
 */


performWrite (options: { path, contentType,
                         stream, contentLength: Number })

/**
 * Return the prefix for reading files from.
 *  a write to the path `foo` should be readable from
 *  `${getReadURLPrefix()}foo`
 * @returns {String} the read url prefix.
 */
getReadURLPrefix ()
```
