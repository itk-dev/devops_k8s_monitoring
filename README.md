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
helm upgrade --install grafana grafana/ --set ingress.domain <DOMAIN>
```

First time login "admin:admin"

### Borads:

* https://raw.githubusercontent.com/nginxinc/nginx-prometheus-exporter/master/grafana/dashboard.json
* https://grafana.com/grafana/dashboards/8588 (k8s)
* https://grafana.com/grafana/dashboards/9614 (igress)
* https://grafana.com/grafana/dashboards/763 (redis)
* https://grafana.com/grafana/dashboards/2322 (es)

## Accessing without ingress

```sh
kubectl port-forward service/prometheus-service 9090
kubectl port-forward service/grafana 3000
```
