# k8s-hpa-example
Example to autoscale pods by connection counts

## Install Custom Metrics API Server

TODO

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
