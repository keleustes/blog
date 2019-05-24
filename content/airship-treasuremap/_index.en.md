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
- This is not a "replacement" for airship treasuremap. This POC merely aims
  at highlighting what would have to be done to adapt treasuremap to tools such
  as kustomize, argo...

## Lessons Learned

### Layering

- TBD

### Substitutions

- TBD

### Schema Validation

- TBD

## Documentation

- [ReadTheDocs](https://airshipit.readthedocs.io/projects/treasuremap/en/latest/)
- [Readme](https://github.com/keleustes/airship-treasuremap/blob/master/README.md)

## Associated GIT Repos

- [airship-treasuremap](https://github.com/keleustes/airship-treasuremap)
- [airship-treasuremap](https://github.com/airshipit/treasuremap)

<!--more-->

{{%children style="h3" description="false" depth="1" sort="weight" %}}
