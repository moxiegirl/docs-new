---
layout: gaia
title: Run a Gaia Hub
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
tags: othertag
author:
---

To get started running a gaia hub, execute the following:

```bash
$ git clone https://github.com/blockstack/gaia.git
$ cd gaia/hub/
$ npm install
$ cp ./config.sample.json ./config.json
# Edit the config file and add in your azure or aws credentials
$ npm run start
```

## Note on SSL

We *strongly* recommend that you deploy your Gaia hub with SSL enabled. Otherwise, the tokens used to authenticate with the Gaia hub may be stolen by attackers, which could allow them to execute writes on your behalf.
