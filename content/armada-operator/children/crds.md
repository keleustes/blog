---
layout: post
title:  "CRDs"
menuTitle:  "CRDs"
weight: 5
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


## CRDs

### ArmadaChart CRD

The ArmadaChart defintion used in production is available here: [Production](https://github.com/openstack/airship-armada/blob/master/armada/schemas/armada-chart-schema.yaml)

The CRD ArmadaChart definition is available here:

1. Its Spec which is update through kubectl: [Spec](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/armadachart_types.go#L27)
2. Its Status which is updated by the operator and accessible through kubectl describe: [Status](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/common_types.go#L161)
3. Its definition made out of the two above components: [Definition](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/armadachart_types.go#L109)
4. The yaml version of the CRD: [Yaml](https://github.com/keleustes/armada-operator/blob/master/chart/templates/armada_v1alpha1_armadachart.yaml)

### ArmadaChartGroup CRD

The ArmadaChartGroup defintion used in production is available here: [Production](https://github.com/openstack/airship-armada/blob/master/armada/schemas/armada-chart-schema.yaml)

The CRD ArmadaChartGroup definition is available here:

1. Its Spec which is update through kubectl: [Spec](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/armadachart_types.go#L27)
2. Its Status which is updated by the operator and accessible through kubectl describe: [Status](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/common_types.go#L161)
3. Its definition made out of the two above components: [Definition](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/armadachart_types.go#L109)
4. The yaml version of the CRD: [Yaml](https://github.com/keleustes/armada-operator/blob/master/chart/templates/armada_v1alpha1_armadachart.yaml)

### ArmadaManifest CRD

The ArmadaManifest defintion used in production is available here: [Production](https://github.com/openstack/airship-armada/blob/master/armada/schemas/armada-chart-schema.yaml)

The CRD ArmadaManifest definition is available here:

1. Its Spec which is update through kubectl: [Spec](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/armadachart_types.go#L27)
2. Its Status which is updated by the operator and accessible through kubectl describe: [Status](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/common_types.go#L161)
3. Its definition made out of the two above components: [Definition](https://github.com/keleustes/armada-operator/blob/master/pkg/apis/armada/v1alpha1/armadachart_types.go#L109)
4. The yaml version of the CRD: [Yaml](https://github.com/keleustes/armada-operator/blob/master/chart/templates/armada_v1alpha1_armadachart.yaml)

### Usage

1. The file passed to the 'armada cli` is available here: [Armada](https://github.com/openstack/airship-armada/blob/master/examples/simple.yaml)
2. The file passed to the kubectl apply is available here: [kubectl](https://github.com/keleustes/armada-operator/blob/master/examples/armada/simple.yaml)
