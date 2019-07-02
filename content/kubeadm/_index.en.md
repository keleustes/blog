+++
title = "Kubeadm"
description = "This is the kubeadm POC page"
weight = 35 
pre = "<b>6. </b>"
chapter = true
+++

# Kubeadm

## Rationale

- Investigate the feasibility of converting promenade functions to kubeadm.
  For that purpose improvments have been made and proposed to the kubeadm community.

{{% notice warning %}}
This is not a "replacement" for airship promenade. This POC merely aims to highlight the potential advantages and pitfalls in going in that direction.
{{% /notice %}}


## Lessons Learned

### Kubernetes High Availibity

- TBD

### Certificates Management

Promenade is currently in charge of deploying certificates. The teams implementating the cluster-api have different approaches:

- [Azure Cluster API implementation](https://github.com/kubernetes-sigs/cluster-api-provider-azure/blob/master/pkg/cloud/azure/services/config/startupscript.go#L70)

### Kubernetes Software Upgrade

Promenade is installing a set of packages:

- [Azure Package Installation](https://github.com/kubernetes-sigs/cluster-api-provider-azure/blob/master/pkg/cloud/azure/services/config/controlplane.go#L117)

### kubelet, kubeadm and kubectl upgrades

- [AWS Cluster API](https://github.com/kubernetes-sigs/cluster-api-provider-aws/blob/master/pkg/cloud/aws/services/ec2/instances.go#L201)

## Documentation

- [ReadTheDocs](https://airshipit.readthedocs.io/projects/promenade/en/latest/)
- [Readme](https://github.com/keleustes/kubeadm/blob/master/README.md)

## Associated GIT Repos

- [kubeadm](https://github.com/keleustes/kubeadm)
- [airship-promenade](https://github.com/airshipit/promenade)

<!--more-->

{{%children style="h3" description="false" depth="1" sort="weight" %}}
