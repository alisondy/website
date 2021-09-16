---
title: "Deploy a Helm Chart using HelmRelease"
date: 2021-09-15T20:42:50+01:00
draft: true
---

## Before You Begin

To follow the guide, you will need a cluster with Flux boostrapped onto it. See Bootstrap Flux for instructions.

The Flux CLI

## Define a source

{{% tabs %}}
{{% tab GitRepository %}}

Use the ``flux create`` command to generate

```shell
flux create source git podinfo
...
--export > podinfo-source.yaml
```

output yaml should look like this yo

```yaml
a yaml file that defines a gitrepository source
```

{{% /tab %}}
{{% tab HelmRepository %}}

Use the ``flux create`` command to generate

```shell
flux create source helm podinfo \ 
--namespace=flux-system \
--interval=1m \
--url=https://stefanprodan.github.io/podinfo \ --export > podinfo-source.yaml
```

Output should look like this yo:

```yaml
apiVersion: source.toolkit.fluxcd.io/v1beta1
kind: HelmRepository
metadata:
  name: podinfo
  namespace: flux-system
spec:
  interval: 1m
  url: https://stefanprodan.github.io/podinfo
```
{{% /tab %}}
{{% tab BucketSource %}}
{{% caution %}}
When using `Bucket` as a source for a `HelmRelease`, the whole storage bucket will be downloaded by source controller at each sync. The
bucket can easily become very large if there are frequent releases of multiple charts
that are stored in the same bucket.
{{% /caution %}}

Use the ``flux create`` command to generate

```shell
flux create source bucket podinfo
...
--export > podinfo-source.yaml
```

output yaml should look like this yo

```yaml
a yaml file that defines a gitrepository source
```

{{% /tab %}}
{{% /tabs %}}

## Define a Helm Release

{{% tabs %}}
{{% tab GitRepository %}}

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
      chart: podinfo
      version: '4.0.x'
      sourceRef:
        kind: GitRepository
        name: podinfo
        namespace: flux-system
      interval: 1m
  values:
    replicaCount: 2
```

{{% /tab %}}
{{% tab HelmRepository %}}

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
      chart: podinfo
      version: '4.0.x'
      sourceRef:
        kind: HelmRepository
        name: podinfo
        namespace: flux-system
      interval: 1m
  values:
    replicaCount: 2
```

{{% /tab %}}
{{% tab BucketSource %}}
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
      chart: podinfo
      version: '4.0.x'
      sourceRef:
        kind: Bucket
        name: podinfo
        namespace: flux-system
      interval: 1m
  values:
    replicaCount: 2
```
{{% /tab %}}
{{% /tabs %}}

## Commit and push changes

```bash
git add podinfo-source.yaml
git add podinfo-helmrelease.yaml
git commit -m "Add podinfo Helm chart"
git push
```