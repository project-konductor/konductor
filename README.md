# Konductor

Konductor is an unofficial distribution of [Netflix Conductor](https://github.com/Netflix/conductor) that allows installation on Kubernetes using Helm.

Conductor is a platform created by Netflix to orchestrate workflows that span across microservices.

Currently Conductor is distributed using docker-compose which is not necessarily suitable for production environments. In addition, there are no current docker images available for download so each user has to build the code themselves.

The goal of the project is to establish a stable distribution of Conductor that can be easily installed as a Helm Chart. Once the goal is achieved, we hope that the project will be integrated as part of the official Conductor repository and become an official distribution.

# Goals

The ultimate goal of the project is to integrate as an official distribution of Conductor, for this purpose the project is divided into 3 phases:

## Phase 1

- [ ] Distribute unofficial ready-to-use Docker Images of Conductor ([fork](https://github.com/project-konductor/conductor))
- [ ] Creating a basic Helm Chart that allows a simple installation with Elasticsearch, Redis and PostgreSQL

## Phase 2

- [ ] Distribute unofficial ready-to-use Docker Images of [Dynomite](https://github.com/Netflix/Dynomite)
- [ ] Creating a Helm Chart for Dynomite (may not be scalable at this point)
- [ ] Added support for using Dynomite in Conductor Helm Chart

## Phase 3

- [ ] Opening a PR for Dynomite to merge the Docker Images and Helm Chart as part of the official repository
- [ ] Opening a PR for Conductor to merge the Docker Images and Helm Chart as part of the official repository
- [ ] Release an official version of all Images and Helm Charts

Once the project is finished, this repository can be archived and users will be able to use the official distributions that will be available. Until then we will try to provide everything needed here in the unofficial distribution.

# Install

tl;dr:

```console
helm repo add konductor https://project-konductor.github.io/konductor/
helm install konductor konductor/konductor
```

## Values

| Parameter | Description | Default |
|-----------|-------------|---------|
| nameOverride | Helm application name override | - |
| fullnameOverride | Helm application full name override | - |
| server.replicaCount | Amount of server containers to spin up | `1` |
| server.image.repository | The image repository for the server image | `quay.io/konductor/conductor` |
| server.image.tag | The image tag for the server image. The default is the chart appVersion | - |
| server.image.pullPolicy | Server image pull policy | `IfNotPresent` |
| server.imagePullSecrets | The image pull secrets for the server image | `[]` |
| server.properties | Extra properties for server's config.properties file | - |
| server.service.type | Server service type | `ClusterIP` |
| server.service.port | Server service port | `80` |
| server.ingress.enabled | Whether to create Ingress resource for the server | `false` |
| server.ingress.className | The server Ingress class name | - |
| server.ingress.annotations | The server Ingress annotations | `{}` |
| server.ingress.hosts | The server Ingress hosts | `[]` |
| server.ingress.tls | The server Ingress TLS | `[]` |
| server.resources | Resource requests and limitations for the server pods | `{}` |
| server.nodeSelector | Node selector for the server pods | `{}` |
| server.tolerations | Tolerations for the server pods | `[]` |
| server.affinity | Affinities and anti-affinities for the server pods | `{}` |
| ui.replicaCount | Amount of UI containers to spin up | `1` |
| ui.image.repository | The image repository for the UI image | `quay.io/konductor/conductor-ui` |
| ui.image.tag | The image tag for the UI image. The default is the chart appVersion | - |
| ui.image.pullPolicy | UI image pull policy | `IfNotPresent` |
| ui.imagePullSecrets | The image pull secrets for the UI image | `[]` |
| ui.service.type | UI service type | `ClusterIP` |
| ui.service.port | UI service port | `80` |
| ui.ingress.enabled | Whether to create Ingress resource for the UI | `false` |
| ui.ingress.className | The UI Ingress class name | - |
| ui.ingress.annotations | The UI Ingress annotations | `{}` |
| ui.ingress.hosts | The UI Ingress hosts | `[]` |
| ui.ingress.tls | The UI Ingress TLS | `[]` |
| ui.resources | Resource requests and limitations for the UI pods | `{}` |
| ui.nodeSelector | Node selector for the UI pods | `{}` |
| ui.tolerations | Tolerations for the UI pods | `[]` |
| ui.affinity | Affinities and anti-affinities for the UI pods | `{}` |
| serviceAccount.create | Whether to create ServiceAccount for conductor pods | `true` |
| serviceAccount.annotations | Annotations for the created ServiceAccount | `{}` |
| serviceAccount.name | Specify a name for the ServiceAccount. Default to the charts fullname | - |
| podAnnotations | Annotations to add to all conductor pods | `{}` |
| podSecurityContext | Pod security context for the conductor pods | `{}` |
| securityContext | Security context for the conductor pods | `{}` |
| elasticsearch.enabled | Install elasticsearch as a chart dependency | `true` |
| redis.enabled | Install Redis as a chart dependency | `true` |
| postgresql.enabled | Install PostgreSQL as a chart dependency | `true` |

- Additional `elasticsearch.*` values can be found here: https://artifacthub.io/packages/helm/elastic/elasticsearch/7.17.3#configuration
- Additional `redis.*` values can be found here: https://artifacthub.io/packages/helm/bitnami/redis/16.13.2#parameters
- Additional `postgresql.*` values can be found here: https://artifacthub.io/packages/helm/bitnami/postgresql/12.2.3#parameters

# License

Licensed under the Apache License, Version 2.0: http://www.apache.org/licenses/LICENSE-2.0
