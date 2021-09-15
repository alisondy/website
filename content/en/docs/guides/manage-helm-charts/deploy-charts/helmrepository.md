---
title: "Deploy using a HelmRepository source"
date: 2021-09-15T20:42:25+01:00
draft: true
---

## Before You Begin

## Define a HelmRepository source

## Define a Helm Release

## Commit and push changes

<!-- Original Documentation -->

### Helm repository

Helm repositories are the recommended source to retrieve Helm charts
from, as they are lightweight in processing and make it possible to
configure a semantic version selector for the chart version that should
be released.

They can be declared by creating a `HelmRepository` resource, the
source-controller will fetch the Helm repository index for this
resource on an interval and expose it as an artifact:

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

The `interval` defines at which interval the Helm repository index
is fetched, and should be at least `1m`. Setting this to a higher
value means newer chart versions will be detected at a slower pace,
a push-based fetch can be introduced using [webhook receivers](webhook-receivers.md)

The `url` can be any HTTP/S Helm repository URL.

{{% alert color="info" title="Authentication" %}}
HTTP/S basic and TLS authentication can be configured for private
Helm repositories. See the [`HelmRepository` CRD docs](../components/source/helmrepositories.md)
for more details.
{{% /alert %}}
