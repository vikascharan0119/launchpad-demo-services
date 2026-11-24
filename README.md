# Launchpad demo services

Small sample services that run on the
[Launchpad platform](https://github.com/vikascharan0119/launchpad-idp). They exist to
give the platform something realistic to deploy, measure and break.

**Status: skeleton only. No service code yet.**

| Service | What it does |
|---|---|
| `orders-api` | Accepts and lists orders, stores them in Postgres, calls `payments-stub` |
| `payments-stub` | Pretends to authorise a payment; can be told to be slow or to fail |
| `loadgen` | Sends steady traffic to `orders-api` |

All three are Python (FastAPI). This is generic sample code written for this
project.

## How a change reaches the cluster

1. A pull request merges here.
2. CI tests the code, builds the image, scans it and pushes it.
3. CI opens a pull request in `launchpad-idp` that bumps the image version.
4. When that merges, ArgoCD starts a canary release.

This pipeline never touches the cluster directly.
