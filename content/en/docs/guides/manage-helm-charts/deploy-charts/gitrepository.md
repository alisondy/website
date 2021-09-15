---
title: "Deploy using a GitRepository source"
date: 2021-09-15T20:42:39+01:00
draft: true
---

## Before You Begin

## Define a GitRepository source

## Define a Helm Release

## Commit and push changes

<!-- Original Documentation -->

### Git repository

Charts from Git repositories can be released by declaring a
`GitRepository`, the source-controller will fetch the contents of the
repository on an interval and expose it as an artifact.

The source-controller can build and expose Helm charts as artifacts
from the contents of the `GitRepository` artifact (more about this
later on in the guide).

**There is one caveat you should be aware of:** to make the
source-controller produce a new chart artifact, the `version` in the
`Chart.yaml` of the chart must be bumped.

An example `GitRepository`:

```yaml
apiVersion: source.toolkit.fluxcd.io/v1beta1
kind: GitRepository
metadata:
  name: podinfo
  namespace: flux-system
spec:
  interval: 1m
  url: https://github.com/stefanprodan/podinfo
  ref:
    branch: master
  ignore: |
    # exclude all
    /*
    # include charts directory
    !/charts/
```

The `interval` defines at which interval the Git repository contents
are fetched, and should be at least `1m`. Setting this to a higher
value means newer chart versions will be detected at a slower pace,
a push-based fetch can be introduced using [webhook receivers](webhook-receivers.md)

The `url` can be any HTTP/S or SSH address (the latter requiring
authentication).

The `ref` defines the checkout strategy, and is set to follow the
`master` branch in the above example. For other strategies like
tags or commits, see the [`GitRepository` CRD docs](../components/source/gitrepositories.md).

The `ignore` defines file and folder exclusion for the
artifact produced, and follows the [`.gitignore` pattern
format](https://git-scm.com/docs/gitignore#_pattern_format).
The above example only includes the `charts` directory of the
repository and omits all other files.

{{% alert color="info" title="Authentication" %}}
HTTP/S basic and SSH authentication can be configured for private
Git repositories. See the [`GitRepository` CRD docs](../components/source/gitrepositories.md)
for more details.
{{% /alert %}}
