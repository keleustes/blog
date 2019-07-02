+++
title = "LifeCycle Manager"
description = "This is keleustes OpenstackService LifeCycle operator POC"
weight = 20
pre = "<b>4. </b>"
chapter = true
+++

# OpenstackLCM

## Rationale

- Create a Kubernetes Operator able to orchestrate draining traffic, upgrading,
  testing, traffic rollout...
- The main lesson learned from this POC is the ability to use the helm rendering
  to provide a unified way of delivering scripts onto a platform and at
  runtime selectively decide which part of the chart to render according to the
  state of the service which lifecycle may not match exactly the lifecycle of a
  helm chart (i.e install, upgrade, rollback, delete).

{{% notice note %}}
The Argo team published since an new subproject to argoproj called argo-rollout which seems really promising.
Currently rely on replacing the standard StatefulSet by an Argo Rollout deployement object
{{% /notice %}}


## Lessons Learned

### Multi facet charts

- TBD

### Traffic Draining

- TBD

### ScaleUp / ScaleDown

- TBD

## Documentation

- [Readme](https://github.com/keleustes/oslc-operator/blob/master/README.md)
- [Argo CD](https://github.com/argoproj/argo-cd)
- [Argo Rollout](https://github.com/argoproj/argo-rollouts)
- [WeaveWorks Flagger](https://github.com/weaveworks/flagger)

{{< youtube id="yeVkTTO9nOA" autoplay="false" >}}

## Associated GIT Repos

- [oslc-operator](https://github.com/keleustes/oslc-operator)

## Build oslc-operator

### Build

```bash
git clone -b kube15 https://github.com/keleustes/oslc-operator.git
make
```

### Branches

- `master` supports kubernetes 1.14.x and helm 2.13.x
- `kube15` supports kubernetes 1.15.x and helm 2.14.x

<!--more-->

{{%children style="h3" description="false" depth="1" sort="weight" %}}
