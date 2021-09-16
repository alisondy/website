---
title: "Chartmuseum as a backend for Bucket source"
date: 2021-09-15T20:42:59+01:00
draft: true
---

<!-- Original Documentation -->

### Cloud Storage


A better option is to use [Chartmuseum](https://github.com/helm/chartmuseum) and run a cluster
local Helm repository that can be used by source controller. Chartmuseum has support
for multiple different cloud storage solutions such as S3, GCS, and Azure Blob Storage,
meaning that you are not limited to only using storage providers that support the S3 protocol.

You can deploy a Chartmuseum instance with a `HelmRelease` that exposes a Helm repository stored
in a S3 bucket. Please refer to [Chartmuseums how to run documentation](https://chartmuseum.com/docs/#how-to-run)
for details about how to use other storage backends.

```yaml
apiVersion: source.toolkit.fluxcd.io/v1beta1
kind: HelmRepository
metadata:
  name: chartmuseum
  namespace: flux-system
spec:
  url: https://chartmuseum.github.io/charts
  interval: 10m
---
apiVersion: helm.toolkit.fluxcd.io/v2beta1
kind: HelmRelease
metadata:
  name: chartmuseum
  namespace: flux-system
spec:
  interval: 5m
  chart:
    spec:
      chart: chartmuseum
      version: "2.14.2"
      sourceRef:
        kind: HelmRepository
        name: chartmuseum
        namespace: flux-system
      interval: 1m
  values:
    env:
      open:
        AWS_SDK_LOAD_CONFIG: true
        STORAGE: amazon
        STORAGE_AMAZON_BUCKET: "bucket-name"
        STORAGE_AMAZON_PREFIX: ""
        STORAGE_AMAZON_REGION: "region-name"
    serviceAccount:
      create: true
      annotations:
        eks.amazonaws.com/role-arn: "role-arn"
    securityContext:
      enabled: true
      fsGroup: 65534
```

After Chartmuseum is up and running it should be possible to use the accompanying
service as the url for the `HelmRepository`.

```yaml
apiVersion: source.toolkit.fluxcd.io/v1beta1
kind: HelmRepository
metadata:
  name: helm-charts
  namespace: flux-system
spec:
  interval: 1m
  url: http://chartmuseum-chartmuseum:8080
```

## Define a Helm release

With the chart source created, define a new `HelmRelease` to release
the Helm chart:

```yaml
apiVersion: helm.toolkit.fluxcd.io/v2beta1
kind: HelmRelease
metadata:
  name: podinfo
  namespace: default
spec:
  interval: 5m
  chart:
    spec:
      chart: <name|path>
      version: '4.0.x'
      sourceRef:
        kind: <HelmRepository|GitRepository|Bucket>
        name: podinfo
        namespace: flux-system
      interval: 1m
  values:
    replicaCount: 2
```

The `chart.spec` values are used by the helm-controller as a template
to create a new `HelmChart` resource in the same namespace as the
`sourceRef`. The source-controller will then lookup the chart in the
artifact of the referenced source, and either fetch the chart for a
`HelmRepository`, or build it from a `GitRepository` or `Bucket`.
It will then make it available as a `HelmChart` artifact to be used by
the helm-controller.

The `chart.spec.chart` can either contain:

* The name of the chart as made available by the `HelmRepository`
  (without any aliases), for example: `podinfo`
* The relative path the chart can be found at in the `GitRepository`
  or `Bucket`, for example: `./charts/podinfo`
* The relative path the chart package can be found at in the
  `GitRepository` or `Bucket`, for example: `./charts/podinfo-1.2.3.tgz`

The `chart.spec.version` can be a fixed semver, or any semver range
(i.e. `>=4.0.0 <5.0.0`). It is only taken into account for `HelmRelease`
resources that reference a `HelmRepository` source.

{{% alert color="info" title="Advanced configuration" %}}
The `HelmRelease` offers an extensive set of configurable flags
for finer grain control over how Helm actions are performed.
See the [`HelmRelease` CRD docs](../components/helm/helmreleases.md)
for more details.
{{% /alert %}}
