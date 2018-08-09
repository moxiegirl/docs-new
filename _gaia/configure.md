---
layout: gaia
title: Configure a Hub
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
tags: othertag
author:
---

### Driver Selection

The Gaia hub currently supports the following drivers:

```
'aws' == Amazon S3
'azure' == Azure Blob Storage
'disk' == Local disk (you must set up static web-hosting to point at this driver)
'google-cloud' === Google Cloud Storage
```

Set the driver you wish to use in your `config.json` file with the `driver` parameter. Many drivers additionally accept the `bucket` parameter, which controls the bucket name that files should be written to.

These driver may require you to provide additional credentials for performing writes to the backends. See `config.sample.json` for fields for those credentials. In some cases, the driver can use a system configured credential for the backend (e.g., if you are logged into your AWS CLI account, and run the hub from that environment, it won't need to read credentials from your `config.json`).

*Note:* The disk driver requires a *nix like filesystem interface, and will not work correctly when trying to run in a Windows environment.

### The readURL parameter

By default, the gaia hub drivers will return read URLs which point directly at the written content. For example, an S3 driver would return the URL directly to the S3 file. However, if you configure a CDN or domain to point at that same bucket, you can use the `readURL` parameter to tell the gaia hub that files can be read from the given URL. For example, the `hub.blockstack.org` Gaia Hub is configured to return a read URL that looks like `https://gaia.blockstack.org/hub/`.

Unset this configuration parameter if you do not intend to deploy any caching.

### Minimum Proofs Requirement

The gaia hub can also be configured to require a minimum number of social proofs in a user's profile to accept writes from that user. This can be used as a kind of spam-control mechanism. However, we recommend for the smoothest operation of your gaia hub, to set the  `proofsConfig.proofsRequired` configuration key to `0`.

### Install Gaia Hub as Executable

To install the Gaia hub as an executable program (required for integration
testing), do the following:

```bash
$ cd gaia/hub
$ sudo npm i -g # or, "sudo npm link"
$ which blockstack-gaia-hub
/usr/bin/blockstack-gaia-hub
```

If you intend to run a Gaia hub in production, you will still need to generate a
`config.json` file per the above instructions.

### Deploy the Hub with Docker, nginx

First have `docker`,`nginx` and `certbot` installed on a server with a FQDN pointed to it. The following guides should help you get this setup.

- [Install `nginx`](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04)
- [Install `docker`](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-16-04)
- [Install `certbot`](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04) (do not run the setup yet!)

Then do the following:

- Make a folder `$HOME/hub` and copy the configuration file `config.sample.json` to `$HOME/hub/config.json` and add in your desired configuration.
- Copy `nginx.conf.sample` to `$HOME/hub/nginx.conf` and replace `hub.example.com` with your FQDN.
- `sudo rm /etc/nginx/sites-enabled/default && sudo ln $HOME/hub/nginx.conf /etc/nginx/sites-enabled/default`
- Finish `certbot` setup and cert generation
- Pull the docker image and start an instance of the container:

```bash
$ docker pull quay.io/blockstack/gaia-hub:latest
$ docker run -d --restart=always -v $HOME/hub/config.json:/src/hub/config.json -p 3000:3000 -e CONFIG_PATH=/src/hub/config.json quay.io/blockstack/gaia-hub:latest
# Now you can test the hub! The exact output will depend on your configuration
$ curl https://hub.example.com/hub_info | jq
```
