# Case Study — OPIP GitOps Delivery Architecture

## Executive summary

This repository documents the GitOps delivery side of the OPIP platform.

It demonstrates a desired-state model where Git is the source of truth and Argo CD, rather than a CI pipeline running direct kubectl commands, is responsible for Kubernetes reconciliation.

## Delivery model

The intended delivery chain is:

application repository -> CI/security controls -> image registry -> signed/attested artifact -> GitOps repository -> Argo CD -> Kubernetes.

## Implemented repository controls

The repository includes:

- reusable Kubernetes base manifests;
- development and production overlays;
- Argo CD application definitions;
- non-root container security settings;
- dropped Linux capabilities;
- disabled privilege escalation;
- runtime-default seccomp;
- readiness/liveness probes;
- CPU and memory requests/limits;
- externalized secret references.

## Security architecture

Secrets are intentionally not stored in Git.

The recommended pattern is:

HashiCorp Vault -> External Secrets Operator -> Kubernetes Secret -> workload.

Image promotion is intended to use immutable digests rather than mutable tags.

## Business value

This pattern supports:

- auditable deployment state;
- controlled production changes;
- separation of CI and cluster reconciliation;
- environment consistency;
- reduced manual cluster mutation;
- platform security guardrails.

## Consulting outcome

A client engagement could include:

- GitOps readiness assessment;
- Argo CD deployment;
- repository structure;
- environment overlays;
- secure image promotion;
- secrets architecture;
- Kubernetes policy standards;
- production delivery governance.

## Evidence

See the main [README](./README.md) and repository manifests.

## Engagement fit

Relevant for:

- Kubernetes platform engineering;
- GitOps adoption;
- Argo CD;
- DevSecOps;
- delivery governance;
- secrets-management architecture.

**Consulting inquiries:** advisory@cloudgenius.ca
