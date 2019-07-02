+++
title = "TreasureMap"
description = "This is the keleustes treasuremap POC page"
weight = 15
pre = "<b>3. </b>"
chapter = true
+++

# TreasureMap

## Rationale

- Investigate the feasibility of converting airship-treasuremap site descriptions
  into kustomize site descriptions (Kubernetes CRD based).
- The kustomize layering are beeing leverage (global, type, site).

{{% notice warning %}}
This is not a "replacement" for airship treasuremap. This POC merely aims at highlighting what would have to be done to adapt treasuremap to tools such as kustomize, argo...
{{% /notice %}}

## Lessons Learned

### Data Layering, Substitions and Validation

- It is possible to support the current airship layering (global, type, site). The three subfolders have be created.
  Each kustomization.yaml is using an entry "base". Check [airsloop](https://github.com/keleustes/airship-treasuremap/blob/master/site/airsloop/kustomization.yaml#L5)

- kustomize supports variables by default
  - Regex is using $(xxx) format.
  - Improvments have been proposed to address what kustomize could not do by default: [PR](https://github.com/kubernetes-sigs/kustomize/pull/1111)

- simple variable: 
  - Definition in the kustomization.yaml: [global](https://github.com/keleustes/airship-treasuremap/blob/master/global/kustomization.yaml#L1085)
  - Tree and structure can be inlined: [inline](https://github.com/keleustes/airship-treasuremap/blob/master/global/software/charts/ucp/drydock/maas.yaml#L48)
  - Variable value extracted from a catalog CRD: [value](https://github.com/keleustes/airship-treasuremap/blob/master/site/airsloop/networks/common-addresses.yaml#L12)

- simple inlining:
  - Definition in the kustomization.yaml: [global](https://github.com/keleustes/airship-treasuremap/blob/master/global/kustomization.yaml#L2553)
  - Tree and structure can be inlined: [inline](https://github.com/keleustes/airship-treasuremap/blob/master/global/software/charts/osh/openstack-glance/glance.yaml#L20)
  - Variable value extracted from a catalog CRD: [value](https://github.com/keleustes/airship-treasuremap/blob/master/global/software/config/versions.yaml#L127)

- parent inlining (for multipass replacement) are currently used the following way:
  - Definition in the kustomization.yaml: [global](https://github.com/keleustes/airship-treasuremap/blob/master/global/kustomization.yaml#L2089)
  - Tree and structure can be inlined: [inline](https://github.com/keleustes/airship-treasuremap/blob/master/global/software/charts/osh/openstack-glance/glance.yaml#L130)
  - Variable value extracted from a catalog CRD: [value](https://github.com/keleustes/airship-treasuremap/blob/master/type/sloop/config/endpoints.yaml#L675)

- Some of the OpenAPI V3 construct are not supported yet by CRDs.
  - AdditionalProperties are allowed in specific conditions, check [additionalProperties](https://github.com/keleustes/airship-treasuremap/blob/master/deploy/crds/DrydockHostProfile.yaml#L141)
  - Definitions and Refs are not supported: [definitions](https://github.com/keleustes/airship-treasuremap/blob/master/deploy/crds/PromenadeGenesis.yaml#L36)
  - AnyOf construct [anyOf](https://github.com/keleustes/airship-treasuremap/blob/master/deploy/crds/PromenadeKubernetesNetwork.yaml#L156)

### Operator experience

- `kubectl get act --all--namespaces` provides the user with a view at a glance of his deployment.
- TBD

## Documentation

- [ReadTheDocs](https://airshipit.readthedocs.io/projects/treasuremap/en/latest/)
- [Readme](https://github.com/keleustes/airship-treasuremap/blob/master/README.md)

## Associated GIT Repos

- [airship-treasuremap](https://github.com/keleustes/airship-treasuremap)
- [airship-treasuremap](https://github.com/airshipit/treasuremap)

## Test airsloop site rendering

### Build

Check that your configuration is correct. Invokes kustomize build and compare the output with
a previously generated output. Be sure to have build the `allinone` version of kustomize.

```bash
make rendering-test-airsloop
```

### Deploy the CRDs without operators

```bash
make deploy-airsloop
kubectl get all act --all-namespaces
```

### Branches

- `master` site manifests which require the inline function but autovar feature is not used.
- `autovar` autovar feature of kustomize is enabled, hence no need for 3000 lines of vars and varreferences:

### Important Issues and Release Notes

#### kubernetes

The definition of the CRD will soon be using v1 instead of v1beta1. The schema will be mandatory and the handling of the unknown field will change.

- [CRD schema validation](https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/#specifying-a-structural-schema)
- [Pruning Unknown Field](https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/#pruning-versus-preserving-unknown-fields)

<!--more-->

{{%children style="h3" description="false" depth="1" sort="weight" %}}
