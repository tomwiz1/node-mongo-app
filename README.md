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

2.Move to the chart directory and run the helm chart while creating new namespace:

```bash
$ cd node-mongo-app
$ helm install --create-namespace -n node-app chart-example ./
```

The output you get from the helm install should look like this :
```bash
NAME: example-chart
LAST DEPLOYED: Fri Mar 25 18:26:50 2022
NAMESPACE: node-app
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export NODE_PORT=$(kubectl get --namespace node-app -o jsonpath="{.spec.ports[0].nodePort}" services example-chart-node-mongo-app-chart)
  echo http://localhost:$NODE_PORT
```

3. In order to get the specific NodePort the application is exposed on we need to run the output result:
```bash
$ export NODE_PORT=$(kubectl get --namespace node-app -o jsonpath="{.spec.ports[0].nodePort}" services example-chart-node-mongo-app-chart)
$ echo http://localhost:$NODE_PORT
```

4. Check if the Application is accesible at the URL given in the previous step. 


## Uninstalling the Chart

To uninstall/delete the `chart-example` chart:

```bash
$ helm uninstall chart-example
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

### Nodejs parameters

| Name                                         | Description                                                                                               | Value                    |
| -------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------ |
| `replicaCount`                               | Number of pods to be deployed                                                                             | `1`                      |
| `image.repository`                           | The source registry for the Docker image                                                                  | `tomwi/nodejs_app        |
| `image.pullPolicy`                           | The Kubernetes pull policy                                                                                | `Always`                 |
| `image.tag`                                  | The Kubernetes pull policy                                                                                | `1.0`                    |
| `appPort`                                    | node-app Port                                                                                             | `3000`                   |
| `imagePullSecrets`                           | Specify docker-registry secret names as an array                                                          | `[]`                     |
| `nameOverride`                               | String to partially override node-mongo-app-chart.fullname template (will maintain the release name)      | `""`                     |
| `fullnameOverride`                           | String to fully override mongodb.fullname template                                                    	   | `""`                     |
| `serviceAccount.create`                      | Enable creation of ServiceAccount for Charts pods                                                         | `false`                  |
| `serviceAccount.annotations`                 | Additional Service Account annotations                                                                    | `{}`                     |
| `serviceAccount.name`                        | Name of the created serviceAccount                                                                        | `""`                     |
| `podAnnotations`                             | Chart Pod annotations                                                                                     | `{}`                     |
| `podSecurityContext`                         | Enable Chart pod(s)' Security Context                                                                     | `{}`                     |
| `securityContext`                            | Define a securityContext                                                                                  | `{}`                     |
| `service.type`                               | Kubernetes Service type                                                                                   | `NodePort`               |
| `service.port`                               | Node app service port   	                                                                               | `80`                     |
| `ingress.enabled`                            | Enable ingress                                                                                            | `false`                  |
| `ingress.className`                          | Name of the ingress                                      					                               | `""`                     |
| `ingress.annotations`                        | Ingress annotations                                           										       | `{}`                     |
| `ingress.hosts.host`                         | Host name           														     				           | `chart.example.local`    |          
| `ingress.hosts.paths.path`                   | Host path                                                    						     				   | `/`                      |
| `ingress.hosts.paths.pathType`               | Host path type                                                        								       | `ImplementationSpecific` |
| `ingress.tls`                                | Secure ingress (443)                                                                                          | `[]`                     |
| `resources`                                  | CPU/memory resource requests/limits                                                                       | `{}`                     |
| `autoscaling.enabled`                        | Enable autoscaling                                                                                        | `false`                  |
| `autoscaling.minReplicas`                    | Minimum pod replicas                                                                                      | `1`                      |
| `autoscaling.maxReplicas`                    | Maximum pod replicas                                                                                      | `100`                    |
| `autoscaling.targetCPUUtilizationPercentage` | target CPU threshold to autoscale pod                                                                     | `80`                     |
| `nodeSelector`                               | Node labels for pod assignment                                                                            | `{}`                     |
| `tolerations`                                | Node tolerations for pod assignment                                                                       | `[]`                     |
| `affinity`                                   | Node affinity for pod assignment                                                                          | `{}`                     |


### MongoDB(&reg;) parameters

[mongodb paramters](https://github.com/bitnami/charts/blob/master/bitnami/mongodb)
