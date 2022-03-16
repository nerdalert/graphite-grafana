# Container image for go-carbon, carbonapi and grafana

## Quick Start

- Using Docker or Podman, run the following. Once up and running point your browser to the container address to view the grafana UI.

```sh
docker run -d \
   --name graphite-grafana \
   --restart=always \
   -p 80:80 \
   -p 2003-2004:2003-2004 \
   quay.io/networkstatic/graphite-grafana
 
 # or Podman
 sudo sysctl net.ipv4.ip_unprivileged_port_start=80
 podman run -d \
    --name graphite-grafana \
    --restart=always \
    -p 80:80 \
    -p 2003-2004:2003-2004 \
    quay.io/networkstatic/graphite-grafana
```

### Includes the following components

* [Nginx](http://nginx.org/) - reverse proxies Grafana dashboard
* [Grafana](http://www.grafana.com/) - front-end dashboard
* [Go-carbon](https://github.com/lomik/go-carbon) - Golang implementation of Graphite/Carbon server
* [Carbonapi](https://github.com/go-graphite/carbonapi) - Golang implementation of Graphite-web

### Mapped Ports

Host | Container | Service
---- | --------- | -------------------------------------------------------------------------------------------------------------------
  80 |        80 | [grafana](http://docs.grafana.org/)
2003 |      2003 | [carbon receiver - plaintext](http://graphite.readthedocs.io/en/latest/feeding-carbon.html#the-plaintext-protocol)
2004 |      2004 | [carbon receiver - pickle](http://graphite.readthedocs.io/en/latest/feeding-carbon.html#the-pickle-protocol)

### Exposed Ports

Container | Service
--------- | -------------------------------------------------------------------------------------------------------------------------
   8081   | [carbonapi](https://github.com/go-graphite/carbonapi/blob/master/doc/configuration.md#general-configuration-for-carbonapi)

### Mounted Volumes

Host              | Container                  | Notes
----------------- | -------------------------- | -------------------------------
DOCKER ASSIGNED   | /etc/go-carbon             | go-carbon configs (see )
DOCKER ASSIGNED   | /var/lib/graphite          | graphite file storage
DOCKER ASSIGNED   | /etc/nginx                 | nginx config
DOCKER ASSIGNED   | /etc/grafana               | Grafana config
DOCKER ASSIGNED   | /etc/carbonapi             | Carbonapi config
DOCKER ASSIGNED   | /etc/logrotate.d           | logrotate config
DOCKER ASSIGNED   | /var/log                   | log files
