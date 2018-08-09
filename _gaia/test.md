---
layout: gaia
title: Test your hub
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
tags: othertag
author:
---

To run the unit tests:
```bash
$ npm run test
```

To run _driver_ tests and the _integration_ tests, you have
to provide configuration for the drivers. Specify a driver config
file using the environment variables:

```bash
AZ_CONFIG_PATH=test.azure.json
S3_CONFIG_PATH=test.s3.json
```

These files are JSON files that only need to contain your credentials
and bucket. For example, an azure config could look like:

```javascript
{
  "azCredentials": {
    "accountName": "your-azure-account-name",
    "accountKey": "b64-account-key"
  },
  "bucket": "spokes"
}
```

To run the tests with the azure driver tests and integration tests included:

```bash
$ AZ_CONFIG_PATH=test.azure.json npm run test
```

This also provides an easy way to test your storage provider
credentials and setup. If your tests fail the first time that may be
because the bucket setup did not complete before the test exited. Wait
a minute and try the `npm run test` command again.

To configure the logging set the `argsTransport` fields in the config file. Here is a list of [logging configuration options](https://github.com/winstonjs/winston/blob/master/docs/transports.md).
