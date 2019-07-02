+++
title = "Kustomize"
description = "This is the keleustes kustomize POC page"
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

{{% notice warning %}}
This is not a "replacement" for airship deckhand. This POC merely aims to highlight the potential advantages and pitfalls in going in that direction.
{{% /notice %}}

## Lessons Learned

### Layering

- It is possible to support the current airship layering (global, type, site). The three subfolders have be created.
  Each kustomization.yaml is using an entry "base". Check [airsloop](https://github.com/keleustes/airship-treasuremap/blob/master/site/airsloop/kustomization.yaml#L5)

### Substitutions

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

## Remaining issues

- [Extract from](https://blog.argoproj.io/the-state-of-kubernetes-configuration-management-d8b06c1205)

{{% notice warning %}}
The Bad:
No parameters & templates. The same property that makes kustomize applications so readable, can also make it very limiting. For example, I was recently trying to get the kustomize CLI to set an image tag for a custom resource instead of a Deployment, but was unable to. Kustomize does have a concept of “vars,” which look a lot like parameters, but somehow aren’t, and can only be used in Kustomize’s sanctioned whitelist of field paths. I feel like this is one of those times when the solution, despite making the hard things easy, ends up making the easy things hard.
{{% /notice %}}

## Documentation

- [ReadTheDocs](https://airshipit.readthedocs.io/projects/deckhand/en/latest/)
- [Readme](https://github.com/keleustes/kustomize/blob/master/README.md)

## Associated GIT Repos

- [kustomize](https://github.com/keleustes/kustomize)
- [airship-deckhand](https://github.com/airshipit/deckhand)

## Build kustomize

### Build

```bash
git clone -b allinone https://github.com/keleustes/kustomize.git
GO111MODULE=on go build -o $HOME/bin/kustomize cmd/kustomize/main.go
```

### Branches

- `master` is aligned with upstream/master
- `inline` contains the enhanced inlining, for instance tree inlining and parent-inline
- `autov` contains the automatic variable declaration
- `diamond` contains the ability to have diamond import of the base folder.
  Important for the tree reorganization
- `slicecase` contains small bug fix.
- `allinone` is built out of all the above branches.

<!--more-->

{{%children style="h3" description="false" depth="1" sort="weight" %}}
