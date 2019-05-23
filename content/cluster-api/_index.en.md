+++
title = "cluster-api"
description = "This is cluster-api POC page"
weight = 30
pre = "<b>5. </b>"
chapter = true
+++

# Cluster API

## Rationale

- This POC of a baremetal cluster-api provider was started before the official [cluster-api-provider-baremetal](https://github.com/metal3-io/cluster-api-provider-baremetal)
- This POC was relying on Airship Drydock/Maas. Thanks to the work done by the the metal3.io team, most of that this POC has become
  irrelevant.
- The remaining questions that can be kind of answered by this POC are:
  - Is DivingBell still relevant. Is the cluster-api in charge of updating, rebooting machines when the machine specs are updated.
  - How much of Promenade is still relevant. cluster-api indeed helping to save the kubeadm token into configmaps to help
    machine to join.
  - Can kustomize be used to build the cluster-api MachineList and Cluster CRDs from Airship Site definitions.

## Documentation

- TBD

## Associated GIT Repos

- [cluster-api](https://github.com/kubernetes-sigs/cluster-api)
- [cluster-api-provider-baremetal](https://github.com/metal3-io/cluster-api-provider-baremetal)
- [cluster-api-provider-airship](https://github.com/keleustes/cluster-api-provider-airship.git) 

<!--more-->

{{%children style="h3" description="false" depth="1" sort="weight" %}}
