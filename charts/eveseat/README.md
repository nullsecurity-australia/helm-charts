# EVE SeAT

[SeAT](https://github.com/eveseat/seat) A Simple, EVE Online API Tool and Corporation Manager 

SeAT is a simple, [EVE Online](https://www.eveonline.com) Corporation and API management tool. SeAT allows you to keep an eye on all things related to your corporation; from wallets, to mail, to assets for both characters and corporations.

## TL;DR
```bash
$ helm repo add nullsec https://helm.nullcontent.net
$ helm install nullsec/eveseat
```

## Introduction

This chart is a maintained version of [tarioch's chart](https://github.com/tarioch/helm/tree/master/docs)

This chart bootstraps [SeAT](https://github.com/eveseat/seat) on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

* Persistent volume provisioner support in the underlying infrastructure

## Installing the Chart
To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release nullsec/eveseat
```

The command deploys SeAT on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the main parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

|             Parameter                     |                     Description                     |                              Default                              |
|-------------------------------------------|-----------------------------------------------------|-------------------------------------------------------------------|
| `global.app.key`                          | Encryption key                                      | random                                                            |
| `global.app.url`                          | URL where the application will be deployed          | ``                                                                |
| `global.eve.clientId`                     | EVE Client Id from Dev Section                      | ``                                                                |
| `global.eve.secret`                       | EVE Secret from Dev Section                         | ``                                                                |
| `global.mail.host`                        | Host for sending mails                              | ``                                                                |
| `global.mail.port`                        | Port for sending mails                              | `587`                                                             |
| `global.mail.username`                    | Username for sending mails                          | ``                                                                |
| `global.mail.password`                    | Password for sending mails                          | ``                                                                |
| `global.mail.encryption`                  | Encrytpion for sending mails connection             | `ntls`                                                            |
| `global.mail.fromAddress`                 | From address for sending mails                      | ``                                                                |
| `global.mail.fromName`                    | From name for sending mails                         | ``                                                                |
| `global.seat.plugins`                     | SeAT plugins to install                             | ``                                                                |
| `mariadb.rootUser.password`               | DB root password                                    | random                                                            |
| `mariadb.db.password`                     | DB password                                         | random                                                            |
| `redis.password`                          | Redis password                                      | random                                                            |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set global.app.url=https://foobar.example.tld,global.eve.clientId=secret,global.eve.secret=secret \
      nullsec/eveseat
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## DB Backup/Restore

To backup the database, first you will have to find the name of the pod for the database, this is named releaseName-mariadb. e.g. if the releaseName is eveseat, it would be

```bash
$ kubectl exec eveseat-mariadb-0 -- sh -c 'exec mysqldump "$MARIADB_DATABASE" -u"$MARIADB_USER" -p"$MARIADB_PASSWORD"' | gzip > seat_backup.sql.gz
```

and to restore

```bash
$ zcat seat_backup.sql.gz | kubectl exec -i eveseat-mariadb-0 -- sh -c 'exec mysql "$MARIADB_DATABASE" -u"$MARIADB_USER" -p"$MARIADB_PASSWORD"'
```

