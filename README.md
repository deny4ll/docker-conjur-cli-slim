# Introduction

This is a docker image with the conjur-cli pre installed using Alpine Linux.


# conjur-cli

Command-line interface for Conjur.

*NOTE*: Conjur v4 users should use the `v5.x.x` release path. Conjur CLI `v6.0.0` only supports Conjur v5 and newer.

A complete reference guide is available at [conjur.org](https://www.conjur.org).

## Docker images

[![Docker Build Status](https://img.shields.io/badge/docker%20buuild-passing-brightgreen.svg)](https://hub.docker.com/r/denyall/conjur-cli/)

Images for development/experimental use are automatically built [on docker hub](https://hub.docker.com/r/denyall/conjur-cli/).

Note these images are not subject to any QA at the moment and so should never be used in production, especially without specific image id pin.



## How to Use it.

### Create a Volume for persistent data

```
docker volume create conjur-conf
```

### Run the container

```
docker run -it --rm  --mount source=conjur-conf,destination=/root conjur-cli:latest
```


### Configure Conjur

In order to use the conjur-cli you need ton configure it against your Conjur Master

Inside the continer run this:

```
conjur init

Enter the hostname (and optional port) of your Conjur endpoint: https://Conjur-int-master.snidigital.com

SHA1 Fingerprint=01:6F:88:B1:72:E6:2D:88:55:E5:52:89:A9:03:39:77:65:1C:0B:BF

Please verify this certificate on the appliance using command:
                openssl x509 -fingerprint -noout -in ~conjur/etc/ssl/conjur.pem

Trust this certificate (yes/no): yes
Wrote certificate to /root/conjur-conjurpoc.pem
Wrote configuration to /root/.conjurrc
```

Done!

now you can try login into the conjur-master

```
root@9f38771a23e3:~# conjur authn login
Enter your username to log into Conjur: testuser
Please enter your password (it will not be echoed):
Logged in
root@9f38771a23e3:~#

```

