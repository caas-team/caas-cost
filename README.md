# CaaS Cost

This repository includes a Helm Chart that is combining two dependency charts (see `Chart.yaml`) and custom resources (see `templates/prometheus`) to deploy the new CaaS cost stack.

## Components

[Opencost](https://www.opencost.io/) and the [kube-prometheus-stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack) are the two main components.

Opencost is the calculating part for all the cost of kubernetes workload in the CaaS clusters. A Prometheus instance is needed to provide a database to store Opencost data.

Additionally some resources are required to enable network communication and RBAC for the prometheus.

The prometheus has a dependency to a defined cluster monitoring stack. The prometheus is scraping needed metrics from the cluster prometheus (federation).

## Installation via Helm

```bash
helm dependency build
helm -n mynamespace upgrade -i caas-cost -f values.yaml .
```

remote install:

```bash
helm -n mynamespace upgrade -i caas-cost -f values.yaml --skip-crds --repo oci://ghcr.io/caas-team/charts/caas-cost --version 0.1.0
```
