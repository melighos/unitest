## Prerequisites

- Kubernetes 1.16+
- Helm 3+

## Description

Test chart for deploying prometheus with two dependencies: blackbox-exporter and grafana.
Blackbox-exporter configured to probe google.com by default.
Grafana configured with Blackbox exporter dashboard by default.

## Install Helm Chart

```console
helm install [RELEASE_NAME] -n unitest --create-namespace ./kube-prometheus-grafana-blackbox/
```
_See [helm install](https://helm.sh/docs/helm/helm_install/) for command documentation._

## Dependencies

By default this chart installs additional, dependent charts:

- [prometheus-community/prometheus-blackbox-exporter](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-blackbox-exporter)
- [grafana/grafana](https://github.com/grafana/helm-charts/tree/main/charts/grafana)

## Uninstall Helm Chart

```console
helm uninstall -n unitest [RELEASE_NAME]
```

This removes all the Kubernetes components associated with the chart and deletes the release.

_See [helm uninstall](https://helm.sh/docs/helm/helm_uninstall/) for command documentation._

CRDs created by this chart are not removed by default and should be manually cleaned up:

```console
kubectl delete crd alertmanagerconfigs.monitoring.coreos.com
kubectl delete crd alertmanagers.monitoring.coreos.com
kubectl delete crd podmonitors.monitoring.coreos.com
kubectl delete crd probes.monitoring.coreos.com
kubectl delete crd prometheuses.monitoring.coreos.com
kubectl delete crd prometheusrules.monitoring.coreos.com
kubectl delete crd servicemonitors.monitoring.coreos.com
kubectl delete crd thanosrulers.monitoring.coreos.com
```

## Upgrading Chart

```console
helm upgrade [RELEASE_NAME] -n unitest ./kube-prometheus-grafana-blackbox/
```