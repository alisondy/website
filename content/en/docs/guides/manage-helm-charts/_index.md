---
title: "Manage Helm Charts"
date: 2021-09-15T20:40:32+01:00
draft: true
---

The [helm-controller](../components/helm/_index.md) allows you to
declaratively manage Helm chart releases with Kubernetes manifests.
It makes use of the artifacts produced by the
[source-controller](../components/source/_index.md) from
`HelmRepository`, `GitRepository`, `Bucket` and `HelmChart` resources.
The helm-controller is part of the default toolkit installation.
