# Install monitoring tools
To easily install Prometheus and Grafana to have observability in a cluster this repository comes with helm charts.  

First create monitoring namespace and switch into the namespace.
```sh
kubectl apply -f namespace.yaml
kubens monitoring
```

## Prometheus
We have created helm charts to install Prometheus with a service discovery that matches the cluster setup used for cover
service.

```sh
helm upgrade --install prometheus prometheus/ --namespace monitoring
```

We do not expose raw Prometheus to the outside, but the UI is available by using port forwarding.
```sh
kubectl port-forward service/prometheus-service 9090
```

## Grafana
First time login "admin:admin" please log in and changes this at once the installation has completed.

```sh
helm upgrade --install grafana grafana/ --namespace monitoring --set ingress.domain=<DOMAIN>
```

## Patches
If the ingress controller don't have the prometheus annotations... patch it.
```sh
kubectl patch pod ingress-nginx-ingress-controller --patch "$(cat ingress-patch.yaml)"
```
