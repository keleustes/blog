+++
title = "OpenstackLCM"
description = "This is openstacklcm-operator blueprint page"
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

## Documentation

- [Readme](https://github.com/keleustes/oslc-operator/blob/master/README.md)

## Associated GIT Repos

- [oslc-operator](https://github.com/keleustes/oslc-operator)

<!--more-->

{{%children style="h3" description="false" depth="1" sort="weight" %}}
