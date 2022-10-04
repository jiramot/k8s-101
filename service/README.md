# Service
An abstract way to expose an application running on a set of Pods as a network service.

## Create service
```
kubectl apply -f cluster-ip.yaml
```

## Delete service
```
kubectl delete -f cluster-ip.yaml
```

## Test
```
kubectl run curl --rm -ti --image krishgobinath/netutils sh
curl http://nginx-service:8000
curl http://nginx-service.default.svc.cluster.local:8000
```
