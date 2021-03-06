---
layout: post
title:  "Ideas"
menuTitle:  "Ideas"
weight: 20
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

### Ideas

1. Can we use the "finalizer" to implement the "protected" feature of ArmadaChart.
2. We need a consistent handling of Conditions, Events and Status and behavior which are easily understood by people understanding K8s.
3. "kubectl get act" should be able to return a synthetic view as good as the "kubectl get pod" does.
4. The Status object should be accurate enough for the DAG in the Argo Workflow to stay simple.

### Questions

1. Should the deletion of ArmadaChartGroup trigger deletion of ArmadaChart
2. How to deal with the "prefix" feature of the "ArmadaManifest".
3. Do we still need the ArmadaManifest
4. Should we add a "workflows" field in the ArmadaManifest.
5. Armada would not be using keystone anymore but Kubernetes RBAC. What are the impacts ?
6. History of ArmadaChart can be implemented two ways: 

   a. Reuse K8s ControllerRevision code.
   b. Reuse Helm storage Driver.
