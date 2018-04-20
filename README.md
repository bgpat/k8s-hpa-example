# k8s-hpa-example
Example to autoscale pods by connection counts

## Install Custom Metrics API Server

```bash
kubectl apply -f addons/custom-metrics/namespace.yml
kubectl apply -f addons/custom-metrics/operator.yml
kubectl apply -f addons/custom-metrics/
```

confitm

```console
$ kubectl api-versions | grep custom.metrics.k8s.io
custom.metrics.k8s.io/v1beta1
$ kubectl --context=minikube get --raw /apis/custom.metrics.k8s.io/v1beta1/namespaces/default/services/custom-metrics/http_requests | jq .
{
  "kind": "MetricValueList",
  "apiVersion": "custom.metrics.k8s.io/v1beta1",
  "metadata": {
    "selfLink": "/apis/custom.metrics.k8s.io/v1beta1/namespaces/default/services/custom-metrics/http_requests"
  },
  "items": [
    {
      "describedObject": {
        "kind": "Service",
        "name": "custom-metrics",
        "apiVersion": "/__internal"
      },
      "metricName": "http_requests",
      "timestamp": "2018-04-20T05:49:56Z",
      "value": "66m"
    }
  ]
}
```

## Deploy sample application

```bash
kubectl apply -f samples/helloworld/
```

confirm

```console
$ kubectl get hpa
NAME         REFERENCE               TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
helloworld   Deployment/helloworld   0/5       2         20        2          4m
```
