# EVE SeAT

[SeAT](https://github.com/eveseat/seat) A Simple, EVE Online API Tool and Corporation Manager

SeAT is a simple, [EVE Online](https://www.eveonline.com) Corporation and API management tool. SeAT allows you to keep an eye on all things related to your corporation; from wallets, to mail, to assets for both characters and corporations.

## TL;DR
```bash
$ helm repo add nullsec https://helm.nullcontent.net
# Do some fun values.yaml stuff here
$ helm install nullsec/eveseat
$ helm install nullsec/eveseat-workers
```

## Introduction

This chart is a maintained version of [tarioch's chart](https://github.com/tarioch/helm/tree/master/docs)

This chart bootstraps [SeAT](https://github.com/eveseat/seat) on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

* An existing SeAT Deployment !!IN THE SAME NAMESPACE!!

## Installing the Chart
To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release nullsec/eveseat-workers
```

The command deploys a set of SeAT worker containers on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the main parameters that can be configured during installation.

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
| `seatdeploymentname`                      | Name of your existing SeAT k8s deployment           | ``                                                                |`
| `global.app.url`                          | URL where the application will be deployed          | ``                                                                |
| `global.mail.host`                        | Host for sending mails                              | ``                                                                |
| `global.mail.port`                        | Port for sending mails                              | `587`                                                             |
| `global.mail.username`                    | Username for sending mails                          | ``                                                                |
| `global.mail.password`                    | Password for sending mails                          | ``                                                                |
| `global.mail.encryption`                  | Encrytpion for sending mails connection             | `ntls`                                                            |
| `global.mail.fromAddress`                 | From address for sending mails                      | ``                                                                |
| `global.mail.fromName`                    | From name for sending mails                         | ``                                                                |
| `global.seat.plugins`                     | SeAT plugins to install                             | ``                                                                |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set global.app.url=https://foobar.example.tld,global.eve.clientId=secret,global.eve.secret=secret \
      nullsec/eveseat
```

> **Tip**: You can use the default [values.yaml](values.yaml)

