+++
title = "Armada"
description = "This is the keleustes armada-operator POC page"
weight = 10
pre = "<b>2. </b>"
chapter = true
+++

# Armada

## Rationale

- Investigate the feasibility of converting airship-armada functions 
  into a Kubernetes operator pattern.
- This is not a "replacement" for airship armada. This POC merely aims
  at highlighting the potential advantages and pitfall in going in that
  direction.

## Lessons Learned

### CRD usages

- Schema validation: TBD
- DeepCopy and structured types in golang: TBD

### Operator Usage

- Kubernetes Event Handling: TBD
- RBAC Implication: TBD
- Deployment of the operator itself: TBD

### HelmV2 vs HelmV3

- Tiller dependency: TBD
- Helm Golang code dependency: TBD

### Multithreading and Concurrency

- One Armada Operator per namespace: TBD

### Underlying resource state management

One of the key feature of armada is to be able to figure if the resources
deployed through `helm install` or `helm upgrade` are ready to be used.

## Documentation

- [ReadTheDocs](https://airshipit.readthedocs.io/projects/armada/en/latest/)
- [Readme](https://github.com/keleustes/armada-operator/blob/master/README.md)

## Associated GIT Repos

- [armada-operator](https://github.com/keleustes/armada-operator)
- [airship-armada](https://github.com/airshipit/armada)

<!--more-->

{{%children style="h3" description="false" depth="1" sort="weight" %}}
