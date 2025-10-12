# Kubernetes GitOps Repository

This repository contains the GitOps configuration for the homelab Kubernetes cluster using ArgoCD.

## Cluster Information

- **Kubernetes Version**: 1.31.13
- **CNI**: Cilium 1.16.3
- **VIP**: 10.128.1.20
- **Masters**: 10.128.1.21, 10.128.1.22, 10.128.1.23
- **Workers**: 10.128.1.31, 10.128.1.32, 10.128.1.33
- **Domain**: homelab.ftscode.de

## LoadBalancer IP Assignments

| Service | IP | Purpose |
|---------|-------|---------|
| nginx-test | 10.128.1.50 | Test application |
| ArgoCD | 10.128.1.51 | GitOps platform |
| Traefik | 10.128.1.52 | Ingress controller |
| Grafana | 10.128.1.53 | Monitoring dashboard |
| Longhorn UI | 10.128.1.54 | Storage management |
| Registry | 10.128.1.55 | Container registry |
| Minio | 10.128.1.56 | S3 storage |

## Repository Structure