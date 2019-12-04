# Docker BURP
This repository contains useful images to deploy a BURP Backup system using Docker.

## burp-client
This image is used in order to create backups connecting to a BURP server. One interesting use case is the possibility to deploy multiple images in a system having multiple connections simultaneously.

Usage:

```
docker run -it -v <host-conf-dir>:/etc/burp/ -v <source-dir>:<docker-source> dlbcn/burp-client
```

NOTE: `<docker-source>` is set inside `/etc/burp/burp.conf`