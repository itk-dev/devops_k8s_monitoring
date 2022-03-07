# Install monitoring tools
To easily install Prometheus and Grafana to have observability in a cluster this repository comes with helm charts.  

First create monitoring namespace and switch into the namespace.
```sh
kubectl apply -f namespace.yaml
kubens monitoring
```

## Prometheus
```sh
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
helm repo update
```

```sh
helm install prometheus prometheus-community/prometheus \
  --set alertmanager.enabled=false \
  --set configmapReload.alertmanager.enabled=false \
  --set server.ingress.enabled=false \
  --set "server.persistentVolume.accessModes={ReadWriteOnce}" \
  --set server.persistentVolume.size=512Gi \
  --set server.persistentVolume.storageClass=azurefile-premium-retain \
  --set pushgateway.enabled=false --namespace monitoring \
  --set server.resources.limits.memory=4096Mi \
  --set server.resources.requests.memory=4096Mi
```

We do not expose raw Prometheus to the outside, but the UI is available by using port forwarding.
```sh
kubectl port-forward service/prometheus-server 9090:http
```

## Grafana
First time login "admin:admin" please log in and changes this at once the installation has completed.

```sh
helm upgrade --install grafana grafana/grafana --namespace monitoring --set ingress.domain=<DOMAIN>
```

## Patches
If the ingress controller don't have the prometheus annotations... patch it.
```sh
kubectl patch pod ingress-nginx-ingress-controller --patch "$(cat ingress-patch.yaml)"
```
