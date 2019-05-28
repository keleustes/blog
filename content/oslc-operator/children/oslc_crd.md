---
layout: post
title:  "Oslc CRD"
menuTitle:  "Oslc CRD"
weight: 25
date:   2019-05-15
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [wiki]
published: true
---


## LifeCycle Modelisation

### Design
--------------------

![](/images/oslc/openstackservice_lifecycle_oslc_crd.png)

### Oslc CRD
--------------------

The CRD Oslc definition is available here:

1. Its Spec which is update through kubectl: [Spec](https://github.com/keleustes/oslc-operator/blob/master/pkg/apis/openstacklcm/v1alpha1/oslc_types.go#L27)
2. Its Status which is updated by the operator and accessible through kubectl describe: [Status](https://github.com/keleustes/oslc-operator/blob/master/pkg/apis/openstacklcm/v1alpha1/common_types.go#L161)
3. Its definition made out of the two above components: [Definition](https://github.com/keleustes/oslc-operator/blob/master/pkg/apis/openstacklcm/v1alpha1/oslc_types.go#L109)
4. The yaml version of the CRD: [Yaml](https://github.com/keleustes/oslc-operator/blob/master/chart/templates/openstacklcm_v1alpha1_oslc.yaml)

### Oslc Controller
---------------------------

TBD

### SubResources
---------------------------

The current PhaseCRD are currently standalone CRDs. This provides control to the phase-controller on those objects.
At one point we will have to weight if we need to keep those CRDs or simply consider the Phase as nodes of an Argo Workflow. 
