<!--- app-name: node-mongo-app; -->

# node-mongo-app

node-mongo-app is a simple nodejs application connecting to a mongodb.

[source code is taken from here](https://github.com/bradtraversy/docker-node-mongo)
                           

## Introduction

This chart bootstraps a nodejs deployment and mongodb on a [Kubernetes](https://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- Git 

## Installing the Chart

To install the chart with the release name `chart-example` do the following procudure:

1.Copy the git repo into your localhost

```bash
$ git clone https://github.com/tomwiz1/node-mongo-app.git
```

2.Move to the chart directory and run the helm chart

```bash
$ cd node-mongo-app
$ helm install chart-example node-mongo-app-chart/
```

The output you get from the helm install should look like this :
```bash
NAME: chart-example
LAST DEPLOYED: Thu Mar 24 23:56:22 2022
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services chart-example-node-mongo-app-chart)
  echo http://localhost:$NODE_PORT
```

3. In order to get the specific NodePort the application is exposed on we need to run the output result:
```bash
$ export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services chart-example-node-mongo-app-chart)
$ echo http://localhost:$NODE_PORT
```

4. Check if the Application is accesible at the URL given in the previous step. 


## Uninstalling the Chart

To uninstall/delete the `chart-example` chart:

```bash
$ helm delete chart-example
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

### Nodejs parameters

| Name                     | Description                                                                                               | Value           |
| ------------------------ | --------------------------------------------------------------------------------------------------------- | --------------- |
| `replicaCount`           | String to partially override mongodb.fullname template (will maintain the release name)                   | `1`             |
| `pullPolicy`             | String to fully override mongodb.fullname template                                                        | `Always`            |
| `appPort`                | Default Kubernetes cluster domain                                                                         | `3000` |
| `extraDeploy`            | Array of extra objects to deploy with the release                                                         | `[]`            |
| `commonLabels`           | Add labels to all the deployed resources (sub-charts are not considered). Evaluated as a template         | `{}`            |
| `commonAnnotations`      | Common annotations to add to all Mongo resources (sub-charts are not considered). Evaluated as a template | `{}`            |
| `diagnosticMode.enabled` | Enable diagnostic mode (all probes will be disabled and the command will be overridden)                   | `false`         |
| `diagnosticMode.command` | Command to override all containers in the deployment                                                      | `["sleep"]`     |
| `diagnosticMode.args`    | Args to override all containers in the deployment                                                         | `["infinity"]`  |


### MongoDB(&reg;) parameters

[mongodb paramters](https://github.com/bitnami/charts/blob/master/bitnami/mongodb)
