# Install monitoring tools


## Prometheus

```sh
kubectl apply -f namespace.yaml
```

```sh
kubens monitoring
```

```sh
helm upgrade --install prometheus prometheus/
```

## Grafana

```sh
helm upgrade --install grafana grafana/
```