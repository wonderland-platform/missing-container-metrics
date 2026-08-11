# Missing Container Metrics - metrics cadvisor won't give you

This chart will install a daemon set that will expose container metrics such as `container_ooms` that are not available otherwise.

## Introduction
For motivation and implementation details please refer to [blog post](https://www.netice9.com/blog/guide-to-oomkill-alerting-in-kubernetes-clusters/) introducing the `missing-container-metrics`

## TL;DR;

```bash
$ helm install missing-container-metrics oci://ghcr.io/wonderland-platform/helm/missing-container-metrics
```

## Chart location

The chart is published as an OCI artifact to the GitHub Container Registry at
`oci://ghcr.io/wonderland-platform/helm/missing-container-metrics`. There is no classic Helm
repository to add — Helm 3.8 and newer can install from the OCI reference directly.

To inspect the available versions:
```bash
$ helm show chart oci://ghcr.io/wonderland-platform/helm/missing-container-metrics
```

## Installing the Chart
```bash
$ kubectl create namespace missing-container-metrics
$ helm install my-release-name oci://ghcr.io/wonderland-platform/helm/missing-container-metrics \
    -n missing-container-metrics
```

To pin a specific chart version, add `--version <chart-version>`.

## Configuration

| Parameter                                             | Description                                                       | Default                                                           |
|-------------------------------------------------------|-------------------------------------------------------------------|-------------------------------------------------------------------|
| image.repository                                      | missing-container-metrics image name                              | `ghcr.io/wonderland-platform/missing-container-metrics`           |
| image.pullPolicy                                      | pull policy for the image                                         | `IfNotPresent`                                                    |
| image.tag                                             | tag of the missing-container-metrics image                        | chart `appVersion`                                                |
| imagePullSecrets                                      | pull secrets for the image                                        | `[]`                                                              |
| nameOverride                                          | Override the generated chart name. Defaults to .Chart.Name.       |                                                                   |
| fullnameOverride                                      | Override the generated release name. Defaults to .Release.Name.   |                                                                   |
| podAnnotations                                        | Annotations for the started pods                                  | `{"prometheus.io/scrape": "true", "prometheus.io/port": "3001"}`  |
| podLabels                                             | Labels for the started pods                                       | `{}`                                                              |
| podSecurityContext                                    | Set the security context for the pods                             |                                                                   |
| priorityClassName                                     | Name of the existing priority class to be used by  pod(s)         | `""`                                                              |
| securityContext                                       | Set the security context for the container in the pods            |                                                                   |
| resources                                             | CPU/memory resource requests/limits                               | `{}`                                                              |
| tolerations                                           | Tolerations used for pod scheduling                               | 
| useDocker                                             | If true, container info is obtained from Docker                   | `false`                                                           |
| useContainerd                                         | If true, container info is obtained from Containerd               | `true`                                                            |
