



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