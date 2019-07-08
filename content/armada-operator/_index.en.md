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

{{% notice warning %}}
This is not a "replacement" for airship armada. This POC merely aims to highlight the potential advantages and pitfalls in going in that direction.
{{% /notice %}}

## Lessons Learned

### Simular problems discussed by the community

The following links are trying to address similar problems

- [Mirantis AppController](https://github.com/Mirantis/k8s-AppController)
- [Facilitate API orchestration](https://github.com/kubernetes/kubernetes/issues/34363)

### CRD usages

- Schema validation: openAPIV3 schema validation is supported by `kubectl`. The schema can be generated
  out of the go code:
  - [generated schema](https://github.com/keleustes/armada-operator/blob/master/chart/templates/armada_v1alpha1_armadachart.yaml#L32)
  - [generation mechanism](https://github.com/keleustes/armada-operator/blob/master/Makefile#L46)
  - [go code](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/armadachart_types.go#L141)
- DeepCopy and structured types in golang: 
  - During the CRD definition, the system especially during deep-copy generation does not
    really support generic yaml object such as interface{}. The Values of the ArmadaChart that would leave untyped (interface{}) when
    using go had to be modified to use a well defined struct:
    [ArmadaChartValue](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/armadachart_types.go#L105).
    This increases the complexity very rapidely. 
  - We could not get a []byte construct to be used instead. 
  - Moreover, any struct not beeing well defined as in 
    [AVConf](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/armadachart_values_types.go#L147), 
    gives ability to the system to be more permissive but the corresponding data is not accessible in the struct return to the 
    [reconcile method](https://github.com/keleustes/armada-operator/blob/master/pkg/controller/armada/chart_controller.go#L120)
- Fundamentally, all the different constructs for the values.yaml of all the charts developped for airship and openstack-helm,
  are beeing funnel through the construct. Even the teams did an outstanding job of consolidation of those charts, outsiders
  are spotted causing very quickly issues and prevent a `kubectl apply -f xxx.yaml` to work.
- In the partical cases of the ArmadaChart, the feature overlapping with the work done by the helmv3 team:
  [schema validation](https://github.com/helm/helm/blob/dev-v3/pkg/chartutil/jsonschema.go#L58)

### Operator Usage

- Ownership of objects:
  - The armada-operator code was largely coming for the operator-fwk helm implemention,
    especially the [watch](https://github.com/operator-framework/operator-sdk/blob/master/pkg/helm/watches/watches.go#L90)
    and the way the owner is added to the top k8s objects deployed by tiller
    [owner](https://github.com/operator-framework/operator-sdk/blob/master/pkg/helm/engine/ownerref.go#L92)
  - The armada-operator can now decide what to do when an object owned by an ArmadaChart is deleted which helps
    for consistency. What to do if a user ran a 'kubectl edit' command in the back of armada, or if a stateful set created
    by an armada chart is beeing deleted. Should the object be recreated or the status of the armadachart set to "inconsistent".
- Kubernetes Event Handling:
  - One of the main arship-armada feature is to be able to detect when the resources deployed by an helm chart are
    available, timeout and potentially delete the release if something went wrong:
    [airship-armada](https://opendev.org/airship/armada/src/branch/master/armada/handlers/wait.py#L391)
  - Since the armada-operator is listening on all the object owned by an ArmadaChart, it was possible to emulate the
    feature:
    - An event detecting a change of state triggers a reconcile: [event](https://github.com/keleustes/armada-operator/blob/master/pkg/controller/armada/base_controller.go#L92)
    - When the resources deployed by the helm release, the ArmadaChart status goes from "running" to "ready/deployed": [ready](https://github.com/keleustes/armada-operator/blob/master/pkg/controller/armada/chart_controller.go#L448)
- RBAC Implication: Kubernetes RBAC and service accounts are used. Because the armada-operator oftens ends up
  running helm charts which are creating new service accounts, the rights provided to the armada-operator looks
  kind of extensive: [roles](https://github.com/keleustes/armada-operator/blob/master/chart/templates/role.yaml)
- Deployment of the operator itself: The operator is deployed in kubernetes itself. If using helm, we have some
  kind of [chicken-egg issue](https://github.com/keleustes/armada-operator/blob/master/Makefile#L87). 
  Otherwise the operator can be deployed using [simple kubectl](https://github.com/keleustes/treasuremap/blob/master/Makefile#L2)

### HelmV2 vs HelmV3

- Tiller dependency:
    - As for the event handling, the bulk of the behavior was provided by the operator-fwk: [helm](https://github.com/operator-framework/operator-sdk/blob/master/pkg/helm/release/manager_factory.go#L89) and then adapter in the armada-operator:
      [armada-operator](https://github.com/keleustes/armada-operator/blob/master/pkg/helmv2/manager_factory.go)
    - Tiller is using an [in-memory storage](https://github.com/keleustes/armada-operator/blob/master/pkg/helmv2/manager_factory.go#L45)
    - Tiller ReleaseServer construct is also local to the operator: 
      [local](https://github.com/helm/helm/blob/master/pkg/tiller/release_server.go#L93)
    - Once helmv3 client library is released, it will be possible to leverage instead of a local tiller release manager as for
      helm v2.
- Helm Golang code dependency: Using the go client code instead of the
  [helm execute](https://github.com/argoproj/argo-cd/blob/master/util/helm/helm.go#L206)
  brings use the power of using go code but also brings dependencies issues on the helm code structure.
  We had to account for the improvments and refactorexing done by the helm team:
    - [v2 tag](https://github.com/keleustes/armada-operator/blob/master/pkg/helmv2/chart_manager.go#L15)
    - [chart struct in helmv2](https://github.com/keleustes/armada-operator/blob/master/pkg/helmv2/chart_manager.go#L40)
    - [v3 tag](https://github.com/keleustes/armada-operator/blob/master/pkg/helmv3/chart_manager.go#L15)
    - [chart struct in helmv3](https://github.com/keleustes/armada-operator/blob/master/pkg/helmv3/chart_manager.go#L38)


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

## Build armada-operator

### Build

```bash
git clone -b kube15 https://github.com/keleustes/armada-operator.git
make
```

### Branches

- `master` supports kubernetes 1.14.x and helm 2.13.x
- `kube15` supports kubernetes 1.15.x and helm 2.14.x
- `helmv3` supports kubernetes 1.15.x and helm 3.0.x beta1

### Important Issues and Release Notes

#### kubernetes

- [CRD schema validation](https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/#specifying-a-structural-schema)

#### helm

- [Rendering Engine](https://github.com/helm/helm/issues/5826). Seems that the rendering engine can not be
  modified in helmV3. That ability of helmv2 is used to render the object and add an owner.


<!--more-->

