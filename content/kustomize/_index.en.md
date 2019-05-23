+++
title = "Kustomize"
description = "This is the kustomize blueprint page"
weight = 5
pre = "<b>1. </b>"
chapter = true
+++

# Kustomize

## Rationale

- Investigate the feasibility of converting deckhand functions to kustomize.
  For that purpose improvments have been made and proposed to the kustomize community.
- CRD have been created and added to the underlying Kubernetes Cluster.
  Note that using CRDs does not force the Airship architecture to migrate to operator
  architecture immediatly.
- Some efforts has been spent into getting the OpenAPIV3Schema in the deploy/crds/xxx.yaml
  to be as accurate as possible. This helps getting kubectl version syntax verification.
  Still the real syntax check will be performed into helmv3 since it verifies the syntax
  of the values obtained from layering the "override" values on top of the "default" values
  provided in the chart.

## Documentation

- [ReadTheDocs](https://airshipit.readthedocs.io/projects/deckhand/en/latest/)
- [Readme](https://github.com/keleustes/kustomize/blob/master/README.md)

## Associated GIT Repos

- [kustomize](https://github.com/keleustes/kustomize)
- [airship-deckhand](https://github.com/airshipit/deckhand)


<!--more-->

{{%children style="h3" description="false" depth="1" sort="weight" %}}
