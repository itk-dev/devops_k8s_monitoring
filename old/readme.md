



## Ingress monitoring

```
kubectl patch pod ingress-nginx-ingress-controller --patch "$(cat ingress-patch.yaml)"
```

https://github.com/helm/charts/tree/master/stable/nginx-ingress

controller.metrics.service.annotations

https://github.com/helm/charts/blob/master/stable/nginx-ingress/templates/controller-deployment.yaml#L26


curl -X POST http://localhost:9090/-/reload

kubectl port-forward service/prometheus-service 9090

kubectl port-forward service/grafana 3000

## Borads:

* https://raw.githubusercontent.com/nginxinc/nginx-prometheus-exporter/master/grafana/dashboard.json
* https://grafana.com/grafana/dashboards/8588 (k8s)
* https://grafana.com/grafana/dashboards/9614 (igress)
* https://grafana.com/grafana/dashboards/763 (redis)
* https://grafana.com/grafana/dashboards/2322 (es)